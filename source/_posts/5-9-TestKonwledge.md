---
title: 5.9 TestKonwledge
date: 2024-05-09 15:57:20
tags: Test
---

## 元素定位
- findElement(By.id()): id 定位
- findElement(By.name()): name 定位
- findElement(By.linkText()): linkText 定位
- findElement(By.partialLinkText()): partialLinkText 定位
- findElement(By.className()): className 定位
- findElement(By.tagName()): tagName 定位
- findElement(By.xpath()): xpath 定位
- findElement(By.cssSelector()): cssSelector 定位
- switchTo().frame: 切换 iframe 表单

` 定位一组元素，用 findElements 方法`
` findElement 方法定位到的元素有多个，那么该方法只会发返回第一个`
---

- ## 元素操作
- getText(): 获取元素的文本信息，也就是在开始和结束标签之间的内容，该内容可以用于断言我们定位到的元素是不是我们想要的元素
- getTagName(): 获取元素的标签名，该方法也可以用于判断是否定位到了正确的元素
- getAttribute(): 根据元素的属性名获取元素的属性值
- isEnabled(): 判断元素是否可以操作，如 click() 点击 等，返回值为 True 或 False
- isDisplayed(): 判断元素是否在页面上展示
- isSelected(): 选项或者元素是否被选中，在单选或者多选框中常用到
- click(): 适用于任何元素，对其进行点击操作
- send_keys(): 适用于文本区域或者可编辑的元素，可以输入指定内容
- clear(): 适用于文本区域或者可编辑的元素，可以清空文本内容
- submit(): 适用于 Form 表单元素，用于提交数据，Selenium 4 中不再推荐使用此方法，而是推荐直接点检表单的提交按钮
- select: 选择单选或者多选框中的元素