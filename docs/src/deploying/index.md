# 部署合约

在 SDK 中，有两种主要的方法来处理合约：使用 SDK 部署合约或使用 SDK 与现有合约进行交互。

## 部署合约二进制文件

<!-- This section should explain the artifacts produced by `forc build`  -->
<!-- build:example:start -->

一旦您用 Sway 编写了一个合约，并使用 `forc build` 编译了它，您将手头拥有两个重要的构件：编译后的二进制文件和 JSON ABI 文件。

<!-- build:example:end -->

> 注意：阅读[这里](https://docs.fueldev.xyz/guides/quickstart/)了解有关如何使用 Sway 的更多信息。

以下是使用 SDK 部署合约的方法。有关此过程中每个组件的更多详细信息，请阅读[abigen 宏](../abigen/the-abigen-macro.md)、[FuelVM 二进制文件](./the-fuelvm-binary-file.md)和[JSON ABI 文件](../abigen/the-json-abi-file.md)。

<!-- This section should explain how to load and deploy a contract  -->
<!-- deploy:example:start -->

首先，使用 `Contract::load_from` 函数加载一个带有 `LoadConfiguration` 的合约二进制文件。如果您只对合约的单个实例感兴趣，请使用默认配置：`LoadConfiguration::default()`。加载合约二进制文件后，您可以使用 `deploy()` 方法将合约部署到区块链上。

<!-- deploy:example:end -->

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:deploy_contract}}
```

或者，您可以使用 `LoadConfiguration` 配置合约的加载方式。`LoadConfiguration` 允许您：

- 使用 `Salt` 加载相同的合约二进制文件以获取一个新的 `contract_id`
- 更改合约的存储槽
- 更新合约的配置参数

> 注意：下一节将提供有关如何使用 `configurables` 的更多信息。

此外，您还可以在部署加载的合约时设置自定义的 `TxParameters`。

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:deploy_with_parameters}}
```

合约部署后，您可以像这样使用合约的方法：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:use_deployed_contract}}
```

> 注意：重新部署现有的 `Contract` 时，请确保使用唯一的 salt 对其进行初始化，以防止由于合约 ID 冲突而导致的部署失败。为此，利用 `with_salt` 方法使用新的 salt 克隆现有的 `Contract`。
