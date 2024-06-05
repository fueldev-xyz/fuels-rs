# Vectors

## 传递向量

你可以透明地将 Rust 的`std::vec::Vec`传递到你的合约方法中。以下代码调用了一个接受`Vec<SomeStruct<u32>>`的 Sway 合约方法。

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:passing_in_vec}}
```

你可以像使用任何其他类型一样使用向量--例如`[Vec<u32>; 2]`或`SomeStruct<Vec<Bits256>>`等。

## 返回向量

从合约方法返回向量是支持的，但有一个限制，就是你不能将它们嵌套在另一个类型内部。这个限制是暂时的。

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:returning_vec}}
```

> **注意：你仍然可以与包含返回向量嵌套在另一个类型内部的方法的合约进行交互，只是不能与方法本身进行交互**
