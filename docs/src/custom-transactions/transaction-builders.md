# 交易构建器

Rust SDK 通过两个便捷的构建器结构体 `CreateTransactionBuilder`、`ScriptTransactionBuilder` 和 `TransactionBuilder` trait 简化了**创建**和**脚本**交易的创建过程。

在构建器上调用 `build(&provider)` 方法将得到相应的 `CreateTransaction` 或 `ScriptTransaction`，可以将其提交到网络中。

## 交易构建器的作用

> **注意** 本节包含有关构建器内部工作原理的额外信息。如果您只对如何使用它们感兴趣，可以跳到下一节。

构建器在幕后承担了繁重的工作，提供了两个显著的优点：处理断言数据偏移和管理见证索引。

当您的交易涉及到断言作为输入的动态数据，比如向量时，动态数据包含一个指针，指向原始数据的开头。这个指针的有效性取决于交易输入的顺序，任何的移动都可能导致它失效。然而，交易构建器方便地将这些指针的解析推迟到您完成构建过程时。

同样地，为已签名币输入添加签名需要使得已签名币输入包含与见证数组中签名对应的索引。如果见证顺序发生变化，这些索引也可能无效。Rust SDK 也将这些索引的解析推迟到交易最终完成时。它在幕后处理了正确分配索引见证的任务，使您免受在输入定义过程中处理索引复杂性的麻烦。

构建器模式的另一个附加优势是，在交易最终化后，它可以防止发生更改。由构建器产生的交易不允许对可能导致交易 ID 修改的结构进行任何更改。这消除了为将来使用计算和存储交易 ID 而计算交易 ID，然后意外修改交易而导致交易 ID 发生变化的烦恼。

## 创建自定义交易

下面是一个示例，概述了交易构建器的一些特性。

在这个场景中，我们有一个断言，它持有 ID 为 **bridged_asset_id** 的一些桥接资产。如果交易将基础资产的 **ask_amount** 发送给 **receiver** 地址，断言会释放其锁定的资产：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_receiver}}
```

我们的目标是创建一个交易，使用我们的热钱包将 **ask_amount** 转移给 **receiver**，然后将解锁的断言资产发送到作为我们冷存储的第二个钱包。

让我们首先实例化一个构建器。由于我们不打算部署合约，因此 `ScriptTransactionBuilder` 是适当的选择：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx}}
```

接下来，我们需要定义基础资产的交易输入，这些输入的总和为 **ask_amount**。我们还需要定义交易输出，这些输出将把这些资产分配给断言地址，从而解锁它。方法 `get_asset_inputs_for_amount` 和 `get_asset_outputs_for_amount` 可以帮助实现这一点。我们需要指定资产 ID、目标金额和目标地址：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_io_base}}
```

让我们重复相同的过程，但这次是为了将断言持有的资产转移到我们的冷存储：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_io_other}}
```

我们将所有的输入和输出组合起来，并设置到构建器中：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_io}}
```

由于我们使用的是需要签名的币，我们必须使用以下方法将签名者添加到交易构建器中：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_add_signer}}
```

> **注意** 在调用 `adjust_for_fee()` 之前最好先添加签名者，因为估算将包括见证的大小。

我们在停止考虑交易输入之前还需要做一件事情。执行交易还会产生一笔费用，该费用由基础资产支付。我们的基础资产输入需要足够大，以便总金额覆盖交易费用和任何其他操作。`Account` trait 允许我们使用 `adjust_for_fee()` 来调整交易输入，以确保覆盖费用。`adjust_for_fee()` 的第二个参数是我们预计的交易基础资产总金额，无论费用如何。在我们的情况下，这是我们转移到断言的 **ask_amount**。

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_adjust}}
```

> **注意** 建议在调用 `adjust_for_fee()` 之前添加签名者，因为估算将包括见证人的大小。

我们也可以定义交易策略。例如，我们可以通过以下方式限制燃气价格：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_policies}}
```

在调用 `build()` 之前，我们的构建器需要来自热钱包的签名以解锁其硬币，并通过提供者提交生成的交易：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_build}}
```

最后，我们验证交易成功，并确保冷存储现在确实持有桥接资产：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_tx_verify}}
```

## 构建无签名的交易

如果您需要构建无签名的交易，这在估算交易成本或模拟时非常有用，您可以使用 `build_without_signatures(&provider)` 方法，然后稍后对构建的交易进行签名。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:tb_build_without_signatures}}
```

> **注意** 与向交易构建器添加签名者相反，当对构建的交易进行签名时，您必须确保签名的顺序与签名输入的顺序相匹配。具有相同所有者的多个已签名输入将具有相同的见证人索引。
