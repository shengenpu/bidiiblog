---
title: 软件测试——Web测试篇
date: 2024-08-26 16:26:23
index_img: ../images/./软件测试/test01.png
tags: 软件测试 功能测试
--- 
# Web自动化测试
欢迎来到笔蒂I的软件测试系列，本部分分为：[功能测试](https://www.bidii.top/2024/08/26/软件测试/SoftWareTest/)，[Web自动化测试](https://www.bidii.top/2024/08/26/软件测试/webtest/)，[App自动化测试](https://www.bidii.top/2024/08/26/软件测试/apptest/)，[接口自动化测试](https://www.bidii.top/2024/08/26/软件测试/apitest/)，性能测试,还有一些面试题等内容，大家可自行跳转链接查看哦。
助大家早日找到工作哦~❤
**P0-P4为重要等级哦~**
## 什么项目适合做自动化？（P3）
1. 需求变换不频繁
2. 项目周期长
3. 项目需要做回归测试
**一般自动化测试在手工测试之后开始进行**
## 环境安装（P0）
本次自动化测试使用的是Python
1. 通过```scoop install python``` 下载python环境,安装完``` python --version ```可用查到版本号即可
2. 通过python自带的pip下载selenium ```pip install selenium ```，这是一个用于在Web浏览器上执行自动化测试的工具
3. 通过``` scoop install chromedriver``` 安装浏览器驱动，他用于模拟用户在浏览器中的行为
4. 至此Web自动化测试的环境已搭建完毕，可用开始代码之旅啦

## 基础代码（P0）
```
    from time import sleep
    from selenium import webdriver
    from selenium.webdriver.common.by import By
    op = webdriver.Chrome()
    op.get('https://www.baidu.com')
    sb=op.find_element(By.LINK_TEXT,"新闻")
    for i in range(0,100,1):
        sb.click()
    sleep(999)
```
执行之后你就会发现，**您的Chrome打开了一百多个新闻网页**...
![](../images/./软件测试/base.png)
如何做到的呢？
1. ```op =webdriver.Chrome() ```用于**创建一个Chrome浏览器实例**，可用于打开Chrome浏览器
2. ```op.get()```类似于在浏览器地址栏输入括号中的**字符串网址**,并且打开这个网站
3. ```op.find_element(By.LINK_TEXT,"链接的文本")``` find_element用于找到网页中的元素，括号中的值后面会详细讲解
4. 用找到的元素模拟100次的循环点击...于是打开了100个新闻网页
5. ```sleep(999)```程序休息999秒，主要为了我们可用及时看到效果

## 查找元素（P0）
**注：这边需要一点点HTML基础**
前面小案例里面提到了find_element方法，这个方法就用于查找元素，它一共有如下几种找元素的方法(**driver为浏览器实例**)：
1. driver.find_element(By.ID,"填写元素ID名来找到此元素")
2. driver.find_element(By.CLASS_NAME,"填写元素CLASS名来找到此元素")
3. driver.find_element(By.TAG_NAME,"填写元素标签名来找到此元素")
4. driver.find_element(By.XPATH,"填写元素XPATH路径来找到此元素")
5. driver.find_element(By.CSS_SELECTOR,"填写元素的CSS来找到此元素,注意这边ID加#，Class加.属性选择是[属性名=属性值]"),例如：```driver.find_element(By.CSS_SELECTOR,"#pig")```
6. driver.find_element(By.LINK_TEXT,"填写a标签的文本来找到此元素，例如刚刚的新闻")
7. driver.find_element(By.PARTIAL_LINK_TEXT,"填写a标签的模糊文本来找到此元素，也就是说我写个新也会找到新闻元素啦")
*注：模糊匹配最好使用具有唯一标志性的关键词（需要唯一代表性，否则默认返回符合操作的第一个，也可以使用完全匹配）*

## XPATH详解（P1）
上面的查找元素方法相信有HTML基础的应该不难理解，唯一没有接触过的就是XPATH定位。
1. 路径定位
   * 绝对路径：以单斜杠开头逐级开始缩写，不能跳     级，如：/html/body/div/p[1]/input
   * 相对路径：以双斜杠开头，双斜杠后面跟元素名  称，不知元素名称可以使用*代替
    如：//input 或者 //*
2. 路径结合属性：
     语法：在Xpath中，所有属性必须使用@符合修饰 如：//*input[@id="id值"]
3. 路径结合逻辑（多个属性）
	语法：//*[@id="id值" and @属性值="属性值"]
4. 路径结合层级
	语法：//*[@id='父级id属性值']/input
拓展：//*[text()="文本内容"]  根据元素的文本内容进行查找，多用于p标签、a标签
    //*[contains(@type,"word")]  属性中含有word的元素
    //*[starts-with(@id,"pass")]  id以pass开头的元素