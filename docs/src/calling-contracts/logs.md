# 日志

每当您在合约方法中记录一个值时，生成的日志条目将被添加到日志收据中，并且变量类型将记录在合约的 ABI 中。SDK 允许您将这些值解析为 Rust 类型。

考虑以下合约方法：

```rust,ignore
{{#include ../../../e2e/sway/logs/contract_logs/src/main.sw:produce_logs}}
```

您可以通过从 `FuelCallResponse` 调用 `decode_logs_with_type::<T>` 来在 Rust 中访问记录的值，其中 `T` 是您想要检索的记录变量的类型。结果将是一个 `Vec<T>`：

```rust,ignore
{{#include ../../../e2e/tests/logs.rs:produce_logs}}
```

您可以使用 `decode_logs()` 函数来检索一个 `LogResult` 结构体，其中包含一个 `results` 字段，该字段是一个 `Result<String>` 值的向量，表示每个日志解码的成功或失败。

```rust, ignore
{{#include ../../../e2e/tests/logs.rs:decode_logs}}
```

由于可能存在性能问题，不建议在非调试场景下使用 `decode_logs()`。

> **注意：** 不能直接记录字符串片段。请先使用 `__to_str_array()` 函数将其转换为 `str[N]`。
