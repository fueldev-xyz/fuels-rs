# `Address`

`Address`类似于`Bytes32`，是对`[u8; 32]`的封装，具有类似的方法，并实现了相同的特征（参见[fuel-types 文档](https://docs.rs/fuel-types/latest/fuel_types/struct.Address.html)）。

以下是创建`Address`的主要方法：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:address}}
```
