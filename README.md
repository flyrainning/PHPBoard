# PHPBoard
ARM 开发板基础框架，支持采用php控制硬件设备，如GPIO，可通过模块支持各种探测器，并可采用php编写业务罗辑，支持本地和web同时访问。

>**注意** 本框架处在测试阶段，部分功能可能无法很好的工作

# 安装

1、根据开发板类型，自行在开发板上配置php+web运行环境，推荐使用nginx+php组合。php需要cli支持。
以Cubieboard 2，Debian系统为例。
```bash
#更新系统
apt-get update
apt-get upgrade

#安装nginx
apt-get install nginx

#安装php
apt-get install php5 php5-fpm php5-cli php5-json

#若项目中需要用到其他组件，可一并安装，如数据库，gd图形库
apt-get install php5-sqlite php5-mysql  php5-gd

```

2、下载phpboard
>config_sample文件夹存放系统配置文件示例，可供配置环境时参考。
>phpboard文件夹为框架主文件，将整个文件夹复制到系统根目录 / 下。

3、安装phpboard
>配置您的web服务根目录指向/phpboard/wwwroot/，如果使用nginx，可直接使用config_sample中的站点配置文件。
>将/phpboard/init 加入开机自动启动，如在 /etc/rc.local 文件中加入
```bash
/phpboard/init &
```
>将/phpboard/phphost/phphost文件在/bin中建立一个连接，方便直接调用phphost命令
```bash
ln /phpboard/phphost/phphost /bin
```
**注意** 请检查/phpboard/init 和/phpboard/phphost/phphost的权限是否为可执行，若不是请使用chmod设置为可执行。

4、配置phpboard
>phpboard的配置采用标准json格式。
>在/phpboard/config/phphost.conf 配置开机需要启动的脚本
>在/phpboard/phphost/config文件夹中配置设备和模块，如GPIO。根据需要用到的模块分别配置。

5、编写业务逻辑
>操作界面部分可按照普通网站进行开发，放入/phpboard/wwwroot中
>硬件控制部分编写控制脚本，放入/phpboard/phphost/script目录中，通过phphost调用。
>界面部分与控制部分通讯可选择框架提供的通讯模块，也可直接采用共享内存，临时文件等方式实现交互与控制。

**详细使用方法请参考wiki**
