---
title: MonkeyRunner在Eclipse中的开发环境搭建步骤(兼.py文件的创建运行)
date: 2019-03-29 14:50:53
categories: 
- Monkey
tags: 
- 自动化测试
- work
---

最近在学习MonkeyRunner，学学自己写脚本，哈哈哈，😺，MonkeyTest的升华版，下面我跟往常一样，写写开发环境搭建步骤。

如果你只是用sublime写了一个.py文件，用下面👇的语句就可以运行(cmd)

```python
monkeyrunner.bat address\name.py
```

这种方式不难，接下来我准备介绍一下MonkeyRunner在Eclipse中的开发环境搭建(Windows版)

## 开发环境搭建

### 1、PyDev插件安装

Open Eclipse -> help -> Install New Software -> Work with中输入:http://pydev.org/updates -> 选择PyDev进行安装

 ![](http://pic.yuti.site/PyDevInstall.png)

### 2、PyDev中配置Jython、Monkeyrunner环境

* Step1：找到Jython解析器的Jar包并解压(.jar可右击进行解压，解压时最好先创建一个文件夹保存解压出的文件)

  ![](http://pic.yuti.site/Monkeyrunner_Jython.png)

  

* Step2：将解压得到的Lib文件放到jython-standalone-2.5.2.jar的同级目录下

  ![](http://pic.yuti.site/Monkeyrunner_Lib.jpg)



* Step3：click Windows -> References ->  PyDev -> Jypthon Interpreter -> click Browse for Jython jar

  ![](http://pic.yuti.site/Monkeyrunner_JythonNew.jpg)

  

  注：一定要进行前两步，不然这一步会出错❌，错误提示为："Error:Python stdlib not found or stdlib found without .py files"

  

* Step4：如果新建Python工程时，提示如下错误：Project interpreter not specified，请进行以下操作，click Browse for Jython jar -> 选择python.exe的安装位置 -> 导入完成

  

  注：只能是python.exe哦，到这里为止我们已经配置好了Jython的开发环境，可以创建一个Jython的项目了，接下来，我们将进行MonkeyRunner的环境配置

  

* Step5：click Windows -> References ->  PyDev -> Jypthon Interpreter -> click New Jar/Zip(s)

  ![](http://pic.yuti.site/Monkeyrunner_JythonOtherjar.png)

  

  其实搭配MonkeyRunner开发环境就是把我们需要的包加入到Jython的PYTHONPATH里面，方便我们直接引用。而这些安装包就在jython-standalone-2.5.2.jar的同级目录下

## .py文件的创建与运行

#### 1、.py文件的创建

* Step1：File -> New -> Project -> PyDev -> PyDev Project ->填写相应内容(如下)

  ![](http://pic.yuti.site/Monkeyrunner_Project.png)

  

  注：一定要进行上面👆的第四步，选择python.exe的安装位置，不然这里就会报错，提示错误为："Project interpreter not specified。''

  

* Step2：File -> New -> PyDev Module -> 填写文件名称

  ![](http://pic.yuti.site/Monkeyrunner_Module.png)

到这里我们就把文件创建好了，是不是很激动，我们可以进行敲代码，啊哈，爽，写完，运行，可就是不能成功，在sublime中可以执行的文件，怎么到Eclipse中，不行了，我找到了一个解决办法，往下看。

#### 2、.py文件的运行

* Step1：Run -> External Tools -> External Tools Configurations -> 根据下图⤵进行配置！

  ![](http://pic.yuti.site/Monkeyrunner_Run.jpg)

  

  &

  ![](http://pic.yuti.site/MonkeyRunner_Running.jpg)

  

  哈哈哈，over，你可以愉快使用下面👇这种方式运行了。

  

* Run -> External Tools -> 你取的Name 

  

  但是有点瑕疵，以上配置只针对test02.py，就是你.py文件修改了，上面👆相应Arguments的配置也得进行修改；如果有新的PyDev Package，那么需要同时更改Working Directory和Arguments的配置。

  

  所以最好一个项目中弄个主文件，其他为函数，在主文件中调用函数即可

## Github自动化初始文件

这几天自己写了一个安装、启动、登录、Monkey、退出、卸载这六大模块，虽然Monkey还不是很完善，有待改进，但是，这也是我的进步，开心，😺。

[github-monkeyrunner](https://github.com/yutiJin/MonkeyRunner)

