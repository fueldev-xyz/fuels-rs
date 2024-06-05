# 调用参数

<!-- 该部分应解释调用参数是什么以及如何配置它们 -->
<!-- call_params:example:start -->

合约调用的参数包括：

1. 金额
2. 资产 ID
3. 转发的 Gas
<!-- call_params:example:end -->

您可以使用这些参数将资金转发到合约。您可以通过创建 [`CallParameters`](https://docs.rs/fuels/latest/fuels/programs/contract/struct.CallParameters.html) 的实例并将其传递给名为 `call_params` 的链式方法来配置这些参数。

<!-- use_call_params:example:end -->

例如，假设以下合约使用 Sway 的 `msg_amount()` 返回在该交易中发送的金额。

```rust,ignore
{{#include ../../../e2e/sway/contracts/contract_test/src/main.sw:msg_amount}}
```

然后，在 Rust 中，在设置和部署上述合约后，您可以像这样配置发送交易中的金额：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:call_parameters}}
```

<!-- This section should explain why `call_params` returns a result -->
<!-- payable:example:start -->

`call_params` 返回一个结果以确保您不会向一个非可支付的合约方法转发资产。

<!-- payable:example:end -->

在以下示例中，我们尝试向 `non_payable` 转发 `100` 个基本资产。正如其名称所示，`non_payable` 在合约代码中未被注释为 `#[payable]`。使用除 `0` 外的金额传递 `CallParameters` 会导致错误：

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:non_payable_params}}
```

> **注意:** 无论合约方法是否为非可支付，都可以向合约调用转发 Gas。

您还可以使用 `CallParameters::default()` 来使用默认值：

```rust,ignore
{{#include ../../../packages/fuels-core/src/utils/constants.rs:default_call_parameters}}
```

这样：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:call_parameters_default}}
```

<!-- This section should explain what the `gas_forwarded` parameter does -->
<!-- gas:example:start -->

`gas_forwarded` 参数定义了实际合约调用的限制，而不是整个交易的 gas 限制。这意味着它受到交易限制的约束。如果设置为大于可用 gas 的金额，则会转发所有可用 gas。

<!-- gas:example:end -->

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:call_params_gas}}
```

<!-- This section should explain the default forwarding behavior for a call -->
<!-- forwarding:example:start -->

如果您没有设置调用参数或使用 `CallParameters::default()`，则会转发交易的 gas 限制。

<!-- forwarding:example:end -->
