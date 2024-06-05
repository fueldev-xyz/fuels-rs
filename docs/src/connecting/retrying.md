# 重试请求

当接收到 `io::Error` 时，可以配置 [`Provider`](https://docs.rs/fuels/0.62.0/fuels/accounts/provider/struct.Provider.html) 进行重试请求。

> 注意：当前所有节点错误都作为 `io::Error` 接收。因此，如果配置了重试，即使例如事务验证失败，也会进行重试。

我们可以通过以下方式配置重试尝试次数和重试策略。

## `RetryConfig`

可以通过提供自定义的 `RetryConfig` 来更改重试行为。它允许配置尝试的最大次数和使用的间隔策略。

```rust, ignore
{{#include ../../../packages/fuels-accounts/src/provider/retry_util.rs:retry_config}}
```

```rust, ignore
{{#include ../../../examples/providers/src/lib.rs:configure_retry}}
```

## 间隔策略 - `Backoff`

`Backoff` 定义了不同的策略来管理重试尝试之间的间隔。
每种策略都允许您根据尝试次数自定义新尝试之前的等待时间。

### 变体

- `Linear(Duration)`: `Default` 使用线性增加的方式增加等待时间。
- `Exponential(Duration)`: 每次尝试时等待时间加倍。
- `Fixed(Duration)`: 尝试之间使用恒定的等待时间。

```rust, ignore
{{#include ../../../packages/fuels-accounts/src/provider/retry_util.rs:backoff}}
```
