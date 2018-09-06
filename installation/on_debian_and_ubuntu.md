# Debian和Ubuntu

在Debian的衍生版中, 你可以用官方的Crystal资源库.

## 配置资源库

首先你需要添加资源库到你的APT配置中. 为了便于设置, 你只需要在命令行中运行下面命令即可:

```bash
curl -sSL https://dist.crystal-lang.org/apt/setup.sh | sudo bash
```

它将自动添加签名秘钥和资源配置. 如果你期望手动操作, 请执行如下的命令:

```bash
curl -sL "https://keybase.io/crystal/pgp_keys.asc" | sudo apt-key add -
echo "deb https://dist.crystal-lang.org/apt crystal main" | sudo tee /etc/apt/sources.list.d/crystal.list
sudo apt-get update
```

## 安装
资源库配置完成后, 你就可以准备安装Crystal了:

```bash
sudo apt install crystal
```

以下软件包不是必须的, 但推荐在标准库中使用响应功能:

```bash
sudo apt install libssl-dev      # for using OpenSSL
sudo apt install libxml2-dev     # for using XML
sudo apt install libyaml-dev     # for using YAML
sudo apt install libgmp-dev      # for using Big numbers
sudo apt install libreadline-dev # for using Readline
```

要构建Crystal编译器本身, 还需要一些其他依赖项, 详情查看[wiki页](https://github.com/crystal-lang/crystal/wiki/All-required-libraries#ubuntu). 他们对于常规编译器不是必须的.

## 升级

当Crystal新版本发布后, 你可以在你的系统中用以下命令来升级:

```bash
sudo apt update
sudo apt install crystal
```
