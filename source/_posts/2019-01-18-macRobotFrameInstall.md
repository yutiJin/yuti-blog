---
title: Robot Framework自动化网页测试之环境配置(mac版)
date: 2019-01-18 11:20:06
categories: 
- RobotFramework
tags: 
- 自动化测试
- work
---

之前已经在windows安装过了Robot Framework，但是吧，马上就要过年回家了，把两台电脑都带回去，太重了，所以准备给我的mac也安装一个，so，又折磨了我很久，才弄好，所以准备写个笔记，造福你们以及之后忘记的我，哈哈哈。

[Robot Framework自动化网页测试之环境配置及HelloWorld(Windows版)](https://yuti.site/2019/01/12/RobotframeworkInstall/)，有需要，可点击观看。

## 环境安装

mac自带python2版本，所以直接安装pip即可

### 1、安装pip

```
sudo easy_install pip    --安装pip

pip help      --测试安装是否成功
```

### 2、安装robotframework

```
sudo pip install robotframework   --安装RobotFramework
```

注：如果之后运行时出现Robot Framework installation not found. To run tets, you need to install Rob…unexpected error: /bin/sh: pybot: command not found这样的提示错误，那么请进行以下操作：

```
sudo pip uninstall robotframework    --pip自动安装的是3.1版本的

sudo pip install robotframework==3.0
```

### 3、安装 robotframework-ride

```
sudo pip install robotframework-ride
```

### 4、安装wxPython

重头戏来啦。。。

```
sudo pip install -U wxPython
```

如果你在执行ride.py之后，提示语句为：<span style='color:brown'>wxPython not found. You need to install wxPython 2.8.12.1 with unicode support to run RIDE</span>，那么你就可以根据他给的网址进行下载安装，或者到以下百度云下载并安装解析。

下载地址：[wxPython](https://pan.baidu.com/s/1z7OqUK0BdyRZCpgWYaVsVQ )

密码：24kb 

**下载之后的操作步骤：**

（1）拷贝pth文件到指定目录

```
sudo cp ~/Downloads/wxPython2.8-mac/wxredirect.pth /Library/Python/2.7/site-packages/
```

（2）解压wxPython-unicode-2.8.12.1文件，拷贝wxPython目录到指定目录（请先确保你的/usr/local/lib目录是存在的，如果lib目录没有就先创建）

```
sudo cp -r ~/Downloads/wxPython2.8-mac/wxPython-unicode-2.8.12.1/ /usr/local/lib/wxPython-unicode-2.8.12.1/
```

拷贝完成后，确保/usr/local/lib/wxPython-unicode-2.8.12.1/目录下是bin、include、lib、share四个目录，这样就完成了wxPython的安装了。

<small>注：Downloades路径为你本机路径即可，可跟我不一样</small>

（3）如果运行ride.py会提示这个：<span style='color:brown'>python should be executed in 32-bit mode with wxPython on OSX</span>，那么在终端运行以下命令

```
defaults write com.apple.versioner.python Prefer-32-Bit -bool yes
```

### 5、安装selenium2library

```
sudo pip install robotframework-selenium2library     --依赖包
```

### 6、chrome配置

下载地址：[chromeDriver](http://chromedriver.storage.googleapis.com/index.html)

依旧根据自身chrome的版本号进行安装

（1）下载好后，将chromedriver.exe放入指定目录下即可

```
sudo cp ~/Downloads/chromedrive /usr/local/bin/
```

（2）路径配置

```
cd ~

touch .bash_profile

open -e .bash_profile
```

（3）在打开的TextEdit文件中输入以下路径

```
export PATH=$PATH:/usr/local/bin/ChromeDriver
```

同理，其他浏览器的webDriver也是如此设置即可。

## 总结

经过以上步骤，你的Robot Framework就安装好，是不是迫不及待的想使用了，哈哈哈，在Terminal中输入`ride.py`即可使用，具体的使用方法和Windows异曲同工，差不多啦，就不重复啦。