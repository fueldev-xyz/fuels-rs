# 运行脚本

您可以使用脚本的 JSON-ABI 和其二进制文件的路径来运行脚本。您可以带参数运行脚本。为此，您必须使用之前见过的 `abigen!` 宏。

```rust,ignore
{{#include ../../e2e/tests/scripts.rs:script_with_arguments}}
```

此外，如果出于任何原因需要将提交与值检索分开，您可以这样做：

```rust,ignore
{{#include ../../e2e/tests/scripts.rs:submit_response_script}}
```

## 使用事务策略运行脚本

传递事务策略的方法与[合约](./calling-contracts/tx-policies.md)相同。作为提醒，工作流程如下：

```rust,ignore
{{#include ../../e2e/tests/scripts.rs:script_with_tx_policies}}
```

## 日志

脚本调用提供与合约调用相同的日志功能，`decode_logs()` 和 `decode_logs_with_type<T>()`。作为提醒，工作流程如下：

```rust,ignore
{{#include ../../e2e/tests/logs.rs:script_logs}}
```

## 从脚本调用合约

脚本使用与[合约方法](./calling-contracts/other-contracts.md)相同的接口来设置外部合约。

以下是使用 `with_contracts(&[&contract_instance, ...])` 的示例。

```rust,ignore
{{#include ../../e2e/tests/logs.rs:external_contract}}
```

这是使用 `with_contract_ids(&[&contract_id, ...])` 的示例。

```rust,ignore
{{#include ../../e2e/tests/logs.rs:external_contract_ids}}
```

## 可配置的常量

与合约一样，您可以在 `scripts` 中定义可配置的常量，这些常量可以在脚本执行过程中进行更改。以下是定义常量的示例。

```rust,ignore
{{#include ../../e2e/sway/scripts/script_configurables/src/main.sw}}
```

每个可配置的常量都将在 SDK 中获得一个专用的 `with` 方法。例如，常量 `STR_4` 将获得 `with_STR_4` 方法，该方法接受与 sway 中定义的相同类型。以下是一个示例，其中我们链式调用了多个 `with` 方法，并使用新的常量执行了脚本。

```rust,ignore
{{#include ../../e2e/tests/configurables.rs:script_configurables}}
```
