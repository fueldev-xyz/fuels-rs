# `ContractId`

与 `Bytes32` 类似，`ContractId` 是对 `[u8; 32]` 的包装器，具有类似的方法并实现相同的特性（参见 [fuel-types 文档](https://docs.rs/fuel-types/0.49.0/fuel_types/struct.ContractId.html)）。

以下是创建 `ContractId` 的主要方法：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:contract_id}}
```
