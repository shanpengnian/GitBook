# Gitbook简介

GitBook 是一个基于 Node.js 的命令行工具，支持 Markdown 和 AsciiDoc 两种语法格式，可以输出 HTML、PDF、eBook 等格式的电子书。GitBook 可以理解为文档格式转换工具。
所以GitBook并不是编辑工具，MarkDown编辑工具可以使用GitBook Editor（整合了git和markdown编辑器）

## 第一步：检查npm

安装Node.js
https://nodejs.org/en/download/ ，在官网下载对应版本（node-v10.3.0）

解压二进制包，解压后可以直接使用

便于使用做一个软连接和设置环境变量

安装教程：https://www.sxpcwlkj.com/016/

推荐用nvm工具进行管理node.js

版本验证:
```
C:\Users\admin>npm -v
6.1.0
```

## 第二步：安装gitbook命令行工具

```
npm install -g gitbook-cli
```
> 如果有报错有可能是nodejs 版本过高 （10.3.0 亲测无误）


## 第三步：初始化

` gitbook init `

> 进入文件夹，执行上面命令 ，执行完后，你会看到多了两个文件 —— README.md 和 SUMMARY.md，它们的作用如下：

> README.md —— 书籍的介绍写在这个文件里
> SUMMARY.md —— 书籍的目录结构在这里配置

## 第四步：编辑SUMMARY.md

```
# 目录

* [简介](README.md)
* [GitBook创建](gitbook/README.md)
* [Markdown语法](markdown/README.md)
* [技术栈](sxpcwlkj/README.md)
    * [项目后端](sxpcwlkj/admin/README.md)
    * [项目前端](sxpcwlkj/ui/README.md)
    * [项目移动端](sxpcwlkj/uniapp/README.md)
```

## 第五步：生成目录

` gitbook init `

GitBook 会查找 SUMMARY.md 文件中描述的目录和文件，如果没有则会将其创建

## 第六步： 本地预览

` gitbook serve ./{book_html} `

启动服务，并生成一个 book_html 的文件夹 里面是html页面

## 第七步：编译

` gitbook build `

当你写得差不多，你可以执行 gitbook build 命令构建书籍，默认将生成的静态网站输出到 _book 目录


## 其他

安装插件

` gitbook install `

扩展文献：https://www.mapull.com/gitbook/comscore/