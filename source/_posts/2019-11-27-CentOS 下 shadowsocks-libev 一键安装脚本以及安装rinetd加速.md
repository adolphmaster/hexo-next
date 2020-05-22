---
title: CentOS 下 shadowsocks-libev 一键安装脚本以及安装rinetd加速
comments: true
share: true
toc: true
categories:
  - vpn
tags:
  - [shadowsocks]
  - [rinetd]
date: 2019-11-27 09:55:47
---



### CentOS 下 shadowsocks-libev 一键安装脚本以及安装rinetd加速

> 原文https://github.com/Puuoi/ss-libev-for-CentoOS



原文链接：https://teddysun.com/357.html

本脚本适用环境：
系统支持：CentOS
内存要求：≥128M
日期：2018 年 06 月 01 日

#### 关于本脚本：
一键安装 libev 版的 Shadowsocks 最新版本。该版本的特点是内存占用小（600k 左右），低 CPU 消耗，甚至可以安装在基于 OpenWRT 的路由器上。

Shadowsocks for Windows 客户端下载：
https://github.com/shadowsocks/shadowsocks-windows/releases

默认配置：
服务器端口：自己设定（如不设定，默认从 9000-19999 之间随机生成）
密码：自己设定（如不设定，默认为 teddysun.com）
加密方式：自己设定（如不设定，默认为 aes-256-gcm）

#### 使用方法：

使用 root 用户登录，运行以下命令：

```shell
wget --no-check-certificate -O shadowsocks-libev.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh 
chmod +x shadowsocks-libev.sh
./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log
```

安装完成后，脚本提示如下：

```shell
Congratulations, Shadowsocks-libev server install completed!
Your Server IP        :your_server_ip 
Your Server Port      :your_server_port 
Your Password         :your_password
Your Encryption Method:your_encryption_method

Welcome to visit:https://teddysun.com/357.html
Enjoy it!
```

#### 卸载方法：
使用 root 用户登录，运行以下命令：

```shell
./shadowsocks-libev.sh uninstall</br>
```

安装完成后即已后台启动 Shadowsocks-libev ，运行：

```shell
/etc/init.d/shadowsocks status
```


可以查看进程是否启动。
本脚本安装完成后，会将 Shadowsocks-libev 加入开机自启动。

#### 使用命令：
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
查看状态：/etc/init.d/shadowsocks status

特别说明：
1、已安装旧版本的 shadowsocks 需要升级的话，需下载本脚本的最新版，直接运行即可自动升级

```shell
./shadowsocks-libev.sh
```

参考链接：
https://github.com/shadowsocks/shadowsocks-libev

### rinetd

1、下载rintd二进制文件(原版bbr和修改版bbr二选一即可):

```shell
wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd
wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd_bbr_powered -O /root/rinetd
```

2、修改权限:

```shell
chmod +x rinetd
```

3、修改rinetd的配置文件rinetd.conf,添加监听地址:

```shell
 vi rinetd.conf
# bindadress bindport connectaddress connectport
0.0.0.0 443 0.0.0.0 443
0.0.0.0 80 0.0.0.0 80
0.0.0.0 52800 0.0.0.0 52800
```

4、设置开机启动

```shell
vi /etc/systemd/system/rinetd.service
[Unit]
Description=rinetd
[Service]
ExecStart=/root/rinetd -f -c /root/rinetd.conf raw venet0:0
Restart=always 
[Install]
WantedBy=multi-user.target
```

5、最后执行:

```shell
systemctl enable rinetd.service && systemctl start rinetd.service

后面可以执行
systemctl start rinetd.service
```