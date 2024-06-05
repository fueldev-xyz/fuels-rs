# 低级调用

通过低级调用，您可以在运行时指定调用的参数，并通过其他合约进行间接调用。

您的调用合约应调用 `std::low_level_call::call_with_function_selector`，并提供：

- 目标合约 ID
- 作为 `Bytes` 编码的函数选择器
- 作为 `Bytes` 编码的调用数据
- 调用数据是否仅包含单个值参数（例如 `u64`）
- `std::low_level_call::CallParams`

```rust,ignore
{{#include ../../../e2e/sway/contracts/low_level_caller/src/main.sw:low_level_call_contract}}
```

在 SDK 方面，您可以使用 `fuels::core::encode_fn_selector` 构造编码的函数选择器，并使用 `fuels::core::calldata!` 宏构造编码的调用数据。

例如，要调用目标合约上的以下函数：

```rust,ignore
{{#include ../../../e2e/sway/contracts/contract_test/src/main.sw:low_level_call}}
```

您可以构造函数选择器和调用数据，并将它们提供给调用合约（就像上面的例子一样）：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:low_level_call}}
```

> 注意：`calldata!` 宏在内部使用默认的 `EncoderConfig` 配置。
