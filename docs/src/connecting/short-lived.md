# 使用 SDK 运行短暂的 Fuel 节点

您可以使用 SDK 快速启动一个本地的 Fuel 节点，最好是短暂的。然后，您可以实例化一个 Fuel 客户端，指向这个节点。

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:instantiate_client}}
```

这种方法非常适合合约测试。

您也可以使用测试助手 `setup_test_provider()`：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_random_wallet}}
```

您还可以使用 `launch_provider_and_get_wallet()`，它将 `setup_test_provider()` 和钱包创建封装在一个方法中：

```rust,ignore
let wallet = launch_provider_and_get_wallet().await?;
```

## 功能

### fuel-core-lib

`fuel-core-lib` 功能允许我们在本地机器上运行 `fuel-core` 节点而无需安装 `fuel-core` 二进制文件。使用 `fuel-core-lib` 功能标志意味着下载运行 fuel-core 节点所需的所有依赖项。

```rust,ignore
fuels = { version = "0.63.0", features = ["fuel-core-lib"] }
```

### RocksDB

`rocksdb` 是一个附加功能，当与 `fuel-core-lib` 结合使用时，提供了在使用 `fuel-core` 作为库时的持久存储功能。

```rust,ignore
fuels = { version = "0.63.0", features = ["rocksdb"] }
```
