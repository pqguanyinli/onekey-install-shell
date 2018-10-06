### FRP内网穿透一键安装及扩展运用，轻松实现外网访问群晖NAS。

一、注意事项

使用国内服务器搭建，需要域名备案才能使用。

推荐使用：谷歌云、vultr、搬瓦工。

其次推荐：阿里云、腾讯云。

FRP github版本地址：https://github.com/fatedier/frp/releases

可使用的Linux版本：建议Debian7或者Debian8/64bit.

二、一键安装FRP服务端

```
wget --no-check-certificate https://raw.githubusercontent.com/clangcn/onekey-install-shell/master/frps/install-frps.sh -O ./install-frps.sh

chmod 700 ./install-frps.sh

./install-frps.sh install

```

安装步骤说明：
```
Loading network version for frps, please wait...
frps Latest release file frp_0.8.1_linux_amd64.tar.gz    #此步骤会自动获取frp最新版本，自动操作，无需理会
Loading You Server IP, please wait...
You Server IP:12.12.12.12                                           #自动获取你服务器的IP地址
Please input your server setting:

Please input frps bind_port [1-65535](Default Server Port: 5443):      #输入frp提供服务的端口，用于服务器端和客户端通信
Please input frps dashboard_port [1-65535](Default dashboard_port: 6443): #输入frp的控制台服务端口，用于查看frp工作状态
Please input frps vhost_http_port [1-65535](Default vhost_http_port: 80):  #输入frp进行http穿透的http服务端口
Please input frps vhost_https_port [1-65535](Default vhost_https_port: 443): #输入frp进行https穿透的https服务端口
Please input privilege_token (Default: WEWLRgwRjIJVPx2kuqzkGnvuftPLQniq): #输入frp服务器和客户端通信的密码，默认是随机生成的
Please input frps max_pool_count [1-200](Default max_pool_count: 50):     #设置每个代理可以创建的连接池上限，默认50

##### Please select log_level #####
1: info
2: warn
3: error
4: debug
#####################################################
Enter your choice (1, 2, 3, 4 or exit. default [1]):        #设置日志等级，4个选项，默认是info


Please input frps log_max_days [1-30]
(Default log_max_days: 3 day):            #设置日志保留天数，范围是1到30天，默认保留3天。

##### Please select log_file #####
1: enable
2: disable
#####################################################
Enter your choice (1, 2 or exit. default [1]):      #设置是否开启日志记录，默认开启，开启后日志等级及保留天数生效，否则等级和保留天数无效

设置完成后检查你的输入，如果没有问题按任意键继续安装
============== Check your input ==============
You Server IP   : 12.12.12.12
Bind port       : 5443
Dashboard port  : 6443
vhost http port : 80
vhost https port: 443
Privilege token : WEWLRgwRjIJVPx2kuqzkGnvuftPLQniq
Max Pool count  : 50
Log level       : info
Log max days    : 3
Log file        : enable
==============================================

安装结束后显示：
Congratulations, frps install completed!
==============================================
You Server IP   : 12.12.12.12
Bind port       : 5443
Dashboard port  : 6443
vhost http port : 80
vhost https port: 443
Privilege token : WEWLRgwRjIJVPx2kuqzkGnvuftPLQniq
Max Pool count  : 50
Log level       : info
Log max days    : 3
Log file        : enable           #  将上面信息添加到你的路由器frp穿透插件中吧
==============================================
frps Dashboard: http://12.12.12.12:6443/   #  这个是frp控制台访问地址
==============================================
```

三、更新命令
```
./install-frps.sh update
```
四、卸载命令
```
./install-frps.sh uninstall
```
五、服务器端管理命令

服务端程序提供了以下几组功能：

运行程序： ```/etc/init.d/frps start ``` 

停止程序： ```/etc/init.d/frps stop```

重启程序： ```/etc/init.d/frps restart```

运行状态：``` /etc/init.d/frps status```

配置程序： ```/etc/init.d/frps config```

程序版本：``` /etc/init.d/frps version```

### 群晖安装FRPC教程：方法一
1.开启群晖SSH功能后运行以下面令。

```sudo -i```         #获取最高权限
```cd / ```             #到默认目录
```mkdir frp```         #建立文件夹frp
```cd frp```            #进入frp文件夹
```wget https://github.com/fatedier/frp/releases/download/v0.20.0/frp_0.20.0_linux_amd64.tar.gz```    #下载frp
```tar -zxvf frp_0.20.0_linux_amd64.tar.gz```   #解压frp文件
```cd frp_0.20.0_linux_amd64``` #进入frp文件夹
```vi frpc.ini``` #修改frpc文件
```:wq``` #保存信息

frpc文件说明 

./frpc -c ./frpc.ini #临时启动启动frpc服务端

nohup ./frpc -c ./frpc.ini & #后台保持启动

2.设置计划任务开启开机自动启动frpc
```
/frp/frp_0.20.0_linux_amd64/frpc -c /frp/frp_0.20.0_linux_amd64/frpc.ini
```

### 群晖安装FRPC教程：方法二

1.下载群晖玩家自制的FRPC套件。

2.下载地址：https://u16883951.pipipan.com/dir/16883951-27851564-b29cac/

 https://www.synology.com/zh-cn/knowledgebase/DSM/tutorial/General/What_kind_of_CPU_does_my_NAS_have 套件架构查询地址
  
3.选择FRPC最新版本下载。

4.选择你群晖机型的apk下载安装。

5.安装设置frpc.ini 后启动套件即可。

### 群晖安装FRPC教程：方法三

1.LEDE软路由安装frpc客服端

2.设置运行即可

/sbin/iptables -I INPUT -p tcp --dport 7000 -j ACCEPT 
#如需开放端口 请按照实际使用情况 依次开放 此处仅以7000端口为例。

