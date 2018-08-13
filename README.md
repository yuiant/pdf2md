# pdf2md项目


## 1 工作内容：
1. 区块链项目白皮书pdf格式转Mardown格式
2. 一个币对应一个目标文件夹，目标文件夹里的内容：
  - 数字币白皮书pdf原文
  - 名为img的文件夹：里面放着markdown文件里引用到的截图，主要从pdf原文中用个截图软件截下来。
  - main.md：从pdf转换后的markdown格式文件。


## 2. 规范

### 2.1 步骤
- **Step1**:新建一个与币名同名的文件夹
- **Step2**:把币的白皮书xxx.pdf与template.md复制到上面创建的文件夹。并将template.md重名为main.md,同时在当前目录下新建一个名为img的文件夹
- **Step3**:根据白皮书内容，填充meta信息。一般有title（题目），author（作者），date（日期）和摘要、关键字等信息。无则留空。

- **Step4**:把pdf文本通过pdf阅读软件复制出来（通常ctrl+c，ctrl+v）,并在markdown编辑器上按markdown格式进行重新排版,注意保留原文的篇章层级结构。
- **Step5**:不需要保留目录、页眉、页脚、页码。删掉。
- **Step6**:处理原文出现的图，表，公式，代码
- **Step7**:处理脚注（footnotes)

### 2.2 划重点！！

#### 2.2.1 段落的层级结构
- 表示标题那行的上一行要留出一个空白行：
    （空白行）

    \# 一级标题

	(空白行)

    \##  二级标题
 
- 段落之间用一行空白行隔开
- 同一段落的文本从pdf中复制到markdown编辑器中可能会强硬断开成几行，要重新接驳成一段。


#### 2.2.2 列表
- 表示有序列表时候，用"序号"+“.”+"空格"的形式(注意空格是必须的，不能漏掉空格)：
  a. haha   
  b. hehe
序号有可能是数字/字母/带括号的数字字母，看具体原文是采用哪一种
- 表示无序列表时，统一用“-”+"空格"表示。其中“-”是减号
- 列表里可以包含子列表，通过缩进的方式实现。其中缩进统一采用两个空格:
  \- 列表1
  \- 列表2
   (2个空格)\-子列表2.1 
   (2个空格)\-子列表2.2


#### 2.2.3 metadata
metadata是一段头尾用三个减号“---”围成的文本块，在template.md里。主要放文章的一些基本信息，请根据pdf原文内容来填写，没有的就留空
\---
title:
author:
date:
keywords:
abstract:
\---


##### 2.2.3.1 详解

- title:文章的题目，如果文章题目含正副标题，用"|"隔开。title的全部内容用单引号包着
- author:文章的作者，用无序列表的方式记录。记录姓名，如有邮箱，和姓名用英文冒号:隔开
- date:日期，统一采用yyyy\-mm\-dd的格式,用单引号包着
- keywords:关键字，通常出现论文形式的文章开头。用中括号\[\]括起，并用英文逗号“,”做分隔
- abstract:摘要。通常出现在论文形式的文章正文前。通常为一段文本。请在abstract:后加一条竖线"|"，然后另起一行再粘贴摘要内容。**如果不是论文形式的文章，摘要也可单独成一个章节，abstract:这里的内容留空**

##### 2.2.3.2 示例
\---
title:'mytitle|my_subtitle'
author:
\- author1:author1@gmail.com
\- author2:author2@gmail.com

date:'2018-11-11'
keywords:[test,example,work]
abstract:|
This is the abstract of the article。。。
\---



#### 2.2.4 脚注（footnote）
- 脚注格式是[^脚注号]
- 脚注标记和脚注解释：
..this is an example of footnotes[^1]-----(脚注标记)

..

..

..this is another example of footnotes\[^2\]----(脚注标记)


--(the bottom of the article)

[^1]the meaning of footnote1 ---脚注解释，统一放在文章末尾

\[^2\]the meaning of footnote2
..
- 因为转换成markdown后没有了页的概念，所以要将全文出现过的脚注及其解释，重新编号后全部追加到文章末尾

#### 图表公式代码
pdf出现过的图表需要重新截图到本地。所有截图放在币名文件夹目录下的img文件夹中。
##### 图
- 通常是一些架构图，和一些人物图。截图到本地的命名法则是:fig+序号.png,如：
fig1.png,fig2.png等等。
- 在markdown里引用本地图片,绑定链接文字，并标记图片说明:
示例：
看看下面Figure1,是POW的架构图
[这里是具体图片]
Figure1:Pow架构图


如上，第一行的Figure1是图片的链接文字，最后一行是图片说明。写成markdown：
看看下面\[Figure1\]\(#fig1\),是POW的架构图
\![Figure1:[]{#fig1}POW架构图]\(img/fig1.png\)

链接文字是点中后能定位到图片的位置，用中括号括住，后跟用小括号括住的图片id(#fig1是图片id,这个id是你自己随便起的，但一定以#开头，系统才知道它是个id)。格式：\[链接文字\]\(#fig_id\)


img/fig1.png是本地的图片路径（相对路径即可）。因为与main.md与img文件夹同在一个目录下，所以直接写img/fig1.png就能读到对应的图片文件。


“Figure1:POW架构图”（最后一行）是图片说明。图片说明和图片路径按照如上格式写在一起，一个符号都不能少（感叹号，英文中括号，英文小括号）


##### 表格
表格的处理方式与图片的处理方式类似，都是截图到本地，然后在markdown里引用。截图的命名法则是：“tbl”+"序号"+".png,如：
tbl1.png,tbl2.png tbl3.png..


##### 公式
- 优先采用latex重新编写公式。具体方法可参看附录教程
- 对于一些比较独立的没有很少上下文引用的公式，允许以截图形式出现，处理逻辑与图片类似。命名法则的前缀是formula,如formula1.png,formula2.png..

##### 代码
所有文章中出现的代码不采用截图形式，统一用markdown格式重新编写，格式：

\```


code


\```

头尾用三个\`包着代码块

#### 文献引用
文章中出现过的引用文献表示成[号码]。并在Reference章节以列表形式列出。


#### 其他：
- 字体的样式不用处理，正常字体即可。不用还原原文中的加粗，下划线，斜体等
- 原文的目录不需要在markdown里出现，删掉。
- 页眉页脚页码，删掉。（注意页脚不是脚注）

## 附录
- [markdown教程](https://www.jianshu.com/p/1e402922ee32)
- [latex编写公式](http://mengrenzi.com/2017/06/15/Mathjax%E4%B8%8ELaTex%E5%85%AC%E5%BC%8F%E7%AE%80%E4%BB%8B/)
- [示例](https://github.com/yuiant/pdf2md/tree/master/example/bread)
- [template.md模板](https://github.com/yuiant/pdf2md/blob/master/template.md)
