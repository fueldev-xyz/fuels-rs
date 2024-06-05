# `Bech32`

`Bech32Address`和`Bech32ContractId`使得地址和合约 ID 可以以`bech32`格式使用。它们可以轻松地转换为它们的对应项`Address`和`ContractId`。

以下是创建`Bech32Address`的主要方法，但请注意，同样适用于`Bech32ContractId`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bech32}}
```

> **注意：**当从`Address`或`ContractId`创建`Bech32Address`或`Bech32ContractId`时，`HRP`（可读部分）默认设置为 **"fuel"**。
