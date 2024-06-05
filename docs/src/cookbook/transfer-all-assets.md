# 转移所有资产

`transfer()` 方法让您可以转移单个资产，但如果您需要将所有资产移动到另一个钱包呢？您可以重复调用 `transfer()` 方法，每次启动一个交易，或者将所有转移捆绑到一个交易中。本章将指导您如何创建自定义交易，用于转移钱包拥有的所有资产。

首先，让我们快速设置环境：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:transfer_multiple_setup}}
```

我们创建了两个带有随机地址的钱包。接下来，我们希望其中一个钱包拥有一些随机资产，因此我们使用 `setup_multiple_assets_coins()` 方法为其设置了资产。创建了这些资产后，我们启动了一个提供程序，并将其分配给之前创建的钱包。

交易需要定义输入和输出币。假设我们不知道 `wallet_1` 拥有哪些资产。我们检索其余额，即由资产 ID 和相应金额组成的元组。这使我们可以使用助手函数 `get_asset_inputs_for_amount()` 和 `get_asset_outputs_for_amount()` 来创建适当的输入和输出。

为了简单起见，我们避免转移基础资产，以免担心交易费用：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:transfer_multiple_input}}
```

现在，唯一剩下的就是构建交易了。我们使用 `ScriptTransactionBuilder` 构建交易，由 `wallet_1` 签名后发送。我们通过检查接收钱包中的余额数量和金额来确认交易已成功：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:transfer_multiple_transaction}}
```
