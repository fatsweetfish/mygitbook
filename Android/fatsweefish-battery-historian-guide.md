## Our Battery-Ｈistorian User Guide

### 说明

**本项目是frok原google在github上开源项目二次开发的，主要解决了编译问题，google cdn问题和工具自身的一些bug。**

地址: https://github.com/fatsweetfish/battery-historian

本项目有三个分支：

google分支：用来同步原项目最新代码

master分支：开发分支，最新的代码都会最先出现在这里，替换了google cdn为国内可以访问的源

orgcdn分支：与master分支不一样的地方是用原代码的google cdn



推存使用方法：

**master分支+ chrome安装Battery-Historian-ReplaceGoogleCDN扩展程序**，若chrome装的扩展程序，工具的所有功能都能用，若不装扩展程序，某些功能不用，比如Historian不能用，因为要访问的goole api是从jar库中发出的，源码改不了

orgcdn分支 + chrome安装Battery-Historian-ReplaceGoogleCDN扩展程序，chrome必须装扩展程序，不然无法使用工具

目前本项目还有一个比较重要的bug是

Android 9导出的bugreport是有App Selection

Android 10导出的就没有



**1.安装go**

```
sudo add-apt-repository ppa:gophers/go
sudo apt-get update
sudo apt-get install golang

```



**2.配置go环境变量**

vim ~/.bashrc

增加

```
export GOPATH=/home/jane/go
export GOBIN=$GOPATH/bin
export PATH=$GOBIN:$PATH

```

source ~/.bashrc



**3.下载google源码**

```
go get -d -u github.com/google/battery-historian/...
```

生成的代码在$GOPATH/src/github.com/google/battery-historian



**4.更新源码**

方法一：删除原battery-historian，替换成自己的battery-historian

```
cd  ~/go/src/github.com/google
rm -rf  battery-historian
git clone https://github.com/fatsweetfish/battery-historian
```



方法二：合并自己的源码

```
cd  ~/go/src/github.com/google/battery-historian
git remote add new https://github.com/fatsweetfish/battery-historian
git remote -v
git fetch new master   将远程new仓库的master分支缓存到本地为new/master
git merge new/master   将缓存的new/master合并到当前分支 跟(git merge FEATH_HEAD 将最新获取的的内容合并到当前分支)效果一样
```

方法一比较暴力但是简单，下代码还要花费些时间，方法二比较优雅但是复杂一些



**5.编译**

这步有时候很快，有时候很慢

```
go run setup.go
```

如果太慢或者出错，可以手动下载

```
cd third_party
git clone https://github.com/google/closure-compiler
git clone https://github.com/google/closure-library
git clone https://github.com/markrcote/flot-axislabels.git
```

再go run setup.go



**6.运行**

```
go run cmd/battery-historian/battery-historian.go [--port <default:9999>]
```



**7.访问**

在chrome上安装插件后可以访问

`http://localhost:9999 `

获取扩展程序

```
git clone https://github.com/fatsweetfish/Battery-Historian-ReplaceGoogleCDN
看README.md来安装
```

若要别的电脑可以访问，要先把9999端口打开，安装好插件，输入ip:9999可以访问



**8.准备bugreport和batterystats.txt**

```
adb kill-server 
adb start-server
adb devices

adb shell dumpsys batterystats -–enable full-wake-history 
adb shell dumpsys batterystats -–reset
```

开始测试，测试完导出bugreport和batterystats.txt

```
adb bugreport bugreport.zip
adb shell dumpsys batterystats > batterystats.txt
```

bugreport.zip上传分析

工具里的Historian功能，部分被遮档了，我们可以自己生成battery.html用浏览器打开

```
cd ~/go/src/github.com.local/google/battery-historian/scripts
$ ./historian.py -a batterystats.txt  > battery.html
```



ps:其它一些可能用上的设置

```
adb shell dumpsys battery set status 2 //设置电池为充电状态 
adb shell dumpsys battery set status 1 //设置电池为非充电状态 
adb shell dumpsys battery unplug //设置断开充电（Android 6.0以上） 
adb shell dumpsys battery reset //复位，恢复实际状态 
```





