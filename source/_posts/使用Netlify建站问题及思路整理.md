---
title: 使用Netlify建站问题及思路整理
date: 2024-04-21 18:34:58
tags: 问题及思路整理
---

# NetLify建站需要注意的问题
1.首先要有自己的Github账户
2.注意 *.gitmodules* 文件的使用（**很重要**）
3.域名解析一定要在第三方网站设置好二级域名
4.使用cloudFlare的CDN加速千万不要得瑟
5.更换主题的同时要更新子模块

---

*以上为**Netlify+Hexo**搭建个人博客网站的问题总结*

--- 

# NetLify建站的思路整理

## Hexo的安装
### 1.全局安装、区域安装 Hexo
*（暂时还不知道有什么太大的区别）*
```bash

$ npm install hexo -g

```  
### 2.Hexo初始化及使用

*（简单来说就是初始化项目、创建文档、启动服务、清空缓存、项目渲染、）*
> *初始化项目*

``` bash
$ hexo init "Project Name" 
```
> *创建文档*

```bash
$ hexo new "Article Name"
```
>*启动服务

``` bash
$ hexo server
```
>*清空缓存*

```bash
$ hexo clean
```
>*项目渲染*

```bash
$ hexo generate
$ hexo deploy
```
---
### 3.Hexo更换主题，修改配置文件

- *没什么说的就是在根目录下新建了个theme文件夹，在配置文件中找到theme配置项，更改新下载的主题*

> *（如果你真的这样做了会在时序集成的时候埋雷）* 

- *至于配置文件暂时没有什么太大的探索，主要就是配置项不能什么都不填，最起码填个 __' '__ 不然会报错*

## Hexo与Nelify建站准备

### 1.账号注册

- 域名注册，Nelify注册，Cloudfare注册，Github注册
> *（如果有当我没说）<br>特别注意需要 __魔法__ 才能注册,当然也可以使用gitee *

### 2.建站流程
- 1. 在GIthub上创建两个仓库，*一个作为写文章*，*一个作为存放主题*。
- 2. 本地新建Hexo项目，初始化**Git**，并添加远程仓库<br>*(创建仓库别名，方便后续辨别)*<br>
按照自己需求修改项目配置文件

```bash
$ git init 
$ git add . / git add <filename>
$ git commit -m "Message"
$ git remote add Alias "Remote Repository Url"
// 这里最好使用 ssh 他比较稳定，但然还需要配置密钥
$ git push --set-upstream Alias main
// main 是分支，不知道当前分支，用git branch 查看
```
- 3. 选择喜欢的主题，下载到本地，同样按照上面一样初始化仓库，作为主题的存放。
>**（在这里如果出现，触发Github的安全扫描了，点击他返回的url进行授权就可以了）**

- 4. 域名映射，在域名控制台，设置域名映射，规则可以自定义，*（控制台会有提示）*，一般来说**@**规则是就可以直接通过域名访问到。

- 5. Netlify建站，在网站注册完后，授权GitHub仓库，按照默认流程走完就行。<br>
*（构建命令最好自定义一个，这样方便我们构建）
```bash
"netlify": "npm run clean && npm run build"
```
- 6. 设置CNAME域名映射，CDN加速，用CloudFare，填入我们在NetLify中定义的域名，这样国内就可以访问到。<br>
还有在域名控制台，替换cdn服务器为cloudfare提供的。

- 7. 最后在Nelify中找到Domain management 中完成SSL证书的配置。*（这样可以使用https进行访问）*

**好的到这里<br>可以拉风地使用帅气的域名进行访问啦**

## 深刻斗争过的问题

- 最开始如果只是简单地下载主题进行使用，那就会报错
> 提示你找不到子模块，子模块是什么呢--（.gitmodules）
> 这个配置文件，是构建的时候会自动拉取的。如果是只是下载克隆，他就用不了

>ps:解决办法如下
>先手动添加上 *（.gitmodules）*文件
```bash
[submodule "themes/hexo-theme-matery"]
	path = themes/hexo-theme-matery
	url = https://github.com/pangrongdian/PrdBlogTheme.git
```
 ```bash
    $git submodule update --init --recursive
    $git submodule add --depth=1 "theme Repository Url"  themes/hexo-theme-matery
  ```
>如果这里不用自己的theme Repository *(开始的时候创建过)*，那无论怎么修改配置文件都不会在网站上起作用。！！！

- Netfily构建的时候，如果有大的更新一定要，在 构建选项中清楚缓存,不然会一直使用之前的构建，就看不到新的效果。
> Deploy->Option->Clear cache and retry with latest branch commit

--- 
到这里搭建个人博客就告一段落啦。也要开始自我探索。

# 结语
临近大学的尾声，才堪堪入门，专业所学。如此长时间患得患失，得知不均，也终于在试错中回到心中。<br>
也是到如今，才明白，**"故余虽愚卒或有所闻"**这求学中所释然的轻快。<br>

而我们终将走向未来，也不必与当下执着，所谓君子不争，是以行制性，修身。君子不救，是以律制心，养德。正念起身，我所无他，唯行是先。

**谨以 今日所事 重勉身心 奋勇向前**

   



