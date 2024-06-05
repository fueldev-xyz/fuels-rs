# `String`

Rust SDK 将 Fuel 的`String`表示为`SizedAsciiString<LEN>`，其中泛型参数`LEN`是给定字符串的长度。这种抽象是必要的，因为 Fuel 和 Sway 中的所有字符串都是静态大小的，即你必须预先知道字符串的大小。

下面是使用`SizedAsciiString`创建简单字符串的方法：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/sized_ascii_string.rs:string_simple_example}}
```

为了更轻松地使用`SizedAsciiString`，你可以使用`try_into()`将 Rust 的`String`转换为`SizedAsciiString`，并使用`into()`将`SizedAsciiString`转换为 Rust 的`String`。以下是一些示例：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/sized_ascii_string.rs:conversion}}
```

如果你的合约方法接受和返回 Sway 的`str[23]`，在使用 SDK 时，此方法将接受并返回`SizedAsciiString<23>`，你可以像这样向其传递字符串：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:contract_takes_string}}
```
