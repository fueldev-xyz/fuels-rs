# 自定义合约和脚本调用

当通过 `ContractCallHandler` 进行合约调用或通过 `ScriptCallHandler` 进行脚本调用时，Rust SDK 在后台使用交易构建器。您可以获取此构建器并在将其提交到网络之前自定义它。交易成功执行后，您可以使用相应的 `ContractCallHandler` 或 `ScriptCallHandler` 生成[调用响应](../calling-contracts/call-response.md)。调用响应可用于解码返回值和日志。以下是合约调用和脚本调用的示例。

## 自定义合约调用

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:contract_call_tb}}
```

## 自定义脚本调用

```rust,ignore
{{#include ../../../e2e/tests/scripts.rs:script_call_tb}}
```
