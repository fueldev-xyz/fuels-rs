# `Bytes32`

在 Sway 和 FuelVM 中，`Bytes32` 表示哈希。它们保存一个 256 位（32 字节）的值。`Bytes32` 是对 `u8` 的大小为 32 的切片的包装器：`pub struct Bytes32([u8; 32]);`。

以下是创建 `Bytes32` 的主要方法：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bytes32}}
```

`Bytes32` 还实现了 `fmt` 模块的 `Debug`、`Display`、`LowerHex` 和 `UpperHex` 特性。例如，您可以使用以下代码获取显示和十六进制表示：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bytes32_format}}
```

有关已实现的方法和特性的完整列表，请参阅 [fuel-types 文档](https://docs.rs/fuel-types/latest/fuel_types/struct.Bytes32.html)。

> **注意：** 在 Fuel 中，还有一种特殊类型叫做 `b256`，它类似于 `Bytes32`；也用于表示哈希，并且保存一个 256 位的值。在 Rust 中，通过 SDK，这被表示为 `Bits256(value)`，其中 `value` 是 `[u8; 32]`。如果您的合约方法接受 `b256` 作为输入，那么在从 SDK 调用时，您只需要传递 `Bits256([u8; 32])`。
