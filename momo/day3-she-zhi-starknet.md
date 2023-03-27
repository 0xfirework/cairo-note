# Day3 设置starknet

### 设置网络

```
export STARKNET_NETWORK=alpha-goerli
```

### 选择钱包提供商

```
export STARKNET_WALLET=starkware.starknet.wallets.open_zeppelin.OpenZeppelinAccount
```

### 创建一个帐户

运行以下命令初始化账户：

```
starknet new_account
```

输出应类似于：

```
Account address: 0x78d796e87cfa496bffad27be9ed42f2709bd6e32a6366f842fdf38664a1412d
Public key: ...
Move the appropriate amount of funds to the account, and then deploy the account
by invoking the 'starknet deploy_account' command.

NOTE: This is a modified version of the OpenZeppelin account contract. The signature is computed
differently.
```

我的地址：0x019531fecb999a7be03c825057383ccc2db704f42c2c1ecec77b3b14a9ceb0a3

## 转入g-ETH至账户

水龙头：[https://faucet.goerli.starknet.io/](https://faucet.goerli.starknet.io/)

要估算部署帐户所需的费用，请运行以下命令：

```
starknet deploy_account --simulate
```

估算部署帐户所需的费用，请运行以下命令：

```
starknet deploy_account --simulate
```

### 部署账户

要部署您初始化的帐户，请运行以下命令：

```
starknet deploy_account
```

输出应类似于：

```
Sent deploy account contract transaction.

Contract address: ...
Transaction hash: ...
```



## 15拼图

临时变量 tempvar

```
tempvar row = loc.row;
```

局部变量

```
func verify_adjacent_locations(
    loc0: Location*, loc1: Location*
) {
    alloc_locals;//为局部变量分配内存空间
    local row_diff = loc0.row - loc1.row;   //局部变量
    local col_diff = loc0.col - loc1.col;

    if (row_diff == 0) {
        // The row coordinate is the same. Make sure the
        // difference in col is 1 or -1.
        assert col_diff * col_diff = 1;
        return ();
    } else {
        // Verify the difference in row is 1 or -1.
        assert row_diff * row_diff = 1;
        // Verify that the col coordinate is the same.
        assert col_diff = 0;
        return ();
    }
}
```

临时变量不需要事先分配内存，但它们的范围是有限的。

局部变量位于函数堆栈的开头，因此需要使用指令预先分配`alloc_locals`，但在函数的整个执行过程中都可以访问它们。



### 验证位置列表

```
func verify_location_list(loc_list: Location*, n_steps) {
    // Always verify that the location is valid, even if
    // n_steps = 0 (remember that there is always one more
    // location than steps).
    verify_valid_location(loc=loc_list);

    if (n_steps == 0) {
        return ();
    }

    verify_adjacent_locations(
        loc0=loc_list, loc1=loc_list + Location.SIZE
    );

    // Call verify_location_list recursively.
    verify_location_list(
        loc_list=loc_list + Location.SIZE, n_steps=n_steps - 1
    );
    return ();
}
```

对SIZE的疑问

`loc_list + Location.SIZE` 是一个指针算术运算，将 `loc_list` 的地址加上 `Location.SIZE` 的值，从而得到指向下一个位置的指针 `loc1`。这里假定 `Location` 是一个结构体或类，并且 `Location.SIZE` 是这个结构体或类占用内存的大小（以字节为单位）。

例如，如果 `Location` 结构体的大小为 8 字节（即一个双精度浮点数的大小），则当 `loc_list` 指向列表中的第一个位置时，`loc_list + Location.SIZE` 将返回指向列表中的第二个位置的指针。







