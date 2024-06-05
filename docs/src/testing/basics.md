# 测试基础知识

如果你是 Rust 新手，你需要查看这些重要的工具，以帮助你构建测试。

## `assert!` 宏

<!-- assert:example:start -->

你可以使用 `assert!` 宏来断言测试中的某些条件。如果表达式的计算结果为 `false`，则此宏将调用 `panic!()` 并使测试失败。

<!-- assert:example:end -->

<!-- assert_code:example:start -->

```rust, ignore
assert!(value == 5);
```

<!-- assert_code:example:end -->

## `assert_eq!` 宏

<!-- assert_eq:example:start -->

`assert_eq!` 宏的工作原理与 `assert` 宏非常相似，但是它接受两个值，如果这两个值不相等，则会引发 panic。

<!-- assert_eq:example:end -->

<!-- assert_eq_code:example:start -->

```rust, ignore
assert_eq!(balance, 100);
```

<!-- assert_eq_code:example:end -->

## `assert_ne!` 宏

<!-- assert_ne:example:start -->

`assert_ne!` 宏的工作方式与 `assert_eq!` 宏类似，但如果这两个值相等，则会引发 panic。

<!-- assert_ne:example:end -->

<!-- assert_ne_code:example:start -->

```rust, ignore
assert_ne!(address, 0);
```

<!-- assert_ne_code:example:end -->

## `println!` 宏

<!--print_ln:example:start -->

你可以使用 `println!` 宏将值打印到控制台。

<!--print_ln:example:end -->

<!--print_ln_code:example:start -->

```rust, ignore
println!("WALLET 1 ADDRESS {}", wallet_1.address());
println!("WALLET 1 ADDRESS {:?}", wallet_1.address());
```

<!--print_ln_code:example:end -->

<!--print_ln_2:example:start -->

使用 `{}` 将打印值，并使用 `{:?}` 将打印值及其类型。

使用 `{:?}` 还可以打印没有实现 `Display` 特性但实现了 `Debug` 特性的值。或者，你可以使用 `dbg!` 宏来打印这些类型的变量。

<!--print_ln_2:example:end -->

<!--print_ln_dbg_code:example:start -->

```rust, ignore
println!("WALLET 1 PROVIDER {:?}", wallet_1.provider().unwrap());
dbg!("WALLET 1 PROVIDER {}", wallet_1.provider().unwrap());
```

<!--print_ln_dbg_code:example:end -->

<!--fmt:example:start -->

要打印更复杂的类型，可以使用 Rust 标准库中的 `fmt` 模块实现自己的格式化显示方法。

<!--fmt:example:end -->

<!--fmt_code:example:start -->

```rust, ignore
use std::fmt;

struct Point {
x: u64,
y: u64,
}

// 使用 fmt 模块添加打印功能
impl fmt::Display for Point {
fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
write!(f, "value of x: {}, value of y: {}", self.x, self.y)
}
}

let p = Point {x: 1, y: 2};
println!("POINT: {}", p);
```

<!--fmt_code:example:end -->

## 运行命令

你可以运行你的测试来查看它们是否通过或失败

```shell
cargo test
```

<!--outputs:example:start -->

如果测试通过，输出将被隐藏。如果你想要看到来自测试的输出，无论测试是否通过，都可以使用 `nocapture` 标志。

<!--outputs:example:end -->

```shell
cargo test -- --nocapture
```
