# 在macOS用Homebrew

在Mac你可以很简单的用[Homebrew](http://brew.sh/)来安装.

```
brew update
brew install crystal
```

## 问题排除 on OSX 10.11 (El Capitan)

如果你得到类似错误:

```
ld: library not found for -levent
```

你需要重新安装命令行工具然后选择默认的工具链:

```
$ xcode-select --install
$ xcode-select --switch /Library/Developer/CommandLineTools
```
