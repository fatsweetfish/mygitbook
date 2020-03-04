





## Ubuntu 18.04安装Shadowsocks 3.0.0

先要到https://justmysocks2.net/买vpn  fatsweetfish@aliyn.com  vpn180928@#$

不要sudo apt-get install shadowsocks  装出来的版本是2.9不支持aes-256-gcm加密

# 1.安装和配置

## 安装pip

- 执行：
  `sudo apt install python3-pip`

## 安装Shadowsocks

- 执行：
  `pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip`
- 安装完后检查是否为3.0.0版本
  `ssserver --version`
  若显示Shadowsocks 3.0.0则进行下一步

## 配置Shadowsocks

- 创建shadowsocks.json
  `sudo vim /etc/shadowsocks.json`
- 编辑shadowsocks.json内容
  复制粘贴一下内容并适当修改：

复制

```
{
    "server":"服务器ip",
    "server_port":6666,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"连接密码",
    "timeout":300,
    "method":"aes-256-cfb"
}
```

我的版本

```
{
    "server":"c36s1.jamjams.net",
    "server_port":15587,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"otDbmaceyF",
    "timeout":300,
    "method":"aes-256-gcm"
}


```



# 启动shadowsocks

sudo sslocal -c /etc/shadowsocks.json -d start

一定不要用

`ssserver -c /etc/shadowsocks.json -d start`

它会报错





---

---





# shadowsocks 3.0安装问题

https://www.igray.cc/614.html



之前用

pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip

安装在　home/gray/.local/bin/下了

sudo sserver

sudo: ssserver: command not found

再执行sudo pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip报

```
ts@ts-OptiPlex-7070:~/sh$ sudo pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip
The directory '/home/ts/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
The directory '/home/ts/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting https://github.com/shadowsocks/shadowsocks/archive/master.zip
  Downloading https://github.com/shadowsocks/shadowsocks/archive/master.zip (115kB)
    100% |████████████████████████████████| 122kB 434kB/s 
  Requirement already satisfied (use --upgrade to upgrade): shadowsocks==3.0.0 from https://github.com/shadowsocks/shadowsocks/archive/master.zip in /home/ts/.local/lib/python3.6/site-packages
  
```

所以执行

sudo pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip --upgrade

就拿到sudo权限了



# 2.配置pac规则+

#### 1. 安装GenPac

```-
sudo pip3 install genpac
sudo pip3 install --upgrade genpac
```

#### 2. 新建pac配置存放目录

用来存放用户自定义规则列表文件user-rules.txt和生成后的autoproxy.pac文件，例如我的放在home目录下

```
mkdir -p ~/config/pac 
cd ~/config/pac
touch user-rules.txt
```



#### 3. 生成autoproxy.pac文件

我使用的是github上托管的这份文件：https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
执行一下命令来创建autoprox.pac

```
genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --output="autoproxy.pac" --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt" --user-rule-from="user-rules.txt"
```



#### 4. 配置系统代理

去Ubuntu`设置 -> 网络 -> 代理设置`设置代理，选择`自动`，配置url填写你本地的文件路径，例如：`file:///home/ts/config/pac/autoproxy.pac`





## 遇到的问题

#### a.chrome不能上，firewfox能上

https://blog.csdn.net/Enterprise_/article/details/90745045

先用这个命令

google-chrome-stable --proxy-server="socks5://127.0.0.1:1080" 

这样可以上google







**b.chrome重启插件，配置都消失，每次开机会报**

```
Some features may be unavailable and changes to preferences won't be saved.
```



解决办法：

```
cd ~ 
cd .config/google-chrome 
sudo chown ts:ts 'Local State' 

cd Default
sudo chown ts:ts Preferences
sudo chown ts:ts 'Network Persistent State'
```





**c.安装扩展 proxy switchyomega**

先google-chrome-stable --proxy-server="socks5://127.0.0.1:1080"可以连google后到chrome 应用商店下

proxy switchomega插件

开启快捷键alt+shift+o



如果只配chrome可以上vpn:

要先在chrome配proxy

点switchomega那个圈圈->Options->proxy->

![img](pic/proxy.png)

再apply changes



再配一个profile

点Newprofie->

Profiename: ss ->

再选PAC Profile

PAC URL file:///home/ts/config/pac/autoproxy.pac   ->

->apply changes





**<font  color=red>这样以后在终端还是不能下载代码，所以还要配</font>**



# Ubuntu18.04中安装shadowsocks和privoxy全局代理

https://ywnz.com/linuxjc/2687.html





#### 如果终端执行操作要vpn只能配系统的

**１.系统设置**

系统设置->Network->Nexwork Proxy->Autamic->Configuration URL file:///home/ts/config/pac/autoproxy.pac



**2.安装privoxy**

sudo apt install privoxy 

sudo vim /etc/privoxy/config



确定

listen-address 127.0.0.1:8118　是打开的

\#forward-socks5t / 127.0.0.1:9050下增加

forward-socks5t / 127.0.0.1:1080

vim ~/.bashrc

最后增加

export http_proxy="127.0.0.1:8118"	

export https_proxy="127.0.0.1:8118"

export ftp_proxy="127.0.0.1:8118"

再source  ~/.bashrc

然后测试 curl www.google.com有返回则说明成功了



```shell
sudo /etc/init.d/privoxy start或者restar或stop
```



**3.为 Git 配置代理**

​	最后，我还要配置一项：为 git 配置代理，否则 google / android 源码是同步不下来的，可以找份代码先验证一下：

​	$ git clone https://chromium.googlesource.com/external/webrtc

​	会报错：

​	正克隆到 'webrtc'… 

​	fatal: unable to access 'https://chromium.googlesource.com/external/webrtc/': 

​	Failed to connect to chromium.googlesource.com port 443: 连接超时

​	所以需先为 git 配置代理：

​	$ git config --global http.proxy 'socks5://127.0.0.1:1080' 

​	$ git config --global https.proxy 'socks5://127.0.0.1:1080'

​	配置好就能 正常clone了：

​	![Ubuntu18.04中安装shadowsocks和privoxy全局代理](pic/1-1PQG10R9516.JPG)

​	如果要关闭代理可使用一下命令：

​	$ git config --global --unset http.proxy

​	$ git config --global --unset https.proxy



------------------------

**END**









以下操作不要

**2.安装proxychains**

下安装proxychains

一、编译安装

1.下载源码包

    git clone https://github.com/rofl0r/proxychains-ng.git

2.进入安装目录

    cd proxychains-ng/

3.编译安装

    ./configure --prefix=/usr --sysconfdir=/etc
    make 
    sudo make install
    sudo make install-config  # 创建配置文件 (不用sudo来安装会报权限错误)

4.配置代理

    sudo vim /etc/proxychains.conf
    将配置文件最后一行修改成 socks5  127.0.0.1 1080

5,测试（要先启动shadowsocks客户端）

    proxychains4 curl http://www.google.com
    proxychains4 wget  http://www.google.com

二、apt安装

1.安装，注意apt源安装的是第3版的proxychains

    apt-get install proxychains

命令提示会同时安装libproxychains3 proxychains
2.卸载

apt-get purge libproxychains3
apt-get purge proxychains



-----会报错

————————————————
版权声明：本文为CSDN博主「只爱写代码」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Lazybones_3/article/details/85129470



## 增加新的网址

经常会遇到有人想要添加和编辑 PAC中的网址规则，但是不知道该怎么添加。

有时候访问一些网站，可能被墙或者打开很慢，于是想要让这个网站走Shadowsocks代理，但是又不想开全局模式，那么你就需要看下面这个文章了。

其实那，PAC文件就是JavaScript语法，里面有个rules的变量，储存着json格式的数组内容。

------

在ShadowsocksR中除了pac.txt文件以外，还会有一个 user-rule.txt 的文件**（如果没有就新建一个）**，是单独给用户来添加网址规则的。所以我们只需要编辑这个文件就行了，毕竟pac.txt里面的内容太多，太乱。

> 注意，因为修改 user-rule.txt 文件后，需要点击选项 更新PAC为 GFWList 才能生效，而因为SSR项目终止，导致此功能不可用，所以下面修改 user-rule.txt 文件的方法已失效，当然可以打开 pac.txt 文件直接修改（按格式），语法规则一样。

## 编辑 user-rule.txt 文件

首先我们打开和Shadowsocks.exe同文件夹中的 **user-rule.txt** 文件，当然你也可以通过 **右键Shadowsocks托盘图标 >-> PAC >-> 编辑 GFWList 的用户规则** 来打开这个文件。

具体的语法我也不是特别懂，所以下面的教程只适合简单的添加和编辑。

------

比如你想要 ipip.net 这个网站走Shadowsocks代理，那么你就需要添加一个 ipip.net 的网址规则。

**例如：**

```
||ipip.net^
```

这个规则的意思是，任何以` ipip.net `为主的所有子域名包括自身，同时还有所有的互联网协议(http:// https:// ftp://)，都走Shadowsocks代理。





我的实践：

vim home/ts/config/pac/user-rule.txt

增加

```
||grc.io^
```



再genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --output="autoproxy.pac" --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt" --user-rule-from="user-rules.txt"

或再执行同目录下脚本：gen_autopac.sh 

生成新的autoproxy.pac







