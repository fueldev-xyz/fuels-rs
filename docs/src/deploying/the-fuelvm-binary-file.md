# FuelVM 二进制文件

`forc build` 命令会编译您的 Sway 代码并生成字节码：Fuel 虚拟机将解释的二进制代码。例如，下面的智能合约：

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

经过 `forc build` 后，会得到一个包含以下内容的二进制文件：

```terminal
$ cat out/release/my-test.bin
G4]�]D`I]C�As@
           6]C�$@!QK%
```

这看起来非常难以阅读！但是，`forc` 有一个很好的字节码解释器：`forc parse-bytecode`，它将解释该二进制数据并输出等效的 FuelVM 汇编代码：

```terminal
$ forc parse-bytecode out/release/my-test.bin
half-word   byte   op                raw           notes
        0   0      JI(4)             90 00 00 04   jump to byte 16
        1   4      NOOP              47 00 00 00
        2   8      Undefined         00 00 00 00   data section offset lo (0)
        3   12     Undefined         00 00 00 34   data section offset hi (52)
        4   16     LW(63, 12, 1)     5d fc c0 01
        5   20     ADD(63, 63, 12)   10 ff f3 00
        6   24     LW(17, 6, 73)     5d 44 60 49
        7   28     LW(16, 63, 1)     5d 43 f0 01
        8   32     EQ(16, 17, 16)    13 41 14 00
        9   36     JNZI(16, 11)      73 40 00 0b   conditionally jump to byte 44
       10   40     RVRT(0)           36 00 00 00
       11   44     LW(16, 63, 0)     5d 43 f0 00
       12   48     RET(16)           24 40 00 00
       13   52     Undefined         00 00 00 00
       14   56     Undefined         00 00 00 01
       15   60     Undefined         00 00 00 00
       16   64     XOR(20, 27, 53)   21 51 bd 4b
```

如果您想要使用 SDK 部署智能合约，这个二进制文件非常重要；这就是我们将在交易中发送到 FuelVM 的内容。
