---
title: 5.12 TestLearning
date: 2024-05-12 10:10:56
tags: Test
---

## Selenium 切换窗口

1. 定位网页，获取当前窗口
`webDriver.getWindowHandle()`
2. 获取所有窗口
`webDriver.getWindowHandles()`
3. 遍历所有窗口，切换窗口

```bash
  @Test
    public  void testWindowsChange()
    {
        webDriver.findElement(By.linkText("图片")).click();
        String currentWindow = webDriver.getWindowHandle();
        Set<String> windows = webDriver.getWindowHandles();

        for (String window : windows) {
            if (window != currentWindow){
                webDriver.switchTo().window(window);

            }
        }

        webDriver.findElement(By.name("word")).sendKeys("selenium");
        webDriver.switchTo().window(currentWindow);
        webDriver.findElement(By.id("kw")).sendKeys("selenium");
    }
```

---

## Selenium iframe界面切换

`iframe 本质上就是一个内嵌网页`
`我们切换到iframe上之后，就无法对iframe以外的元素进行操作，如果需要，我们需要退出iframe`

1. 页面中首先要定位到iframe界面

2. 切换到iframe界面

>

```bash
  @Test
    public void testIframe()
    {
        webDriver.get("https://login.anjuke.com/login/form?history=aHR0cHM6Ly9kYWxpYW4uYW5qdWtlLmNvbS8=");
        WebElement iframe=webDriver.findElement(By.id("iframeLoginIfm"));
        webDriver.switchTo().frame(iframe);
        webDriver.findElement(By.id("phoneIpt")).sendKeys("1234567890");
    }

```

**Selenium 切换iframe页面的方式有三种**

1. 索引（适用于只有一个iframe的情况）
`  driver.switchTo.frame(0)   `

2. name属性（需要找到切换的iframe）
`  driver.switch_to.frame("iframe的name属性")   `

3. webElement 对象切换
`先通过findElement找到webElement对象才能切换`
`   driver.switchTo().frame(iframe);    `

--- 

## Selenium 等待时间

`隐式等待`

(无条件等待，在一个时间段内等待)

- 一次设置，全局生效。不要当作固定等待使用，不要每次需要等待时都写一次隐式等待。
- 隐式等待设置了一个最长等待时间，在规定时间内网页加载完成，则执行下一步，否则一直等到时间结束，然后执行下一步。

`如果是只需等待页面中的一个元素加载就用显示等待，等待整个网页加载就用隐式等待。`

 ```bash
 webDriver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
 
 
 ```

`显式等待`
(有条件等待，判断等待的元素是否加载出来)
```bash
WebElement foo = new WebDriverWait(driver, Duration.ofSeconds(3))
          .until(driver -> driver.findElement(By.name("q")));
```