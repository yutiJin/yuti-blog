---
title: Robot Framework自动化网页测试之环境配置及HelloWorld(Windows版)
date: 2019-01-12 09:33:10
categories: 
- RobotFramework
tags: 
- 自动化测试
- work
---

注意：Robot Framework只支持python2.7以下的（2.7版本的最nice），不支持3以上的哦，不然你会一堆能烦死你的bug。

Robot Framework的主要特点：

**表格型语法 + 关键字驱动 + 数据驱动 + selenium为基础**

好来，来个该篇的环境安装的灵魂 -- 思维导图

![安装和启动](http://pic.yuti.site/RF-ProcessTotally.png)

## 环境安装

### Python安装：

#### 1、安装Python2.7.14

* 下载地址： [Python2.7.14](https://pan.baidu.com/s/154g7mC0KTBkok3dz08sOLA)  
* 密码：wm9e
* 下载直接双击安装即可

#### 2、Python环境配置

* 在path下面追加`C:\Python27;C:\Python27\Scripts;`两个目录（如图）

![环境配置](http://pic.yuti.site/RF-EnvironmentConfig.jpg)

注：Python3版本和Python2.7版本能共存，但是如果有两个2.7版本就会出错，竟然你觉得你步骤啥的都没有错，可就是不对，唉，我就是因为共存了两个2.7版本的Python，然后，嗯呢，炸裂

### Robot Framework安装：

#### 1、wxPython包的安装

Python图形用户界面的使用需导入wxPython包，这是一个成熟而且特性丰富的包RIDE是基于这个库开发的，所以必须安装。

* 下载地址：[wxPython](https://pan.baidu.com/s/1teYlvb9PNv26V5QsEs48Ew)  
* 密码：8atq
* 也是直接下载安装即可（<small>Python27会多出一个site-packages文件夹</small>）

#### 2、cmd命令行中用pip下载

```
pip install robotframework

pip install robotframework-ride               //RIDE是Robot Framework测试数据的编辑器

pip install robotframework-selenium2library
```



注：如果cmd直接打开下载不了，有可能是你环境配置有问题，你可以进入 `C:\Python27\Scripts` 中再输入语句，可能就是电脑问题，我就是怎么都不行，中途一路怀疑自己，哈哈哈

### WebDriver安装：

### 1、下载地址

* 谷歌：[ChromeDriver](http://chromedriver.storage.googleapis.com/index.html)  

  （<small>note.txt中查看你谷歌版本对应的ChromeDriver，一定要对应哦，不然之后肯定会出错，这个坑我帮你们踩过了</small>）

* 火狐：[GeckoDriver](https://github.com/mozilla/geckodriver/releases)

* IE：[IEDriverServer](http://selenium-release.storage.googleapis.com/index.html)

#### 2、存放地址

下载后解压的WebDriver放在` C:\Python27` 文件夹中（如图）

![webdriver](http://pic.yuti.site/RF-WebDriver.jpg)

### 启动：

安装完毕，那就必须是启动啦。

进入`C:\Python27\Scripts`找到ride.py，右键选择`打开方式（Python）`打开即可，会有两个弹窗，都要保留着哦。



## 快捷方式及图标处理

一定会觉得这样开启不方便是不是，想要一个快捷的方式打开，哈哈，一起来见证

#### 1、创建快捷方式

* 地址：`C:\Python27\Scripts`
* 如果没有ride.py的快捷方式，则创建一个；否则只要发送到桌面快捷方式即可

![ride.py快捷方式](http://pic.yuti.site/RF-RIDEPy.jpg)

但是有个问题哦，这个图标不好看，想不想换一个，想的话，follow me。

#### 2、修改图标

* 右键选择属性
* 点击更换图标按钮
* 选择图标（地址：`C:\Python27\Lib\site-packages\robotide\widgets\robot.ico`）

这样就可以啦，啦，啦，啦，开心。

![robot图标](http://pic.yuti.site/RF-RobotIco.jpg)



## Demo

ok，软件安装、环境配置、图标更换等前期基本工作都做好了以后，重头戏来了 -- first demo

基本路程：Project --> Suite --> Case

#### 1、创建新项目 new project

* File --> New Project 或者（Ctrl + N）

![new project](http://pic.yuti.site/RF-Newproject.png)

注：选择directory原因是，在directory的项目下可以创建测试套件，如果是tpye为file，则只能创建测试用例，这不利于用例的管理。



#### 2、创建测试套件 new suite

* project右键New Suite 或者（Ctrl + Shift + F）

![new suite](http://pic.yuti.site/RF-Newsuite.jpg)

注：选择file原因是，在file的测试套件下可以创建测试用例，如果是tpye为directory，还得重新再继续建file的测试套件，才能创建测试用例，因为测试用例只能在file类型下创建。

#### 3、创建测试用例 new test case

* suite右键New Test Case 或者（Ctrl + Shift + T）

![new test case](http://pic.yuti.site/RF-Newtestcase.png)

over, 最终显示如下，那你就成功一半啦：

![finally show](http://pic.yuti.site/RF-testdemoshow.png)

#### 4、导入库

我们只是RF是以selenium为基础，因此RF是需要selenium库的支持，而我们之前也下载selenium2library 库了，二话不说，导入。

* 点击suite，即Browser
* 在 Edit 的标签页，点击“Library”按钮
* 在弹出输入框中输入：Selenium2Library （要注意大小写）
* 点击 OK 完成

![add library](http://pic.yuti.site/RF-AddLibrary.png)

注：如果导入的库显示为红色，表示导入的库不存在；如果是黑色则表示导入成功。其中RF有个bug就是不能自动刷新，因此你发现自己如果是红色，不着急，你先刷新一下，如果还是红色，那就只能重新添加一遍了

Robot Framework所支持的测试非常丰富，如下图：

![](http://pic.yuti.site/RF-SupportLibrary.png)



#### 5、编写测试用例

Case书写界面：

![write test case](http://pic.yuti.site/RF-WriteCase.png)

TestCase实例：

![](http://pic.yuti.site/RF-TestCaseDemo.png)

注：按F8启动，如果报错pybot的错误，你看看你有没有pybot.bat文件

* 下载地址：[pybot.bat](https://pan.baidu.com/s/11QXS4a0Egt2XmN_nereUyQ )
* 密码： h6bn

你可能会说，我怎么知道哪些是关键字，嘻嘻，我也不知道，那么我们就可以按F5快捷键来打来帮助文档查看关键字，下图为一个例子：

![](http://pic.yuti.site/RF-TestCaseDemo.png)

over！😯



## 总结

> 环境的搭建一直都是我难题，老是会莫名其妙的出现很多意想不到的bug，能折磨的我想放弃，我也很无奈，所以记下笔记，希望我走过的坑，你们可以避免。
>
> 不过写了一天的文档是我没有想到的，不过很有成就感。
>
> 找资料的时候又发现了虫师大神的Robot Framework文档，又可以深入膜拜啦