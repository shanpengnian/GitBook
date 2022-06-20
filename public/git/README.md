# Git使用

# 一、注册账号

[Github官网](https://github.com/)：https://github.com/

# 二、创建仓库

注册账号，登录成功之后，选择`“+”`，点击右上角的`New repository`，创建一个新的仓库

# 三、安装Git客户端

Github是服务端，因此，在自己电脑上使用Git需要下载Git客户端
Windows下载链接：https://git-scm.com/download/win

安装时直接Next，在安装时的一些默认选项可以忽略。回到桌面，鼠标右键，出现Git GUI Here和Git Bash Here，则说明安装没有问题


![图片](..\..\assets\images\git\git01.png)

# 四、初始化项目

`git init`

# 五、全局配置

```
git config --global user.name "shanpengnian"
git config --global user.email "shanpengnian@163.com"
```

# 六、生成密钥

```
ssh-keygen -t rsa -C "shanpengnian@163.com"
```

> 代码参数含义：
> -t 指定密钥类型，默认是 rsa ，可以省略。
> -C 设置注释文字，比如邮箱。
> -f 指定密钥文件存储文件名。

按三次回车

```
[root@localhost ~]# ssh-keygen -t rsa       <== 建立密钥对，-t代表类型，有RSA和DSA两种
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):   <==密钥文件默认存放位置，按Enter即可
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase):     <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again:     <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa.    <== 生成的私钥
Your public key has been saved in /root/.ssh/id_rsa.pub.    <== 生成的公钥
The key fingerprint is:
SHA256:K1qy928tkk1FUuzQtlZK+poeS67vIgPvHw9lQ+KNuZ4 root@localhost.localdomain
The key's randomart image is:
+---[RSA 2048]----+
|           +.    |
|          o * .  |
|        . .O +   |
|       . *. *    |
|        S =+     |
|    .    =...    |
|    .oo =+o+     |
|     ==o+B*o.    |
|    oo.=EXO.     |
+----[SHA256]-----+


```
windows生成的秘钥地址：C:\Users\admin\.ssh  上面的代码定义是：/root/.ssh 这个路径下

> id_rsa（私有秘钥）和id_rsa.pub（公有密钥）

# 七、添加密钥到远端

进入.ssh文件夹下，使用记事本打开id_rsa.pub文件，全选所有内容，复制

打开GitHub服务端：https://github.com
点击用户头像，选择Settings，进入到个人信息页面

进入：SSH and GPG keys  选择：SSH keys

任意填写一个标题，粘贴复制的密钥，点击添加SSH密钥即可。（如果弹窗提示输入账户和密码，点击确认）
![图片](..\..\assets\images\git\git02.png)

# 八、验证是否授权成功

`ssh -T git@github.com`

```
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?

```

如果提示输入yes或其他，表示缺少一个文件，输入yes，回车即可

```
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi shanpengnian! You've successfully authenticated, but GitHub does not provide shell access.

```

# 九、初始化本地仓库

I: 在你要提交的目录下, `git init` 
II: 和远程刚创建的仓库连接, `git remote add origin git@github.com:shanpengnian/sxpcwlkj-book.git `
III: push前先将远程repository的修改pull(拉)下来, 避免之前本地仓库和远程仓库不一致, 导致提交出错! `git pull origin master` 

# 十、本地作出修改并提交

作出修改, 如: 修改文件和增加文件(或者文件夹)
+ 将当前目录所有到暂存区
 `git add .`
+ 提交你的文件, 添加消息”第一次提交”  
` git commit -m 'first commit' `
+ 发送你的提交到GitHub  
`git push origin master`
+ 查看git状态 
`git status`

# 十一、获取代码

1. git pull：获取最新代码到本地，并自动合并到当前分支


//查询当前远程的版本

`git remote -v`

//直接拉取并合并最新代码

示例1：拉取远端origin/master分支并合并到当前分支

`git pull origin master`

示例2：拉取远端origin/dev分支并合并到当前分支

`git pull origin dev`


> 分析：不推荐这种方式，因为是直接合并，无法提前处理冲突。


2. git fetch + merge: 获取最新代码到本地，然后手动合并分支

+ 额外建立本地分支

```
//查看当前远程的版本
$ git remote -v 
//获取最新代码到本地临时分支(本地当前分支为[branch]，获取的远端的分支为[origin/branch])
$ git fetch origin master:master1  [示例1：在本地建立master1分支，并下载远端的origin/master分支到master1分支中]
$ git fetch origin dev:dev1[示例1：在本地建立dev1分支，并下载远端的origin/dev分支到dev1分支中]
//查看版本差异
$ git diff master1 [示例1：查看本地master1分支与当前分支的版本差异]
$ git diff dev1    [示例2：查看本地dev1分支与当前分支的版本差异]
//合并最新分支到本地分支
$ git merge master1    [示例1：合并本地分支master1到当前分支]
$ git merge dev1   [示例2：合并本地分支dev1到当前分支]
//删除本地临时分支
$ git branch -D master1    [示例1：删除本地分支master1]
$ git branch -D dev1 [示例1：删除本地分支dev1]
```


> 不推荐这种方式，还需要额外对临时分支进行处理。


+ 不额外建立本地分支

```
//查询当前远程的版本
$ git remote -v
//获取最新代码到本地(本地当前分支为[branch]，获取的远端的分支为[origin/branch])
$ git fetch origin master  [示例1：获取远端的origin/master分支]
$ git fetch origin dev [示例2：获取远端的origin/dev分支]
//查看版本差异
$ git log -p master..origin/master [示例1：查看本地master与远端origin/master的版本差异]
$ git log -p dev..origin/dev   [示例2：查看本地dev与远端origin/dev的版本差异]
//合并最新代码到本地分支
$ git merge origin/master  [示例1：合并远端分支origin/master到当前分支]
$ git merge origin/dev [示例2：合并远端分支origin/dev到当前分支]
```


> 🤞**推荐这种方式**