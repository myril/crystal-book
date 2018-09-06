# RedHat和CentOS

在RedHat衍生版中, 你可以用Crystal官方资源库.

## 配置资源库

首先你需要添加资源库到你的YUM配置中. 为了便于设置, 你只需要在命令行中运行下面命令即可:

```
curl https://dist.crystal-lang.org/rpm/setup.sh | sudo bash
```

它将自动添加签名秘钥和资源配置. 如果你期望手动操作, 请执行如下的命令:

```
rpm --import https://dist.crystal-lang.org/rpm/RPM-GPG-KEY

cat > /etc/yum.repos.d/crystal.repo <<END
[crystal]
name = Crystal
baseurl = https://dist.crystal-lang.org/rpm/
END
```

## 安装
资源库配置完成后, 你就可以准备安装Crystal了:

```
sudo yum install crystal
```

## 升级

当Crystal新版本发布后, 你可以在你的系统中用以下命令来升级:

```
sudo yum update crystal
```
