## gitbook

#### 一、安装

1. 全局安装`gitbook-cli`

   `sudo apt-get install npm`

   `sudo npm install gitbook-cli -g`
   
   在家里的ubuntu14.4安装报了错误
   
   **报错1：**
   
   ```
   jane@lemon:~/myspace/mygitbook/MiscRecord$ sudo npm install gitbook-cli -g
   npm http GET https://registry.npmjs.org/gitbook-cli
   npm http GET https://registry.npmjs.org/gitbook-cli
   npm http GET https://registry.npmjs.org/gitbook-cli
   npm ERR! Error: CERT_UNTRUSTED
   npm ERR!     at SecurePair.<anonymous> (tls.js:1370:32)
   npm ERR!     at SecurePair.EventEmitter.emit (events.js:92:17)
   npm ERR!     at SecurePair.maybeInitFinished (tls.js:982:10)
   npm ERR!     at CleartextStream.read [as _read] (tls.js:469:13)
   npm ERR!     at CleartextStream.Readable.read (_stream_readable.js:320:10)
   npm ERR!     at EncryptedStream.write [as _write] (tls.js:366:25)
   npm ERR!     at doWrite (_stream_writable.js:223:10)
   npm ERR!     at writeOrBuffer (_stream_writable.js:213:5)
   npm ERR!     at EncryptedStream.Writable.write (_stream_writable.js:180:11)
   npm ERR!     at write (_stream_readable.js:583:24)
   npm ERR! If you need help, you may report this log at:
   npm ERR!     <http://github.com/isaacs/npm/issues>
   npm ERR! or email it to:
   npm ERR!     <npm-@googlegroups.com>
   
   npm ERR! System Linux 4.4.0-148-generic
   npm ERR! command "/usr/bin/nodejs" "/usr/bin/npm" "install" "gitbook-cli" "-g"
   npm ERR! cwd /home/jane/myspace/mygitbook/MiscRecord
   npm ERR! node -v v0.10.25
   npm ERR! npm -v 1.3.10
   npm ERR! 
   npm ERR! Additional logging details can be found in:
   npm ERR!     /home/jane/myspace/mygitbook/MiscRecord/npm-debug.log
   npm ERR! not ok code 0
   
   ```
   
   解决办法：
   
   ```
   sudo npm config set strict-ssl false
   ```
   
   
   
   **报错2：**
   
   ```
   jane@lemon:~/myspace/mygitbook$ gitbook init
   /usr/bin/env: node: No such file or directory
   ```
   
   ```
   ln -s /usr/bin/nodejs /usr/bin/node
   ```
   
   
   
   **报错3：**
   
   ```
   jane@lemon:~/myspace/mygitbook$ gitbook -V
   
   /usr/local/lib/node_modules/gitbook-cli/node_modules/fs-extra/lib/index.js:3
   const assign = require('./util/assign')
   ^^^^^
   SyntaxError: Use of const in strict mode.
       at Module._compile (module.js:439:25)
       at Object.Module._extensions..js (module.js:474:10)
       at Module.load (module.js:356:32)
       at Funnoction.Module._load (module.js:312:12)
       at Module.require (module.js:364:17)
       at require (module.js:380:17)
       at Object.<anonymous> (/usr/local/lib/node_modules/gitbook-cli/lib/config.js:2:10)
       at Module._compile (module.js:456:26)
       at Object.Module._extensions..js (module.js:474:10)
       at Module.load (module.js:356:32)
   
   ```
   
   ```
   升级Node.js：
   
   npm cache clean -f
   sudo npm install -g n
   sudo n stable
   ```
   
   升级成功后提示
   
   old : /usr/bin/node
   
   new: /usr/local/bin/node
   
   ```
   rm -rf /usr/bin/node
   sudo ln -s /usr/local/bin/node /usr/bin/node
   ```
   
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



```
cd mygitbook
git init
git remote add origin https://github.com/fatsweetfish/mygitbook
git push origin master
```




ref:https://www.jianshu.com/p/421cc442f06c

https://blog.csdn.net/lu_embedded/article/details/81100704



https://segmentfault.com/a/1190000017960359?utm_source=tag-newest

