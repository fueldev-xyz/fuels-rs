# JSON ABI 文件

<!-- 该部分应讨论 ABI 的重要性 -->
<!-- abi:example:start -->

无论您是想部署还是连接到现有的智能合约，JSON ABI 文件都非常重要：它告诉 SDK 您的智能合约中的[ABI 方法](https://docs.fueldev.xyz/guides/quickstart/building-a-smart-contract/#abi)。

<!-- abi:example:end -->

对于与上面相同的 Sway 代码示例：

```Rust
contract;

abi MyContract {
    fn test_function() -> bool;
}

impl MyContract for Contract {
    fn test_function() -> bool {
        true
    }
}
```

JSON ABI 文件如下所示：

```json
$ cat out/release/my-test-abi.json
[
  {
    "type": "function",
    "inputs": [],
    "name": "test_function",
    "outputs": [
      {
        "name": "",
        "type": "bool",
        "components": null
      }
    ]
  }
]
```

Fuel Rust SDK 将以此文件作为输入，并生成相应的方法（如果适用，还包括自定义类型），您可以从 Rust 代码中调用这些方法。
