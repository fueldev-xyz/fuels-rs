# 解码

请务必阅读解码的[先决条件](./index.md#prerequisites-for-decodingencoding)。

解码是通过[`ABIDecoder`](https://docs.rs/fuels/latest/fuels/core/codec/struct.ABIDecoder.html)完成的：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:decoding_example}}
```

首先是转换为[`Token`](https://docs.rs/fuels/latest/fuels/types/enum.Token.html)，然后通过[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)特性，转换为所需的类型。

如果类型来自[`abigen!`](../abigen/index.md)（或使用[`::fuels::macros::TryFrom`](https://docs.rs/fuels/latest/fuels/macros/derive.TryFrom.html)派生），那么您也可以使用`try_into`将字节转换为同时实现[`Parameterize`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Parameterize.html)和[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)的类型：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:decoding_example_try_into}}
```

在内部，调用了[`try_from_bytes`](https://docs.rs/fuels/latest/fuels/core/codec/fn.try_from_bytes.html)，这与前面的示例所做的事情相同。

## 配置解码器

可以配置解码器以限制其资源消耗：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:configuring_the_decoder}}
```

<!-- TODO: Add a link once a release is made -->
<!-- https://docs.rs/fuels/latest/fuels/core/codec/struct.DecoderConfig.html -->

有关每个配置值的解释，请访问`DecoderConfig`。

<!-- TODO: add a link once a release is made -->
<!-- https://docs.rs/fuels/latest/fuels/core/codec/struct.DecoderConfig.html -->

`DecoderConfig`的默认值为：

```rust,ignore
{{#include ../../../packages/fuels-core/src/codec/abi_decoder.rs:default_decoder_config}}
```

## 配置合约/脚本调用的解码器

您还可以配置用于解码合约方法返回值的解码器：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:contract_decoder_config}}
```

同样的方法也适用于脚本调用。
