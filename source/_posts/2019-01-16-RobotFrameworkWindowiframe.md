---
title: Robot Framework自动化网页测试之mouse over、select window(frame)
date: 2019-01-16 21:31:57
categories: 
- RobotFramework
tags: 
- 自动化测试
- work
toc: true
---

悬停：mouse over

切换窗体：select window

切换frame：select frame

这三个感觉真重要哦，第一次接触selenium的时候就被折磨的很惨，这次到了Robot Framework还是被折磨了，😒，从今以后搞定你。

### 1、mouse over

代码：

```c
MouseOver
    [Setup]    Open Browser    http://47.93.233.188/gpshop/    chrome
    Maximize Browser Window
    Mouse Over    xpath=//*[@id="js_climit_li"]/li[1]/div[1]/h3/a
    Sleep    2s
    Click Element    xpath=//*[@id="js_climit_li"]/li[1]/div[2]/div/div/div/div/dl[1]/dd[1]/a/span
    Sleep    3s
    [Teardown]    Close All Browsers
```

源截图：

![](http://pic.yuti.site/RF-MouserOver.jpg)

注：

（1）Set Up：起始语句；Teardown：结束语句 --> 不管程序期间会不会发生错误，他们都必定会执行

（2）在使用mouse over语句时，一定不要移动鼠标，不然不会出现这样的效果



### 2、切换窗体

切换窗口对下一个窗口进行操作

代码：

```c
SelectWindow
    [Setup]    Open Browser    https://www.baidu.com    chrome
    Maximize Browser Window
    Input Text    xpath=//*[@id="kw"]    林依晨
    Sleep    1s
    Click Element    xpath=//*[@id="su"]
    Sleep    2s
    Click Element    xpath=//*[@id="1"]/h3/a
    @{handles}=    Get Window Handles    #得到所有窗口的句柄；有没有=都可以
    Close Window    #关闭当前页
    Select Window    @{handles}[1]
    Sleep    2s
    Mouse Over    xpath=/html/body/div[2]/div/div/div/div/div/dl[3]/dt/a
    Sleep    2s
    Click Element    xpath=/html/body/div[2]/div/div/div/div/div/dl[3]/dd/div[2]/a
    Sleep    2s
    [Teardown]    Close All Browsers
```

本来想搜索一下自己的博客的，结果发现，呜呜呜呜，根本搜索不到，心痛。

源截图：

​![](http://pic.yuti.site/RF-SelectWindow.png)

注：${name}：定义变量；@{list}：表示数组；&{dict}：表示字典（即键值对）

### 3、切换frame

如果web页面中存在 iframe 标签，那么必须得切换到要进行操作的frame上，才能正确的进行操作。

![](http://pic.yuti.site/RF-SelectFrameLog.png)

就像这样，我们要使用的select下拉框在iframe下，那么我们就必须得切换到该frame下才能进行之后操作。

![](http://pic.yuti.site/RF-SelectFrameOutside.jpg)

如果我们在select下拉选择星座后，还行对Input进行搜索操作，那就必须得先退出frame，才能对输入框进行输入。请看代码

代码：

```c
SelectList
    [Setup]    Open Browser    http://www.hao123.com/xingzuonew    chrome
    Maximize Browser Window
    Sleep    1s
    Select Frame    xpath=//*[@id="J_iframe"]
    Select From List By Index    xpath=/html/body/div[1]/div/div[2]/ul[1]/li[1]/form/select    9
    Sleep    5s
    Unselect Frame#退出frame
    Input Text    xpath=//*[@id="grayFixed"]/div/div[3]/form/input    射手座
    Sleep    5s
    [Teardown]    Close All Browsers
```

源图片：

![](http://pic.yuti.site/RF-SelectFramePhoto.jpg)

注：F12调出开发者工具，找到相对应的元素，右键选中copy --> copy XPath即可完成元素选择

> 啦啦啦，完成啦，不容易啊，小姑凉。
>
> 碰到问题，解决他，会有很大成就感哦。