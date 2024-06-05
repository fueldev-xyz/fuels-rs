# `Bytes`

在 Fuel 中，称为 `Bytes` 的类型表示紧密打包的字节集合。Rust SDK 将 `Bytes` 表示为 `Bytes(Vec<u8>)`。以下是在合约调用中使用 `Bytes` 的示例：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:bytes_arg}}
```

如果您有一个十六进制值作为字符串，并希望将其转换为 `Bytes`，可以使用 `from_hex_str` 来实现：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/bytes.rs:bytes_from_hex_str}}
```
