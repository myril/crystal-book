# 通过源文件

如果你想做出贡献, 也许你想从源文件中来安装Crystal.

1. [安装最新的Crystal版本](https://crystal-lang.org/docs/installation). 为了编译Crystal, 你需要Crystal :).

2. 确保在环境变量中存在支持的LLVM版本. 目前Crystal支持LLVM 3.8, 3.9, 4.0, and 5.0. 如果可能请用最新版本.

3. 确保暗转改了[所有必须的类库](https://github.com/crystal-lang/crystal/wiki/All-required-libraries). 你也许想要了解[贡献指南](https://github.com/crystal-lang/crystal/blob/master/CONTRIBUTING.md).

4. 克隆资源库:

```
git clone https://github.com/crystal-lang/crystal
```

5. 运行`make`来构建你自己的编译器版本.
6. 运行`make spec`确保所有测试通过, 并且你已经正确安装了所有内容.
7. 用`bin/crystal`来运行你的crystal文件.

如果你想了解更多关于`bin/crystal`的信息, 可以查看[使用编译器](https://crystal-lang.org/docs/using_the_compiler/)文档.

注意: 实际的二进制文件是构建在`.build/crystal`, 但`bin/crystal`是你来运行crystal的包装脚本.
