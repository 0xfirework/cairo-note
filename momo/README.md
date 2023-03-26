# Day1 环境配置

## 安装虚拟机

安装了虚拟机和ubuntu，在GPT的帮助下，终于完成了环境的配置。



教程https://www.cairo-lang.org/docs/quickstart.html



sudo apt install -y libgmp3-dev



安装cairo-langPython包

pip3 install cairo-lang



启动跟踪器

使用--tracer 标志启用 Cairo 追踪器

&#x20;

在文件夹中编译程序

cairo-compile test.cairo --output test\_compiled.json

&#x20;

启动程序

cairo-run --program=test\_compiled.json --print\_output --print\_info --relocate\_prints

