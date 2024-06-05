# 连接到 Fuel 节点

<!-- This section should explain at a high level the main ways to connect to a node with the Rust SDK and when they are appropriate to use-->
<!-- rs_node:example:start -->

在高层次上，您可以使用 Fuel Rust SDK 构建基于 Rust 的应用程序，通过与 Sway 编写的智能合约进行交互，在 Fuel 虚拟机上运行计算。

为了使这种交互正常工作，SDK 必须能够与 `fuel-core` 节点进行通信；您有两种选择：

1. 使用测试网或运行 Fuel 节点（使用 `fuel-core`），并实例化一个指向该节点 IP 和端口的提供程序。
2. 使用 SDK 的本地 `launch_provider_and_get_wallet()`，它会运行一个短暂的测试 Fuel 节点；

第二种选项非常适合智能合约测试，因为您可以在特定的测试用例之间快速启动和关闭节点。

对于应用程序构建，您应该使用第一种选项。

<!-- rs_node:example:end -->
