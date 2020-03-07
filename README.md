如何搭建自己的Wiki
==================

前言
----

在漫漫人生之路上我们会学到许多知识，如何将这些零散的知识记录下来并整理归档就显得尤为重要，因此搭建一个属于自己的Wiki是一个不错的选择。在看到**乐鑫ESP-IDF编程指南**这份在线文档时候，突发奇想能否自己也构建这样一个在线文档系统呢？在查阅网上许多资料后发现这类文档系统一般借助于**Markdown+Sphinx+GitHub+ReadtheDocs**，正好周末闲来无事说干就干！

在正式搭建前先简单介绍一下各个工具：

> -   **Markdown：**一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，可以使普通文本内容具有一定的格式。它允许人们使用易读易写的纯文本格式编写文档，然后转换成格式丰富的HTML页面，Markdown文件的后缀名是“.md”
> -   **Sphinx：**一个基于ReStructuredText的文档生成工具，可以令人轻松的撰写出清晰且优美的文档，
>     由Georg
>     Brandl在BSD许可证下开发。新版的Python文档就是由Sphinx生成的，并且它已成为Python项目首选的文档工具，同时它对C/C++项目也有很好的支持；并计划对其它开发语言添加特殊支持。
> -   **GitHub：**这个我想无需多说
> -   **Read the
>     Docs：**一个在线文档托管服务，可以从各种版本控制系统中导入文档。支持webhooks，当你提交代码时，文档将被自动构建。

一、流程
--------

利用Markdown编辑器编写文档，然后通过格式转换工具将.md格式文件转换为.rst格式。接下来用Sphinx生成文档，将文档托管至GitHub，最后导入Read
the Docs在线展示！

二、实施部署
------------

本人是在window系统虚拟机中部署，当然你也可以直接在windows下部署，这个大家自己选择。

### 2.1 安装sphinx

``` {.python}
    //安装sphinx
    pip install sphinx sphinx-autobuild sphinx_rtd_theme
    //创建一个目录wiki
    mkdir wiki
    //切换至wiki目录
    cd wiki
    //快速初始化一个sphinx
    sphinx-quickstart
```

在执行命令sphinx-quickstart的时候，会让你输入配置，除了以下几个个性化配置外，其他的都可以按照默认的来（回车默认配置）。

``` {.python}
    Project name: Yuri's Wiki
    Project release []: 1.0
    Project language [en]: zh_CN
```

完了后，就可以看见创建的工程文件

-   build：文件夹，当你执行make
    html的时候，生成的html静态文件都存放在这里
-   source：文件夹：你的文档源文件全部应全部放在source根目录下
-   Makefile：编译文件
-   make.bat：bat脚本

三、撰写文章
------------

大家可以在网上搜一大把Markdown编辑器，可以根据自己的喜好选择一个撰写文档，不过话说如果第一次使用Markdown可能感觉很别扭，这都是word这类有工具栏帮助给惯坏了。在Markdown中格式化都是以符号标识来进行，所以如果要掌握Markdown需要一段时间的练习。
写好文档后，大家记得先将.md格式转换为.rst，这里给大家推荐一个在线转换工具[cloudconvert](https://cloudconvert.com/)，然后千万记得要把这个文档写进目录排版里面。

``` {.python}
.. toctree::
    :maxdepth: 2
    :caption: Contents:
    
    introduction
```

排版配置文件是 source\index.rst，千万要注意中间的空行不可忽略。
然后执行make
html生成html静态文件，可以用浏览器打开，如果效果不满意可以修改后重新编译。
![Building
test](http://www.yurichen1028.cn/wp-content/uploads/2019/11/building-test.png)

四、托管文档
-------------

在Github上新建一个repositorie，然后将刚才新建wiki目录里的文件上传至自己这个repositorie中，不知道如何上传的童鞋自己百度吧。

五、发布
--------

如果没有Read the
Docs账号可以先注册一个，然后关联一下GitHub，此时你就可以将GitHub里的项目导入到Read
the Docs中然后Bulid version，编译通过后可以通过短网址在线阅读文档了。

![Buliding
wiki](http://www.yurichen1028.cn/wp-content/uploads/2019/11/Building-wiki.png)
