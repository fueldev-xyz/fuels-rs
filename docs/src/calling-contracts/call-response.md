# 调用响应

<!-- 这一部分应该解释为什么经常要链接 `.call().await.unwrap()` -->
<!-- chaining:example:start -->

您可能已经注意到您经常需要链接 `.call().await.unwrap()`。这是因为：

1. 您必须在 `.call()` 和 `.simulate()` 之间进行选择（下一节将详细介绍）。
2. 合约调用是异步的，因此您可以选择 `.await` 它或执行并发任务，充分利用 Rust 的异步功能。
3. 对合约调用返回的 `Result<FuelCallResponse, Error>` 进行 `.unwrap()`。

<!-- chaining:example:end -->

<!-- 这一部分应该解释 `FuelCallResponse` 是什么 -->
<!-- call_resp:example:start -->

一旦解开 `FuelCallResponse`，您就可以访问该结构体：

<!-- call_resp:example:end -->

```rust,ignore
{{#include ../../../packages/fuels-programs/src/call_response.rs:fuel_call_response}}
```

<!-- 这一部分应该解释 `FuelCallResponse` 结构体的字段 -->
<!-- call_resp_fields:example:start -->

其中 `value` 将保存其相应合约方法返回的值，由 FuelVM 返回的确切类型表示，例如，如果您的合约返回 FuelVM 的 `u64`，那么 `value` 的 `D` 将是 `u64`。如果它是 FuelVM 的元组 `(u8,bool)`，那么 `D` 将是 `(u8,bool)`。如果它是自定义类型，例如，一个包含两个组件的 Sway 结构体 `MyStruct`，一个 `u64` 和一个 `b256`，那么 `D` 将是在编译时生成的结构体，称为 `MyStruct`，其中包含 `u64` 和 `[u8; 32]`（在 Rust 中等价于 `b256`）。

- `receipts` 将保存由该特定合约调用生成的所有 [receipts](https://specs.fuel.network/master/protocol/abi/receipts.html)。
- `gas_used` 是合约调用消耗的 gas 数量。
- `tx_id` 将保存相应提交的交易的 ID。

<!-- call_resp_fields:example:end -->

## 错误处理

<!-- 这一部分应该解释如何使用调用响应的 `is_ok` 和 `is_err` 方法 -->
<!-- call_resp_ok:example:start -->

您可以使用 `is_ok` 和 `is_err` 方法来检查合约调用的 `Result` 是否是 `Ok` 或包含错误。这些方法将返回 `true` 或 `false`。

<!-- call_resp_ok:example:end -->

<!-- 这一部分应该展示如何使用调用响应的 `is_ok` 和 `is_err` 方法的示例 -->
<!-- call_resp_ok_code:example:start -->

```rust, ignore
let is_ok = response.is_ok();
let is_error = response.is_err();
```

<!-- call_resp_ok_code:example:end -->

<!-- 这一部分应该解释如何使用调用响应的 `unwrap_err` 方法 -->
<!-- call_resp_error:example:start -->

如果 `is_err` 返回 `true`，您可以使用 `unwrap_err` 方法来解包错误消息。

<!-- call_resp_error:example:end -->

<!-- 这一部分应该展示如何解包调用响应的错误 -->
<!-- call_resp_error_code:example:start -->

```rust, ignore
if response.is_err() {
    let err = response.unwrap_err();
    println!("ERROR: {:?}", err);
};
```

<!-- call_resp_error_code:example:end -->
