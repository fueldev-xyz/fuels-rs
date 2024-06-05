# 调用其他合约

如果您的合约方法调用其他合约，则必须为您的交易添加适当的 `Inputs` 和 `Outputs`。为了方便起见，`ContractCallHandler` 提供了准备这些输入和输出的方法。您可以使用两种方法：`with_contracts(&[&contract_instance, ...])` 和 `with_contract_ids(&[&contract_id, ...])`。

`with_contracts(&[&contract_instance, ...])` 需要使用 `abigen` 宏创建的合约实例。使用此方法设置外部合约时，来自外部合约的日志和 require revert 错误可以由调用合约传播和解码。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:external_contract}}
```

但是，如果您不需要解码日志或者没有使用 `abigen` 宏生成的合约实例，您可以使用 `with_contract_ids(&[&contract_id, ...])` 并提供所需的合约 id。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:external_contract_ids}}
```
