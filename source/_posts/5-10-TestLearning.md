---
title: 5.10 TestLearning
date: 2024-05-10 18:29:25
tags: Test
---


## Selenium 环境搭建

1. 下载浏览器驱动（根据浏览器版本）

2. 两种方式使用驱动
> 1. 配置系统环境变量，系统会自动找到配置好的WebDriver
> 2. 在项目中新建Package|directory，使用Java的Path得到路径后，将环境设置进去。
```bash
       // mac用户推荐使用这个，下面的exe后缀就不用写了
        Path path = Path.of("src","drivers","chromedriver.exe");
        System.setProperty("webdriver.chrome.driver",path.toAbsolutePath().toString());
```

3. 新建测试类，使用@Test注解进行测试

```bash
public class Testcase
 {
    public WebDriver webDriver;


    @BeforeClass
    public void  setWebDriver()
    {
        Path path = Path.of("src","drivers","chromedriver.exe");
        System.setProperty("webdriver.chrome.driver",path.toAbsolutePath().toString());
        webDriver = new ChromeDriver();
    }


    @Test
    public void openBaidu()
    {
        webDriver.manage().window().maximize();
        webDriver.get("https://www.baidu.com");
    }


    @AfterClass
    public  void tearDown()
    {
        webDriver.quit();
    }
}

```

*输出：Default Suite Total tests run: 1, Passes: 1, Failures: 0, Skips: 0*

`测试类的代码结构就和上面一样啦`

---

## Selenium 元素定位
`在使用对应属性进行定位的时候必须确保他是唯一的`

1. 通过id进行定位
> `webDriver.findElement(By.id("kw")).sendKeys("pangRongDian");`
> `webDriver.findElement(By.id("su")).click();`

2. 通过name、class进行定位
> `webDriver.findElement(By.name("wd")).sendKeys("use name findElement");`
> `webDriver.findElement(By.className("s_btn")).click();`


3. 通过Xpath进行定位
//*[@属性=""]

> // 表示从任意位置开始匹配
> @ 表示 访问某个元素
> * 表示匹配所有的标签，当然也可以改成其他标签：div、a、h1····

**xpath 还可以增加 text（）=""进行限定查找**
//a[@class='prd' and text()="pangrongdian"]

4. 通过CSS进行定位

li[id="de6"]>a[class="balaba"]
`在这里 > 表示a是li的子元素/下级元素`
*也就是说可以先定义到上级元素在定位到下级元素*

---

## Selenium 模拟键鼠操作

*进行构建前一定要注意啊@Before里面的前置操作都搞定了*

1. 使用Action进行构建行为
`import org.openqa.selenium.interactions.Actions;`
> 1. new Actions对象，传入 webDriver
> 2. 定位元素，action的move方法移动
> 3. 构建完action之后调用perform方法

```bash
 @Test
    public void testAction()
    {

        Actions actions = new Actions(webDriver);
        //By.linkText("更多")适用于链接文本，通常 a标签都有链接
        WebElement moreBtn = webDriver.findElement(By.linkText("更多"));
        actions.moveToElement(moreBtn);
        WebElement mp3Link = webDriver.findElement(By.xpath("//a[@name=\"tj_mp3\"]"));
        actions.moveToElement(mp3Link).click().perform();

    }
```

**模拟鼠标拖拽百度地图**

1. 打开百度地图网站，构建action
> 1. 定位地图元素，移动到地图上
> 2. 鼠标右键，选择开始位置
> 3. 按下鼠标左键不松开，按照偏移量移动
> 4. 然后释放鼠标，点击右键
> 5. 定位结束位置，调用perform方法

```bash
  @Test
    public void  testDrag() throws InterruptedException 
    {
        webDriver.get("https://map.baidu.com");
        WebElement map = webDriver.findElement(By.id("mask"));
        Actions actions = new Actions(webDriver);
        actions.moveToElement(map).contextClick();
        actions.pause(6000);
        WebElement start = webDriver.findElement(By.id("cmitem_start"));
        actions.moveToElement(start).click();
        actions.clickAndHold();
        actions.moveByOffset(200,100);
        actions.release();
        actions.contextClick().pause(6000);
        WebElement end = webDriver.findElement(By.id("cmitem_end"));
        actions.moveToElement(end).click();
        actions.perform();
        Thread.sleep(2000);
    }
```
*一些元素不好定位可以使用  右键->检查*
*由于网路原因，可能会出现WebElement没有加载出来*

操作回顾|操作名
:--|:--|
释放鼠标|release
鼠标右键|contextClick
点击并拖住|clickAndHold
移动到元素上|moveToElement






