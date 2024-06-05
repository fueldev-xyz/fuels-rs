# 与合约交互

如果您已经部署了一个合约，并想使用 SDK 调用其方法，但不想再次部署它，您只需知道您已部署的合约的合约 ID。您可以跳过整个部署设置过程，直接调用 `::new(contract_id, wallet)`。例如：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:deployed_contracts}}
```

上面的示例假设您的合约 ID 字符串是以 `bech32` 格式编码的。您可以通过人类可读部分 "fuel" 后跟分隔符 "1" 来识别它。然而，当使用其他 Fuel 工具时，您可能会得到一个十六进制编码的合约 ID 字符串。在这种情况下，您可以按以下方式创建您的合约实例：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:deployed_contracts_hex}}
```

您可以在此了解有关 Fuel SDK `bech32` 类型的更多信息[此处](../types/bech32.md)。
