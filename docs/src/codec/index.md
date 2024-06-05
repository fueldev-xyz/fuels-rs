# 编解码

编码和解码按照[Fuel 规范](https://specs.fuel.network/master/abi/argument-encoding.html)进行。为此，`fuels`使用了[`ABIEncoder`](https://docs.rs/fuels/latest/fuels/core/codec/struct.ABIEncoder.html)和[`ABIDecoder`](https://docs.rs/fuels/latest/fuels/core/codec/struct.ABIDecoder.html)。

## 编码/解码的先决条件

要编码一个类型，必须首先将其转换为[`Token`](https://docs.rs/fuels/latest/fuels/types/enum.Token.html)。这通常通过实现[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)特性来完成。

要解码，也需要提供描述该类型模式的[`ParamType`](https://docs.rs/fuels/latest/fuels/types/param_types/enum.ParamType.html)。这通常通过实现[Parameterize](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)特性来完成。

所有由[`abigen!`](../abigen/index.md)宏生成的类型都实现了[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)和[`Parameterize`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)特性。

`fuels`还包含了以下类型的实现：

- [`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)适用于[此处](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html#implementors)列出的`fuels`拥有的类型以及[一些外部类型](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html#foreign-impls)（例如`u8`、`u16`、`std::vec::Vec<T: Tokenizable>`等）。
- [`Parameterize`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)适用于[此处](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html#implementors)列出的`fuels`拥有的类型以及[一些外部类型](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html#foreign-impls)（例如`u8`、`u16`、`std::vec::Vec<T: Parameterize>`等）。

## 派生特性

如果所有内部类型都实现了派生特性，那么[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)和[`Parameterize`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)都可以为`struct`和`enum`派生：

```rust,ignore
{{#include ../../../examples/macros/src/lib.rs:deriving_traits}}
```

> 注意：
> 为`enum`派生[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)要求所有变体也实现[`Parameterize`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)。

### 调整派生

#### 更改导入位置

派生代码期望`fuels`包通过`::fuels`访问。如果情况并非如此，则需要给派生宏提供`fuels::types`和`fuels::core`的位置。

```rust,ignore
{{#include ../../../examples/macros/src/lib.rs:deriving_traits_paths}}
```

#### 生成 no-std 代码

如果需要生成`no-std`代码：

```rust,ignore
{{#include ../../../examples/macros/src/lib.rs:deriving_traits_nostd}}
```
