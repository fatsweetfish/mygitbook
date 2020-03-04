## gitbook

#### 一、安装

1. 全局安装`gitbook-cli`

   `sudo apt-get install npm`

   `sudo npm install gitbook-cli -g`
   
   `gitbook -V`

#### 二、使用

1. 新建mygitbook文件夹　

   `mkdir mygitbook`

2. 初始化:

   `cd mygitbook `

   `gitbook init`

生成

README.md —— 书籍的介绍写在这个文件里

 SUMMARY.md —— 书籍的目录结构在这里配置

接下来，我们输入 `$ gitbook serve` 命令，然后在浏览器地址栏中输入 `http://localhost:4000` 便可预览书籍。



运行该命令后会在书籍的文件夹中生成一个 `_book` 文件夹, 里面的内容即为生成的 html 文件，我们可以使用下面命令来生成网页而不开启服务器。

```undefined
gitbook build
```





在SUMMARY.md编写架构后

执行gitbook init会生成相应的文件



build 命令可以指定路径：

    gitbook build [书籍路径] [输出路径]

serve 命令也可以指定端口：

    gitbook serve --port 2333

你还可以生成 PDF 格式的电子书：

    gitbook pdf ./ ./mybook.pdf

生成 epub 格式的电子书：

    gitbook epub ./ ./mybook.epub

生成 mobi 格式的电子书：

    gitbook mobi ./ ./mybook.mobi

如果生成不了，你可能还需要安装一些工具，比如 ebook-convert。或者在 Typora 中安装 Pandoc 进行导出。

除此之外，别忘了还可以用 Git 做版本管理呀！在 mybook 目录下执行 git init 初始化仓库，执行 git remote add 添加远程仓库（你得先在远端建好）。接着就可以愉快地 commit，push，pull … 啦！


ref:https://www.jianshu.com/p/421cc442f06c

https://blog.csdn.net/lu_embedded/article/details/81100704



https://segmentfault.com/a/1190000017960359?utm_source=tag-newest

