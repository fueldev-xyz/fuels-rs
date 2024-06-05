# RocksDB

RocksDB 可以在本地保存区块链的状态，以便将来使用。

要创建或使用本地数据库，请按照以下说明操作：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:create_or_use_rocksdb}}
```

> 注意：如果指定的数据库不存在，则会在该路径下创建一个新的数据库。要使用上述代码片段，必须存在 `fuel-core` 二进制文件，或者必须同时启用 `fuel-core-lib` 和 `rocksdb` 功能。
