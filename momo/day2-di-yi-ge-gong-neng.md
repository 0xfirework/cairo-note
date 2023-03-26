# Day2 第一个功能

教程

[https://www.cairo-lang.org/docs/hello\_cairo/intro.html#](https://www.cairo-lang.org/docs/hello\_cairo/intro.html)



//缩写技巧：

每次都要输入cairo-compile很麻烦，可以使用别名

将 cairo-compile 定义为一个更短的命令别名

&#x20;

方法：

在终端中输入以下命令

alias cc='cairo-compile'

使用 cc 这个更短的命令来调用 Cairo 编译器

希望永久保存此别名设置，可以将上述命令添加到 shell 配置文件中

echo "alias cc='cairo-compile'" >> \~/.bashrc

重新打开终端或者执行 source \~/.bashrc 加载新的配置文件即可。

&#x20;

在终端中查看已有的别名：

输入 alias 命令，可以列出所有已定义的别名。

输入 alias 别名名称 命令，可以查看特定别名的定义。

如果您希望删除之前定义的别名，可以使用 unalias 命令来移除别名定义。



\-------



\#断言语句

断言语句：

&#x20;

assert \<expr0> = \<expr1>;

功能1：验证两个值是否相同

功能2：一个内存单元赋值。例如，assert \[ptr] = 0; 将把地址ptr处的内存单元的值设置为0（如果之前没有设置）

&#x20;

main() 函数

%builtins output

from starkware.cairo.common.serialize import serialize\_word

func main{output\_ptr: felt\*}() {

&#x20;   serialize\_word(1234);

&#x20;   serialize\_word(4321);

&#x20;   return ();

}

&#x20;

易错点：Cairo文件的非顶部位置使用了指令。在Cairo中，指令必须出现在文件的开头。

如：%builtins output

from starkware.cairo.common.serialize import serialize\_word

应该放在顶部

&#x20;

&#x20;

运行代码

cairo-compile array\_sum.cairo --output array\_sum\_compiled.json

cairo-run --program=array\_sum\_compiled.json \\

&#x20;   \--print\_output --layout=small

该--layout标志是必需的



内存分配Memory allocation：我们使用标准库函数alloc()来分配一个新的内存段。

常量Constants：Cairo 中的常量是必须是一个整数

&#x20;
