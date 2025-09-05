# 关于Alpine

Alpine Linux是一个社区开发的面向安全应用的轻量级Linux发行版操作系统，占用资源很少，初始状态基本只占用几M内存和几十兆硬盘，而且还很稳定，适合很多小型服务器和设备使用。


# ovz一键安装Alpine

通过脚本将VPS上现有的Linux系统一键转换为Alpine Linux。需要注意的是，脚本~~只支持openvz6构架~~的vps，并且VPS上原有数据会全部丢失，安装成功后ssh端口号会变为22，密码不变。（20201229，更新对openvz7的支持。）

```shell
wget --no-check-certificate -O alpine-install.sh https://file.207614.xyz/chfs/shared/script/alpine-install.sh && bash alpine-install.sh
```


# 更新系统

一键安装脚本安装的Alpine版本是3.9版,下面的脚本，可以一键更新alpine到最新版本，并更新时区为上海。满足折腾怪们的癖好。

```shell
apk add ca-certificates&& update-ca-certificates && apk --no-cache add openssl wget && wget --no-check-certificate -O alpine-update.sh https://file.207614.xyz/chfs/shared/script/alpine-update.sh && chmod 755 alpine-update.sh &&./alpine-update.sh
```

更新完成后，会重启，重新连上SSH后，可以通过以下命令查看系统版本。

```shell
cat /etc/alpine-release.apk-new
或者
cat /etc/issue
```


# Alpine使用手册

## Alpine常用命令

```shell
apk update //更新最新镜像源列表
apk search //查找所以可用软件包
apk search -v //查找所以可用软件包及其描述内容
apk search -v 'acf*' //通过软件包名称查找软件包
apk search -v -d 'docker' //通过描述文件查找特定的软件包
apk add openssh //安装一个软件
apk add openssh openntp vim //安装多个软件
apk add --no-cache mysql-client //不使用本地镜像源缓存，相当于先执行update，再执行add
apk info //列出所有已安装的软件包
apk info -a zlib //显示完整的软件包信息
apk info --who-owns /sbin/lbu //显示指定文件属于的包
apk upgrade //升级所有软件
apk upgrade openssh //升级指定软件
apk upgrade openssh openntp vim //升级多个软件
apk add --upgrade busybox //指定升级部分软件包
apk del openssh //删除一个软件
```

## Alpine服务管理

```shell
alpine没有使用fedora的systemctl来进行服务管理，使用的是RC系列命令：
rc-update     //主要用于不同运行级增加或者删除服务
rc-status       //主要用于运行级的状态管理
rc-service     //主用于管理服务的状态
rc-status -a  //列出系统所有服务
```




<!-- ##{"timestamp":1607500014}## -->