# `Bits256`

在 Fuel 中，称为 `b256` 的类型表示哈希并保存一个 256 位值。Rust SDK 将 `b256` 表示为 `Bits256(value)`，其中 `value` 是 `[u8; 32]`。如果您的合约方法接受 `b256` 作为输入，则在从 SDK 调用时必须传递 `Bits256([u8; 32])`。

下面是一个示例：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:256_arg}}
```

如果您有一个十六进制值作为字符串，并希望将其转换为 `Bits256`，可以使用 `from_hex_str` 来实现：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/bits.rs:from_hex_str}}
```
