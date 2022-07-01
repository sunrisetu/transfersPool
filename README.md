# 矿池中转 ！！
矿池中转，解决矿池连接不上的问题。
中转矿池的方式主要有两种：自搭中转服务器、使用中转平台。自搭中转服务器需要购买海外服务器，也需要些许的计算机操作基础。因此，建议小白用户直接使用现成的中转平台，简单修改挖矿地址即可。

## 1.使用中转平台
中转平台在矿机和海外矿池之间搭建了双向的连接桥梁。矿工可以像直接连接矿池一样使用中转平台提供的地址。优秀的中转平台应该做到延迟低（减少无效哈希计算）、抽水少、长期稳定。

这里推荐使用  中转平台 (Telegram **中转交流圈** [t.me](https://t.me/+uoSRngB_OAY5NjE1))：
* 支持几乎全部ETH海外矿池
* 超低延迟（10ms-30ms）
* 低至0.3%的抽水（平稳无暗抽+[抽水信息公开透明]）
* 全面支持安全防探测的SSL链接（需设置挖矿程序使用stratum+ssl协议）

### 中转服务节点  
不想或不会自建服务器，可直接使用下面的地址  
有问题可联系微信号sx_sunrise  
## fo2pool 官网：http://fo2pool.com 
|    矿池/币种  |   ETH（TCP协议）      |   ETH（SSL加密）      |
| ---- | ---- | ---- |
|   鱼池（f2pool.com）   |   f2pool.fo2pool.com:6688      |   f2pool.fo2pool.com:6699      |
|   e池（ethermine.org）   |   ethermine.fo2pool.com:2144      |   ethermine.fo2pool.com:4471      |
|   币印（poolin.me）   |   poolin.fo2pool.com:1883      |   poolin.fo2pool.com:1884      |
|   hive OS（hiveon.net）   |   hiveon.fo2pool.com:24442      |   hiveon.fo2pool.com:24443     |
|   凤池（flexpool.io）   |   flexpool.fo2pool.com:3344      |   flexpool.fo2pool.com:4455      |
|   蚂蚁（antpool.com）   |   antpool.fo2pool.com:8008     |   antpool.fo2pool.com:8009      |



## 2. 安全的矿场中转服务

除了面向矿工，还提供最安全的矿场中转方案，流量加密、混淆、伪装，且可防止挖矿软件Dev乱连。
欢迎加入Telegram **中转交流圈** [t.me（https://t.me/+uoSRngB_OAY5NjE1）](https://t.me/+uoSRngB_OAY5NjE1) 或者添加微信号进群 sx_sunrise  


## 3. 自搭中转服务器
自搭中转服务器需要自行购买海外服务器，并设置网络端口转发。

### 3.1 购买海外服务器
购买海外服务器首选地是**香港**（延迟20ms-60ms），次选日本、新加坡（延迟50ms-100ms）。综合价格、延迟、稳定性、支付便利性（支持支付宝或微信支付），推荐购买腾讯云、阿里云、LayerStack
| 厂商 | 购买链接 | 价格 | 优缺点 |
| :----: | :----: | :----: | :---- |
| 腾讯云 | https://curl.qcloud.com/ZSLvjpe9  | 最低配香港CVM服务器约400元/年 | CN GIA2直连延迟低约30ms，支持微信支付，有新人优惠（腾讯云老用户只能注册新账户才能享受了，用邮箱，手机号等都可以重新注册和实名认证，一个人可以最多注册5个新账户） | 
| 阿里云 | https://www.aliyun.com/daily-act/ecs/activity_selection?source=5176.11533457&userCode=w8nqlq0k | 最低配香港直连服务器约1200元/年 | CN GIA2直连延迟低约30ms，支持支付宝支付 |

### 3.2 Windows网络转发设置

（1）登录到服务器后，打开windows PowerShell命令行

（2）输入代码：
netsh interface portproxy add v4tov4 listenport=14444 connectaddress=asia2.ethermine.org connectport=14444

（3）不报错就是成功了！
如果不放心，可以输入下面的代码查看状态： netsh interface  portproxy show  v4tov4

（4）通过windows服务器的IP地址和端口14444进行ethermine挖矿


### 3.3 Ubuntu/Debian网络转发设置

 #### 方法一 redir
（1）首先得租用一个海外VPS（见上述方法）
    
（2）用root用户登录服务器  

（3）首先安装redir  
```bash
sudo apt-get install redir
```
  
（4）查看redir版本，显示版本号则表示成功，我的是3.1  
```bash
redir -version
#3.1
```
  
（5）矿池中转，格式   
```bash
redir :14444 asia2.ethermine.org:14444

#:14444 是本地端口  asia2.ethermine.org是矿池地址 :14444是矿池端口  
```



查看中转状态，应该能看到以下的行，如果没出现，需要开启端口  
```bash
netstat -anpt

#tcp        0      0 0.0.0.0:14444             0.0.0.0:*               LISTEN      31316/redir  
```


（6）设置挖矿软件，把挖矿地址改成搭建的服务器ip:端口的格式，比如  
xx.xx.xx.xx:14444  
  
启动挖矿，此时应该已经可以挖矿了  
  
（7）防止redir被误关，设置定时开启  
```bash
vim root.cron
```
  
（8）在打开的页面里输入以下内容，其中端口和矿池地址根据需要填写，然后保存，以下内容表示，每天0点杀死redir，并在每小时的第二分钟重启redir  
 
 ```bash
1 0 * * * /bin/ps aux|grep redir|grep -v grep|cut -c 9-15|xargs kill -15  
2 * * * * /usr/bin/redir :14444 asia2.ethermine.org:14444
```


  
(9)启动cronrtab，查看crontab，若输出以下内容，就说明设置成功  
```bash
crontab root.cron
crontab -l

#1 0 * * * /bin/ps aux|grep redir|grep -v grep|cut -c 9-15|xargs kill -15  
#2 * * * * /usr/bin/redir :14444 asia2.ethermine.org:14444
```

 
 #### 方法二 rinetd
 
 （1）下载安装rinetd
 
 ```bash
apt update
apt install rinetd
```
（2）配置重定向文件

 ```bash
vim /etc/rinetd.conf

#输入一下内容，#:14444 是本地端口  asia2.ethermine.org是矿池地址 :14444是矿池端口 
0.0.0.0 14444 asia2.ethermine.org:14444
allow *.*.*.*
logfile /var/log/rinetd.log
```

（3）运行重定向程序

 ```bash
rinetd -c /etc/rinetd.conf
```

（4）设置挖矿软件，把挖矿地址改成搭建的服务器ip:端口的格式，比如 

xx.xx.xx.xx:14444 
  
启动挖矿，此时应该已经可以挖矿了 
