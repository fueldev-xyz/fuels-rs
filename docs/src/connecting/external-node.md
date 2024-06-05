# 连接到测试网或外部节点

我们可以通过以下示例与`Testnet`节点进行交互。

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:connect_to_testnet}}
```

> 有关各种测试网络及其项目的最佳工具链配置的详细信息，请访问以下链接：
>
> [networks](https://fuelbook.fuel.network/master/networks/networks.html)

在代码示例中，我们连接了一个新的提供程序到 Testnet 节点，并从私钥创建了一个新的钱包。

> **注意：** 在 Testnet 上的新钱包将不包含任何资产！您可以通过将钱包地址提供给以下水龙头来获得资产：
>
> [faucet-beta-5.fuel.network](https://faucet-beta-5.fuel.network)
>
> 一旦资产转移到钱包中，您就可以通过提供私钥在其他测试中重用它！
>
> 除了水龙头之外，还有一个 Testnet 的区块浏览器位于
>
> [block-explorer](https://fuellabs.github.io/block-explorer-v2)

如果您想连接到另一个节点，只需更改 URL 或 IP 和端口即可。例如，要连接到使用`fuel-core`创建的本地节点，可以使用：

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:local_node_address}}
```
