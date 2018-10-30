---
title: Maven+Appium+java关于计算器的测试Demo
date: 2018-10-11 14:25:44
categories:
- 工作
- 测试
- Appium
tags: 
- Appium
- 测试
- java
- maven
---

这两天一直在解决这个Demo出现的错误，明明之前就已经解出来过，不过一段时间没有接触，就忘的差不多了。以前一直觉得我花了那么多时间，之后肯定不会忘记，哎呀，我还是高估我自己了。所以这次怎么的也得好好记记笔记。

## Appium的工作原理

测试脚本通过http协议传输至服务端`http://127.0.0.1:4723/wd/hub`，再交由bootstrap来进行解析和发送指令至AndroidSDK中UIautomatorviewer，最后执行到界面中

## 创建过程

### 1、IDEA中Maven创建项目

先创建一个java项目，再导入相应的jar包也可以，但是我感觉Maven更加方便。

步骤：File -> New Project -> Maven(导入Android SDK包) -> next -> 填入GroupId、ArtifactId即可创建
![](http://pic.yuti.site/mavenBuild)

### 2、pom.xml内容添加
这里面填写的就是我们需要的依赖包，话不多说，直接上代码。

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>site.yuti.test.appium.demo</groupId>
    <artifactId>UITest</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>3.4.0</version>
        </dependency>

        <dependency>
            <groupId>io.appium</groupId>
            <artifactId>java-client</artifactId>
            <version>5.0.0-BETA7</version>
        </dependency>
    </dependencies>
</project>

```
其中dependencies里的内容就是我们需要添加的依赖。

### 3、创建一个Java Class文件

```
import io.appium.java_client.android.AndroidDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.remote.DesiredCapabilities;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.concurrent.TimeUnit;

public class TestDemo {
    public static void main(String[] args) {

        DesiredCapabilities capabilities = new DesiredCapabilities();
       // 虚拟机
//        capabilities.setCapability("deviceName", "Nexus 5 API 28");
//        capabilities.setCapability("automationName", "Appium");
//        capabilities.setCapability("platformName", "Android");
//        capabilities.setCapability("platformVersion", "9");
        
        //真机
        capabilities.setCapability("deviceName", "9eaefa04");
        capabilities.setCapability("automationName", "Appium");
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("platformVersion", "5.1.1");


        capabilities.setCapability("appPackage", "com.android.bbkcalculator");
        capabilities.setCapability("appActivity", ".Calculator");
        capabilities.setCapability("appWaitActivity", ".Calculator");

        //把以上配置传到appium服务端并链接手机

//        <WebElement> 这个不是必须的

        AndroidDriver driver = null;
        try {
            driver = new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }

        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
                driver.findElement(By.id("com.android.bbkcalculator:id/digit1")).click();
        driver.findElement(By.id("com.android.bbkcalculator:id/plus")).click();
        driver.findElement(By.id("com.android.bbkcalculator:id/digit5")).click();
        driver.findElement(By.id("com.android.bbkcalculator:id/equal")).click();
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        String result = driver.findElement(By.id("com.android.bbkcalculator:id/edit_result_text")).getText();
        System.out.println(result);

        driver.quit();
    }
}
```

### 4、运行
最后打开Appium，并点击运行，你就可以静等最后的效果啦。当然了，前提是你必须要自行安装Appium和Maven。可自行问度娘。

**注意1**：打开Appium的时候得进行如下修改，目的是为了跟代码匹配
![](http://pic.yuti.site/appiumStart)

**注意2**：以上代码有真机和虚拟机之分，如果是采用真机的方式，一定要用`adb devices`语句查看确保真机已经连接成功了。如果提示adb不是内部或外部命令，请自行安装。

## 问题解决

### 1、 name选择器的错误

错误提示：说不能采用name这样的获取方法（driver.findElement(By.name("1"))）

原因：在新版本里是没有name这个选择方式的，因此得自己手动添加

```
修改文件driver.js的地址路径：
C:\Users\Administrator\AppData\Local\Programs\Appium\resources\app\node_modules\appium\node_modules\appium-android-driver\build\lib
```
![](http://pic.yuti.site/driverChange)
在下面添加 'name' 即可。

### 2、版本问题

比如一直提示
```
AppiumDriver driver = new AppiumDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
```
这句话有错，但是有没有讲出具体错在哪里；比如说CSS选择器有问题
`Locator Strategy 'css selector' is not supported for this session`
，但是也没有具体指出哪里有问题，这些感觉代码都对，但是就是跑不通，能纠结你很久的问题，你都可以考虑考虑是不是Appium和Selenium的版本结合问题。

你可能会百度到说把他改成
```
AppiumDriver<WebElement> driver = new AppiumDriver<WebElement>(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
```
就可以解决问题，经验证这是不可行的，还会在<WebElement>下出现红色波浪线，我现在能确定出现这些问题都是是版本结合的问题。

就是因为这个问题，折磨了我很久，刚开始是真的毫无头绪。

哈哈哈，`pom.xml`文件中的两个版本是我尝试以后可以成功的版本。

### 3、真机上按钮的id如何获取

Android自带一个`uiautomatorviewer.bat`这个工具非常棒，他可以截屏获取id。

这个工具在此处可以找到，双击打开即可使用。

```
C:\Users\Administrator\AppData\Local\Android\Sdk\tools\bin
```
但是我遇到了一个很奇怪，之前没有遇到过的问题，如下图
![](http://pic.yuti.site/uiautomatorviewer.png)

我百度了好多，是要修改什么root，或者是修改uiautomatorviewer.bat里的call代码，对我来说统统没有用，最后是靠这两句代码解决的。

```
adb kill-server
adb start-server
```

如果用`adb devices`验证设备，如果出现`List of devices attached`的错误的时候，巧了，也可以用上面两个语句解决

> 经过整理发现也没有多少问题，但是确实还是被难住了，加油吧，少年。

