# 安装

首先要配置好安装环境。

安装后，Microweber将在其基本文件夹中创建或修改.htaccess文件。它还将为拒绝访问代码的每个脚本目录创建几个这样的文件。

## 下载 via composer

```
composer create-project microweber/microweber my_site dev-master
```

## 手动下载

下载最新的版本： https://microweber.com/download.php


## 安装过程

在浏览器打开你的网站。你应该可以看到下面的


Microweber需要一个数据库来存储网站内容。数据库引擎有： mysql,sqlite , pgslq

在安装期间，你必须配置数据连接并创建一个管理账户。这将是你管理网站的唯一方法。填写的字段包括以下：

database hostname: 数据库地址
database username: 数据库用户名
database password:  数据库密码
database name:  数据库名
table prefix: 数据库表前缀，如果提供的数据库不是专门用于一个Microweber安装，您应该设置一个前缀来区分您的网站的数据与其他数据
admin username: 选择您的用户名来管理您的网站。我们建议您使用您的真实姓名或一些比默认的“admin”更难猜的东西。
admin E-mail:请使用有效的电子邮件。您可能需要它的密码恢复或网站通知。
admin password: 请设置一个尽可能长且难以猜出的密码。也让它容易记住。

点击`Install`按钮，一旦安装完成，该页面将提供你查看新创建的网站或直接进入管理面板。


## 选择安装方法

还有其他可用于自动安装的方法

地址： http://docs.microweber.com/guides/installation_cli.md


## 可写文件夹

以下文件夹可写：
* config
* storage
* userfiles

*安装完成后*
当你完成安装时，Microweber将在`config/Microweber.php`创建一个文件，你将看到一个选项`'installed'=> true`，如果需要新的安装，必须将该项设置为false。


## 配置

Microweber应用程序使用laravel配置类来夹中系统变量，比如数据凭据和内部设置。

*开启调试模式*
在`config/app.php`中`'debug'=> true`来设置。

*数据库配置文件*
在`config/database.php` 
示例可看：https://github.com/microweber/microweber/blob/master/config/database.php

*多站点设置*
你可以使用一个Microweber实例，通过单独安装来管理多个域。

为了在同一个安装上有两个站点，你需要为dns设置一条记录，以指向与Microweber安装相同的IP。
要进行安装，只需在`config`创建一个文件夹。然后在`config/second-domain.com/microweber.php`创建一个空文件。

注意请不要使用`www`作为文件夹名称。

之后，当你访问`second-domain.com`时，将看到安装屏幕。

















