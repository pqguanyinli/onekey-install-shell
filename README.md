## FRP服务端一键安装及扩展运用

使用国内服务器搭建，需要域名备案才能使用。推荐使用：谷歌云、vultr、搬瓦工，其次推荐：阿里云、腾讯云。

FRP github版本地址：https://github.com/fatedier/frp/releases

可使用的Linux版本：建议Debian7或者Debian8/64bit.

### Install
```
wget --no-check-certificate https://raw.githubusercontent.com/pqguanyinli/onekey-install-shell/master/frps/install-frps.sh -O ./install-frps.sh
chmod 700 ./install-frps.sh
./install-frps.sh install
```
### Uninstall
```
./install-frps.sh uninstall
```

### Update
```
./install-frps.sh update
```

### 服务器端管理命令

运行程序： ```/etc/init.d/frps start ``` 

停止程序： ```/etc/init.d/frps stop```

重启程序： ```/etc/init.d/frps restart```

运行状态：``` /etc/init.d/frps status```

配置程序： ```/etc/init.d/frps config```

程序版本：``` /etc/init.d/frps version```

## 扩展：群晖安装FRPC教程：方法一

### 1.开启群晖SSH功能后运行以下面令。

```sudo -i```         #获取最高权限

```cd / ```             #到默认目录

```mkdir frp```         #建立文件夹frp

```cd frp```            #进入frp文件夹

```wget https://github.com/fatedier/frp/releases/download/v0.21.0/frp_0.21.0_linux_amd64.tar.gz```    #下载frp

```tar -zxvf frp_0.21.0_linux_amd64.tar.gz```   #解压frp文件

```cd frp_0.21.0_linux_amd64``` #进入frp文件夹

```vi frpc.ini``` #修改frpc文件

```:wq``` #保存信息

frpc文件说明 

```./frpc -c ./frpc.ini``` #临时启动启动frpc服务端

```nohup ./frpc -c ./frpc.ini &``` #后台保持启动

### 2.设置计划任务开启开机自动启动frpc
```
/frp/frp_0.21.0_linux_amd64/frpc -c /frp/frp_0.21.0_linux_amd64/frpc.ini
```

## 扩展：群晖安装FRPC教程：方法二

下载群晖玩家自制的FRPC套件。

> 1.套件架构查询，确定群晖架构。
>
> 查询地址：
> https://www.synology.com/zh-cn/knowledgebase/DSM/tutorial/General/What_kind_of_CPU_does_my_NAS_have 
>  
> 2.选择你群晖机型的apk下载安装。
>
> 下载地址：https://u16883951.pipipan.com/dir/16883951-27851564-b29cac/
>
> 3.安装设置frpc.ini 后启动套件即可。

## 扩展：群晖安装FRPC教程：方法三

> 1.LEDE软路由安装frpc客服端
>
> 2.设置运行即可

/sbin/iptables -I INPUT -p tcp --dport 7000 -j ACCEPT 
#如需开放端口 请按照实际使用情况 依次开放 此处仅以7000端口为例。

