
			




    
        
            
#### [用Markdown来写自由书籍-开源技术的方案](http://www.ituring.com.cn/article/828)
        



        
            
                
    
[推荐](http://www.ituring.com.cn/article/vote/828)
    

#### 17



    [收藏](http://www.ituring.com.cn/article/vote/828?isFave=True)











            


            
                

#### {{ page.title }}


#### 背景

随着互联网的进步和技术积累，国内技术圈交流的气氛越来越浓，微博博客上到处可见有质量的技术贴，但是有时候想系统阅读时却不是很方便，如果能够整理成册自由分享该有多好。虽然少数人有幸通过出版社出书了，但代价太大，也不能普及大众，现在技术那么发达，有没有办法自己自助出版呢？



看了图灵社区的文章[为什么写作自由书籍？](http://www.ituring.com.cn/article/details/764)，作为爱书之人，我为什么不能想个办法来解决呢？



技术无极限，办法现在有好几种，在本文中，我就介绍用现在流行的Markdown格式的方式来产生专业的书籍，而且还可以做到利用互联网，不需要本地机器参与的完美方案。如果你喜欢微软的Word，觉得用它已经足够了，那我们不是同道，不用往下看了。




#### markdown能做出什么效果呢？

多说无益，先来看看效果吧。下面是我去年写的一本小册子：[跟我学企业敏捷开发](https://github.com/downloads/larrycai/sdcamp/sdcamp.zh.snapshot.pdf) 在PDF阅读器中的效果。注意还有完整的目录和页眉。



![http://larrycai.github.com/images/mkbokpdf.png](http://larrycai.github.com/images/mkbokpdf.png)



书的内容就全是用markdown格式写的，上图相对应的文件内容（6.2节）片断如下。




```
## Cucumber 简介 ##
Cucumber（英文：黄瓜）(官方网站是<http://cukes.info/>)是一个实例化需求的极佳实现伴侣。它是基于Ruby的开源测试工具，得益于Ruby便于创建和使用DSL的特性，它可以通过自然语言（文本文字）来描述需求（业务层），并通过关键字驱动和正则表达式匹配告诉去做哪些事情（驱动层），在运行自动化测试结束以后，还会给出详细的报告。

Insert 18333fig0601.png
图 6-1. Cucumber的架构

下面就是一个加法例子的需求描述，Cucumber文件以`.feature`结尾。

  # 加法 adding.feature
  Feature: Adding
    In order to avoid silly mistakes
    As a math idiot
    I want to be told the sum of two numbers

```


下面就是书的全部markdown文件，每一章一个文件。我把它们分成了序、前言、致谢、正文和附录，蛮像回事吧。有兴趣的朋友可以看看[作译者手册](http://www.phei.com.cn/wstg/zyzxz)，来了解标准的书是怎么组成的。




```
$ find zh
zh
zh/0preface
zh/0preface/00-chapter1-preface.markdown
zh/0preface/00-chapter2-changes.markdown
zh/0preface/00-chapter3-acknowledgement.markdown
zh/1chapters
zh/1chapters/01-chapter1-agile-scrum.markdown
zh/1chapters/01-chapter2-git-gerrit.markdown
zh/1chapters/01-chapter3-ci.markdown
zh/1chapters/01-chapter4-java.markdown
zh/1chapters/01-chapter5-sbe.markdown
zh/1chapters/01-chapter6-cucumber.markdown
zh/1chapters/01-chapter7-workshop.markdown
zh/2appendix
zh/2appendix/02-chapter1-sample.markdown
zh/2appendix/02-chapter2-cc2git.markdown

```


全书的内容够可以在github上找到[https://github.com/larrycai/sdcamp/tree/master/zh](https://github.com/larrycai/sdcamp/tree/master/zh)



样式的产生全部有模板完成，一般不需要改动，这个稍后讲。




#### 什么是markdown

有兴趣了，就可以聊聊markdown了，简单来说，markdown格式的文件看着像一般的文本文件，里面只是加了很少的格式标记，因此看文本文件也不影响理解，这种格式也有很多工具帮你去转化，而且很容易自动化解决。并且这些技术大多数是开源或免费的。



如 ## Cucumber 简介 ##就可以转换成html的<h2>Cucumber 简介</h2>或者书中的小节, 空四个就是表示代码，是否很简单。具体可以看图灵社区的文章 [Markdown语法说明（详解版）](http://www.ituring.com.cn/article/504)




#### 为什么要用markdown

原因也很简单，因为简洁和流行。markdown格式的普及要归功于Github和[StackOverflow](http://stackoverflow.com/)。因为它们越来越流行，它们支持markdown格式也越来越流行。这里要赞一个的是，国内的[图灵社区](http://www.ituring.com.cn/)也支持markdown，用起来超级方便。



我的体会是，它让你关注内容，格式怎么显示不是要你在写得时候关注的。Word让我讨厌的原因就是老要关注格式。



实际上核心是软件思想中的分离，就像HTML关注内容，CSS关注格式表现一样。




#### 背后的魔法

从Markdown源文件产生电子书一般有两种方案：一种是产生HTML中间格式再转换出电子书，另一种是对应地转换产生出[LaTeX](http://zh.wikipedia.org/zh/LaTeX)文件格式，再和LaTeX模板合在一起，最后转换产生PDF，达到标准书籍出版的质量（完整的封面，目录，页眉等等），这里主要讨论第二种。



![http://larrycai.github.com/images/mk2pdf.png](http://larrycai.github.com/images/mk2pdf.png)



LaTeX（就是Donald E. Knuth（高德纳）发明的）是一个出版界（至少是科技界）常用的格式，PDF也能很容易地产生出来，它的好处是内容和形式是很容易分开的，感谢大师的设计。



Markdown可以通过工具自动转换出LaTeX的标准内容。




```
\section{Cucumber 简介} % 

```


就是上面由## Cucumber 简介 ##自动生成的LaTeX内容，表示小节。



余下书的表现形式就有预先调好的LaTeX的模板来处理，像页眉、目录、字体之类的和内容无关的就全部有LaTeX搞定了。不同的出版社或者图书系列都会有特定的模板，这和作者的内容无关。



这有点像HTML和CSS的关系。下面这一段是调整小节标题显示：




```
\definecolor{colorsection}{RGB}{95,158,160}    % CadetBlue
\setromanfont[Mapping=tex-text,BoldFont="WenQuanYi Micro Hei"]
\titleformat{\section}
    {\color{colorsection}\normalfont\Large\bfseries}
    {\color{colorsection}\thesection}{1em}{}

```


\bfseries 是让 LaTeX 使用粗体字排版，这儿选择了文泉驿的微黑。



下面这一段是调出页眉左上角（LE=Left Head）的：显示页码和内容，颜色设定为钢铁蓝，




```
\definecolor{colorheader}{RGB}{70,130,180} % SteelBlue
\fancyhead[LE]{\color{colorheader}\quad\small\textbf\thepage\quad\quad\small\leftmark} %页眉左上角

```


初看有点复杂，学习曲线蛮陡的。不懂的话，知道里面含有样式就可以了，反正你可以用现成的模板，这也是出版的专业所在，不用写书的负责。



工具软件[pandoc](http://johnmacfarlane.net/pandoc/)能帮着从markdown转换出LaTeX格式，然后通过[TexLive](http://www.tug.org/texlive/)软件中的xelatex再转成PDF格式。



强烈建议你到[Pandoc的在线实验环境](http://johnmacfarlane.net/pandoc/try)试一下。



这里主要讨论PDF的格式，实际上epub/mobi格式的用pandoc生成也很方便。




#### 其他常用格式的出版方案

计算机类图书对格式要求不是很多，图文、章节、源代码基本就够了，就算有些复杂公式，也可用图来显示。这也从理论上说明，它不需要复杂的格式。现在对这类技术书出版我的理解主要有几种：




Microsoft的Word格式，虽然国内出版界如日中天，缺省就认它（对技术没追求，鄙视）。简单好学，但是不擅长自动化，是开源的死敌。

直接用LaTeX格式，这是很棒的东西，特别适合学术类的各种复杂的公式等，不过学习曲线很高，国内也只有几家学术期刊使用。

DocBook格式是最有名的（从SGML演化过来），O'Reilly和Pragmatic出版社缺省就用它，它能很方便地转化出出版要的各种样式。如[Jenkins - the definition guide](http://www.wakaleo.com/books/jenkins-the-definitive-guide)开源书就是采用docbook。但由于是XML格式，很多人不习惯，而且多人网上协作不是很方便。

通过蒋鑫的[Got Github](http://www.worldhello.net/gotgithub/)开源书，我也了解reStructureText也是和markdown差不多纯文本（plain text)的，也是蛮流行的，结合[sphinx](http://sphinx-doc.org/)也所向无敌。



#### 自己动手产生电子书

讲了那么多，作为码农，该动手实践一下，其他读者可以跳过这一章。



你需要一台Linux机器（虚拟机就可以了）和简单的Linux命令就可以试验了。有git和ruby的知识那就更方便了。



我用的试验环境是Ubuntu 12.04 (Precise) 版本。




#### 下载书的源代码

很简单，git clone一下就可以了，下载它的源文件包我觉得还是烦了点。




```
$ git clone https://github.com/larrycai/sdcamp.git

```


生成PDF是一个比较复杂的东西，用到了[pandoc](http://johnmacfarlane.net/pandoc/)和[TexLive](http://www.tug.org/texlive/)软件，用Ubuntu库里就可以了。关于Pandoc，可以看图灵社区翻译的文章[关于通用文档转换器Pandoc](http://www.ituring.com.cn/article/679)，TexLive就是LaTeX的工具集。




```
$ sudo apt-get install pandoc 
$ sudo apt-get install texlive-xetex texlive-latex-recommended texlive-latex-extra # 安装texlive 2011

```


因为是中文PDF，需要把字体嵌入在文件中，因此需要安装字体文件（如果不是Ubuntu中文版），具体可看我在图灵社区的文章[开源书和开源技术-PDF中蛋疼的中文字体](http://www.ituring.com.cn/article/904)




```
$ sudo apt-get install ttf-arphic-gbsn00lp ttf-arphic-ukai ttf-wqy-microhei ttf-wqy-zenhei

```


现在你就可以生成pdf文件了。




```
$ ./mkbok    

```



#### mkbok 脚本

pandoc本身也支持模板，但很多情况下，还需要调整，写个脚本就方便多了。我用的脚本mkbok是基于[Pro Git](http://github.com/progit/progit)里面的脚本makeebooks和makepdfs开发的。原书作者Scott原来还用[calibre](http://calibre-ebook.com/)产生epub文件，我统一用pandoc。并原有的基础上进行了扩展，统一为mkbok脚本。




```
$ ./mkbok --build pdf,html,epub --lang zh --template latex/template.tex

```


这样就可一次性完成电子书的活，而且还改造了LaTeX模板（加了前言、致谢和页眉等，使它最后的结果更像一份标准的书。主要功能差不多，但是扩展应该会更好些，特别是有机会更方便地采用不同的专业模板。




#### 基于Github和Travis-ci的互联网在线方案

你可以建一套基于上述技术的方便的出版系统。不过也可以利用互联网的服务，混搭一下。Github和Travis-ci就是我要利用的混搭服务。



Github和Travis CI这里就不介绍怎么使用了，具体可以先看[晓斌的博客](http://www.juvenxu.com/2012/03/06/travis-ci/)和蒋鑫的[Got Github](http://www.worldhello.net/gotgithub/)，强烈建议你先试一下。要不下期码农吧。



简单道理就是当你把代码推送到Github时，就可以触发Travis-ci的构建。Travis-ci会启动一个基于Virtualbox的Ubuntu的虚拟机（当前是12.04版本），然后根据你的.travis-ci.yml中的配置来构建你的产品，也就是执行上面的步骤来产生PDF文件。



构建结束后，虚拟机会被删除掉，虽然Travis-ci网站本身没有提供归档功能，但是Github的API提供了极好的方法来上传文件。所以我们可以用

#### Github API和Travis-ci的保密环境变量

的方式来把Travis-ci的结果上传回Github。



具体请看我的博客[把Travis-ci的结果上传回Github](http://larrycai.github.com/2012/11/06/publish-the-artifacts-inside-travis-ci-to-github.html)。



李明老师的[源码开放学ARM](http://www.lumit.org/LASO/)也是此方案的忠实用户，基本上可以全用浏览器解决。




#### 结尾

里面的技术细节还有蛮多的，不知是否你都明白，实际上照着试一遍，你会发现不是那么复杂。如果有问题，尽管找我 （@larrycaiyu）。



我一直设想中有一天上面提到的各个环节都能打磨得非常流畅，吸引更多的使用者。然后能够有很多人有兴趣用它来写书，可能是自娱自乐，也可以免费出版。不管怎样都是促进图书业。



出版界或者LaTeX的高手可以提供设计些更好的LaTeX模板（可以收费）供大家使用。



图灵出版社也提供网上的编辑服务（当然是可以收费的），对一些想把书写得专业点的作者提供额外的帮助，这样或许是一个很好的增值服务。至少像我这样的文笔超烂的技术人员很想得到的。



这些本是我2012想做到的事情：[设想中的开源书项目](https://github.com/larrycai/kaiyuanbook)，而且域名都买好了，留个遗憾放到明年吧。



技术无极限，只怕没追求。 


                



                
本文仅用于学习和交流目的，不代表图灵社区观点。非商业转载请注明作译者、出处，并保留本文的原始链接。
                


                

[markdown](http://www.ituring.com.cn/article/tagged/214)

[电子书](http://www.ituring.com.cn/article/tagged/924)

[pandoc](http://www.ituring.com.cn/article/tagged/947)

[文档转换器](http://www.ituring.com.cn/article/tagged/951)

[latex](http://www.ituring.com.cn/article/tagged/1079)
                                                            
                        
                            
