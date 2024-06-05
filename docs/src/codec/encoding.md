# 编码

请务必阅读编码的[先决条件](./index.md#prerequisites-for-decodingencoding)。

编码是通过[`ABIEncoder`](https://docs.rs/fuels/latest/fuels/core/codec/struct.ABIEncoder.html)完成的：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:encoding_example}}
```

还有一个快捷宏可以编码多个实现了[`Tokenizable`](https://docs.rs/fuels/latest/fuels/core/traits/trait.Tokenizable.html)的类型：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:encoding_example_w_macro}}
```

## 配置编码器

可以配置编码器以限制其资源消耗：

```rust,ignore
{{#include ../../../examples/codec/src/lib.rs:configuring_the_encoder}}
```

`EncoderConfig`的默认值为：

```rust,ignore
{{#include ../../../packages/fuels-core/src/codec/abi_encoder.rs:default_encoder_config}}
```

## 配置合约/脚本调用的编码器

您还可以配置用于编码合约方法参数的编码器：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:contract_encoder_config}}
```

同样的方法也适用于脚本调用。
