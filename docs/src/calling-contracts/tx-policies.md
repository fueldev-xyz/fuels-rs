# 交易策略

<!-- 本节应解释什么是交易策略以及如何配置它们 -->
<!-- tx_policies:example:start -->

交易策略定义如下：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/wrappers/transaction.rs:tx_policies_struct}}
```

其中：

1. **小费（Tip）** - 用于支付区块生产者以优先处理交易的金额。
2. **见证数据限制（Witness Limit）** - 交易允许的最大见证数据量。
3. **成熟度（Maturity）** - 交易无法包含在此区块之后的区块中。
4. **最大费用（Max Fee）** - 此交易可支付的最大费用。
5. **脚本 Gas 限制（Script Gas Limit）** - 交易在执行其脚本代码时可以消耗的最大 Gas 量。

当未设置**脚本 Gas 限制**时，Rust SDK 将在后台估算消耗的 Gas 并将其设置为限制。

如果未设置**见证数据限制**，SDK 将其设置为交易生成器中定义的所有见证和签名的大小。

您可以通过创建`TxPolicies`实例并将其传递给名为`with_tx_policies`的链式方法来配置这些参数：

<!-- tx_policies:example:end-->

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:tx_policies}}
```

<!-- 本节应解释如何使用默认交易策略 -->
<!-- tx_policies_default:example:start -->

您还可以使用`TxPolicies::default()`来使用默认值。

<!-- tx_policies_default:example:end -->

如下所示：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:tx_policies_default}}
```

正如您可能已经注意到的，`TxPolicies`也可以在部署合约或转移资产时通过将其传递给相应的方法来指定。
