---
title: 5.7-TestKnowledgePoint
date: 2024-05-07 14:33:38
tags: Test
---


## Selenium 浏览器操作


`driver需要初始化，指定driver的类型，创建driven的对象`

1. **打开网页** getUrl（）；返回为空，传入String；

2. **获取当前网页的标题** getTitle（），返回String；

3. **关闭浏览器** 有两个方法close和quit，会关闭页面

- 1. close方法不会关闭浏览器进程
- 2. quit方法会关闭浏览器进程

4. **浏览器页面切换操作** driver.switchTo.window(tab)
- 每个tab页面都有一个完整句柄
- 通过getWindowHandles() 来获取句柄


5. **导航操作：刷新、前进、后退**

- 1. 打开网页： navigate().to(url)

- 2. 前进/后退：navigate.forward()/navigate.back()

- 3. 刷新操作： navigate.refresh()

6. **浏览器窗口大小**

操作名称|代码
:---|:---|
获取大小|window().getSize()
设置大小|window().setSize(Dimension targetSize)
获取位置|window().getPosition()
设置位置|window().setPosition(Point targetPosition)
最大化|window().maximize()
全屏|window().fullscreen()

---
