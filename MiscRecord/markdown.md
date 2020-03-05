

## Markdown语法

#### 一般常用:

**1.突出显示**

```markdown
==我是高亮== （默认为黄色)
`我是标记`
```

==我是高亮== （默认为黄色)
`我是标记`

**2.字体修饰**

```markdown
**加粗**
*斜体*
<u>下划线</u>
~~删除线~~
```

**加粗**
*斜体*
<u>下划线</u>
~~删除线~~

**3.自动编号**

```markdown
@[toc]
```

**4.硬换行符**

```markdown
<br/>
shift+enter
双击space键，右侧会出现一个灰色的向下箭头
```

**5.字体颜色、字号、大小**

```markdown
<font color=red>我是红色</font>
**<font color=red>我是红色加粗</font>**
<font color=red><strong>加粗方式２</strong></font>
<b><font color=red>加粗方式3</font></b>
<font face=黑体>我是黑体</font>
<font size=5>我是5号字体</font>
<font size=5 color=red face=黑体>红色5号黑体字</font>
```

<font color=red>我是红色</font>

**<font color=red>我是红色加粗</font>**

<strong><font color=red>加粗方式２</font></strong>

<b><font color=red>加粗方式3</font></b>

<font face=黑体>我是黑体</font>
<font size=5>我是5号字体</font>
<font size=5 color=red face=黑体>红色5号黑体字</font>



`<span style='color:文字颜色;background:背景颜色;font-size:文字大小;font-family:字体;'>文字</span>`

```
<span style='color:red;font-size:20px;font-weight:blob'>RED</span>
```

<span style='color:red;font-size:20px;font-weight:bold'>RED</span>

**6.上下标**

```markdown
H^2^
H~2~O
```

H^2^

H~2~O

**7.插入表情**

```markdown
:happy:
```

:happy:

**8.引用**

```
>
>>
>>>
```

>

> >

> > > 

**9.水平分割线**

```
---
***
```

---
***

**10.数学表达式**

```
使用$$符号包裹的Tex命令
右键>插入>公式
```



**11.标注**

```markdown
这是一个注释[^注释]
[^注释]： 这是一个注释
```

[^注释]: 这是一个注释

**12.插入图片(默认为 居中)**

```
右键>插入>图像
可以直接从“剪贴板”复制过来
![img](imgpath or url)
```

**13.调整图片尺寸**

```markdown
<img src='图片网址或者图片文件地址' style='width:300px;height:100 px'/>
<img src='图片网址或者图片文件地址' style='zoom:50%'/>
```

**14.插入视频**

```
将视频文件拖放到Typora中，Typora会自动插入视频
```



#### HTML常用语法

**1.居中**

```html
<center>居中</center>
```

<center>居中</center>
**2.高亮（默认为黄色）**

```html
<mark>高亮</mark>
```

<mark>高亮</mark>

**3.字体修饰**

```html
<b>加粗</b>
<i>斜体</i>
<u>下划线</u>
<s>删除线</s>
```

<b>加粗</b>
<i>斜体</i>
<u>下划线</u>
<s>删除线</s>

**4.上下标**

```html
< SUP > I’m feeling high. </ SUP > 
< SUB > I’m feeling low. </ SUB > 
```

HaHaHa<sup>i'm feeling high,</sup>

WuWuWu<sub> I’m feeling low. </sub>



#### Reference:

https://blog.csdn.net/weixin_44441012/article/details/86023918

#### [Markdown基本语法](https://www.jianshu.com/p/191d1e21f7ed)

#### [Markdown 编辑器指南](https://www.cnblogs.com/linuxAndMcu/p/11212486.html)

