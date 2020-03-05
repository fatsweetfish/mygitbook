### ChkBugreport安装使用

ChkBugReport软件是索尼（Sony）公司开发的，开源在 Github 上，是用来分析bugreport的。

我已经编译好ChkBugReport.jar放在Tools下，若直接用，跳过步骤1和２，从３开始

#### 1.安装

```
$ git clone https://github.com/sonyxperiadev/ChkBugReport
```

#### 2.编译

用Android  Studio导入后编译

File->New->Import Project先中ChkBugReport/core下的build.gradle或者settings.gradle

Build->Make Project然后就开始build了

编好会在ChkBugReport/core/build/libs生成ChkBugReport.jar

#### 3.简化命令

然后在~/bin下（~/bin已经加入PATH）

```
vim chkbugreport
```

写入

```
#!/bin/sh

DIR=/home/ts/workspace/performance/ChkBugReport/core/build/libs
CBR=$DIR/ChkBugReport.jar


if [ ! -f $JAR]; then
    echo "can not find ChkBugReport.jar in $DIR"
    exit 1
fi

java -jar $CBR "$@"
```

这样下次要用这个工具就可以从java -jar XXX_PATH/ChkBugReport.jar简化成chkbugreport

#### 4.使用

```
$ adb bugreport  bugreport.zip
$ unzip bugreport.zip -d bug
$ cd bug
$ chkbugreport bugreport-xxx-verion-2020-02-25-11-20-29.txt
```

生成报告在bugreport-xxx-version-2020-02-25-11-20-29_out/index.html，可以直接打开看



#### Ref:

 https://www.jianshu.com/p/002de25a176b

##### ChkBugReport使用指南

http://www.voidcn.com/article/p-ngdhydls-bez.html

##### 调试系列2：bugreport实战篇

https://www.jianshu.com/p/1ada78f09336