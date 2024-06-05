# 输出变量

<!-- 本节应解释变量输出 -->
<!-- variable_outputs:example:start -->

有时，您调用的合约可能会根据其执行向特定地址转移资金。这种合约调用的底层交易必须具有适当数量的[变量输出](https://specs.fuel.network/master/tx-format/output.html#outputvariable)才能成功。

<!-- variable_outputs:example:end -->

假设您部署了一个具有以下方法的合约：

```rust,ignore
{{#include ../../../e2e/sway/contracts/token_ops/src/main.sw:variable_outputs}}
```

当使用 SDK 调用 `transfer_coins_to_output` 时，您可以通过在调用中链式添加 `append_variable_outputs(amount)` 来指定变量输出的数量。就像这样：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:variable_outputs}}
```

<!-- This section should explain what the `append_variable_outputs` method does -->
<!-- append_variable_outputs:example:start -->

`append_variable_outputs` 方法实际上将给定数量的 `Output::Variable` 添加到交易的输出列表中。该输出类型表示金额和所有者可能会根据交易执行而变化。

<!-- append_variable_outputs:example:end -->

> **注意：** Sway 的 `lib-std` 函数 `mint_to_address` 在内部调用了 `transfer_to_address`，因此您需要像对待 `transfer_to_address` 一样在 Rust SDK 测试中调用 `append_variable_outputs`。
