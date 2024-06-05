# 自定义资产转移

<!-- This section should explain the `add_custom_asset()` method -->
<!-- transfer:example:start -->

SDK 提供了在进行合约调用时在同一交易内转移资产的选项。通过使用 `add_custom_asset()` 方法，您可以指定资产 ID、金额和目标地址：

<!-- transfer:example:end -->

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:add_custom_assets}}
```
