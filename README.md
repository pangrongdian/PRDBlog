## 更新主题

### 第一种操作

```bash
cd themes
git pull
git submodule update 
cd ../
git push
```

### 第二种操作

```bash
git submodule update --remote  
//可以增加选项为 指定分支名称，不指定的话则默认更新全部子模块

```

## 如果发生错误

### 关于子模块报错问题

- .gitmodule 文件缺失
- 在主项目中提交了子项目的更新，导致找不到仓库 *(可以去github上查看对应hash值仓库)*

```bash
cd "submodule  path"
git fetch "remote branch"
git branch -r
git reset --hard origin/main
```
