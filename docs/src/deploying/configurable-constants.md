# 可配置常量

在 Sway 中，您可以定义 `configurable` 常量，这些常量可以在 SDK 中的合约部署过程中进行更改。以下是定义常量的示例。

```rust,ignore
{{#include ../../../e2e/sway/contracts/configurables/src/main.sw}}
```

每个可配置的常量将在 SDK 中获得一个专用的 `with` 方法。例如，常量 `STR_4` 将获得 `with_STR_4` 方法，该方法接受与合约代码中定义的相同类型。以下是一个示例，其中我们链接了几个 `with` 方法，并使用新常量部署了合约。

```rust,ignore
{{#include ../../../e2e/tests/configurables.rs:contract_configurables}}
```
