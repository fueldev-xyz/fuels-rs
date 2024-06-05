# `AssetId`

`AssetId`类似于`Bytes32`，是对`[u8; 32]`的封装，具有类似的方法，并实现了相同的特征（请参阅[fuel-types documentation](https://docs.rs/fuel-types/0.49.0/fuel_types/struct.AssetId.html)）。

以下是创建`AssetId`的主要方法：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:asset_id}}
```
