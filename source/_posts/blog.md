---
title: 博客的自动化部署发布
date: 2021-01-03
tags:
    - CI
---
# 利用 hexo 创建一个博客网站
  可以参观 [我的博客](https://justsuccess.github.io),完全免费创建，不要998，不要88 ，完全免费，完全免费...
  下面我介绍一下这个过程
## 1、首先有个gitHub 的账号
 没有的小伙伴赶紧到 [gitHub官网](https://github.com/) 注册一个
 新建一个工程，
  点号 前面的名字一定是你gitHub 的用户名，例如的我用户名是 [justsuccess](https://github.com/justsuccess),创建的工程名字就是 justsuccess.github.io 
## 2、用HEXO 创建本地博客
### 准备环境
##### 1. Node（建议使用12以上的版本）
##### 2. Git
把公钥ssh放到github 的官网 setting >> SSH and GPG keys (不放也是可以的，后面将博客发布到服务器的时候比较麻烦)
### 安装 Hexo 
 ```node
    npm install -g hexo-cli
 ```
 找一个废弃不用的文件夹
 ```node
    hexo init <folder>
    cd <folder>
    npm install
 ```
 建立本地文件夹与gitHub 仓库的联系
```
    git init // 初始化本地
    git remote add origen git@github.com:<gitHub Name>/<gitHub Name>.github.io.git
```
 ##### 搭建本地服务器
```node
    npm install hexo-server --save
```
安装完成之后 输入一下命令启动服务器，默认地址是 *http://localhost:4000* Hexo 是热更新，文件变化无需重新启动
```node
    hexo s // s 是 server 的缩写
```
如果想更改端口 可以 使用 -p 指定其他端口
```
    hexo s -p 5000
```
### 发布到gitHub
github 虽然也可以读取到md 文件，但也只能读取到maskdown 文件，不能跳转 连接 等等，我们需要将maskdown 转换成html 文件，这时候我们就要用Hexo 的转换功能
```
    hexo g // g 是 generate 的简写
```
可以监视文件变化 至少官网是这么说的，实践中发现不写-w 也是可以的

```
    hexo g -w // -w 是 --watch 的缩写
```

#### 安装 hexo-deployer-git
这是一个发包工具
```
    npm i hexo-deployer-git --save
```
#### 编辑器打开 _config.yml
  网站中的[配置](https://hexo.io/zh-cn/docs/configuration)信息，可以在此配置修改大部分参数

修改配置信息
```
    auther: <gitHub Name>
···
    // 这将是你的博客地址
    url: <gitHub Name>.github.io
...
    deploy:
        type: git
        repo:  https://github.com/<gitHub Name>/<gitHub Name>.github.io.git // github 地址
        branch: master // 分支
```
在public 文件夹下生成站点文件，并将此文件推送到远端服务器改分支下
```
    hexo clean && hexo d // deploy
```
过一会儿 用浏览器访问 <gitHub Name>.github.io 就可以访问到你自己的博客了
 关注我，下一期 持续发布博客的流程
##### 以上全是废话
详细的建站流程参照 [Hexo官网](https://hexo.io/zh-cn/docs) 里面有详细的教程