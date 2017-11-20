
---
title: git常用命令(完全学会git的24节课笔记)
date: 2017-11-13 18:23:30
tags: git
author:
  nick: 大左
subtitle: git常用指令总结...
cover: 

---

#### git常用指令

#### 一、git分支提交
###### 1、如果想把本地的某个分支test提交到远程仓库，并作为远程仓库的master分支，或者作为另外一个名叫test的分支，那么可以这么做。


```
$ git push origin test:master
```
> 提交本地test分支作为远程的master分支
$ git push origin test:test              // 提交本地test分支作为远程的test分支

如果想删除远程的分支呢？类似于上面，如果:左边的分支为空，那么将删除:右边的远程的分支。


```
$ git push origin :test
```
>  刚提交到远程的test将被删除，但是本地还会保存的，不用担心

###### 2、展示当前代码仓库地址
```
git remote -v
```

###### 3、如果在commit之后想更改刚才提交的commit信息可以执行
```
git commit --amend -m "新的信息" --author="用户名 <邮箱>"
```

###### 4、 查看当前文档中有哪些文件可以执行（用图形查看模式查看文档）
```
gitk
```

此时右下角的方块里显示两种模式一种是patch模式一种是tree模式

patch： 记录了前后两次commit的差异

tree： 完整显示当前commit上文件内容

查看完文档之后结束图形操作模式，回到git bash执行
```
exit
```
这样下次在启动git bash会自动恢复之前离开的状态

###### 5、git的基本工作原理

先修改文件，之后执行git add命令之后会把文件内容加入git系统的索引，接着执行git commit 指令将文件存入文档库。

##### 二、git配置文件

git有三个不同级别的配置文件，他们有不同的优先权，高优先权的文件设置项会覆盖低优先权文件中相同的设置项。

- 文件中的  .git  子文件中的config文件
拥有最高的优先权。也就是说他的设置会覆盖其他配置文件中相同的设置项，例如在该文件中设置了A = B的话在别的文件中红设置A = C是不生效果的 （只针对当前文档库）


- 登陆账号的   home directory 中的.gitconfig文件
只有在前一个配置文件中没有设置的项，这个配置 文档的设置才会生效


- git程序的安装文件夹中的    etc/gitcofig文件
    只有前两个文件中没有设置的项，在这个配置文件中设置才会生效，这是公共的配置文件，对所有的git文档库都生效。

###### 1、git config指令的使用

查看当前git的设置值用

```
git config -l 

```

该指令会显示配置文件中所有的设置项，先显示优先级最低的设置

也即是前面的第三种文件形式中的设置， 接着是home directory中的最后优先级最高的文件设置。

###### 2、git config配置命令

每次commit中的--author选项的默认配置
```
git config user.name "操作者姓名"

git config user.email "操作者的email"

```

配置在登陆账号home directory中的.gitconfig文件
```
git config --global user.name "操作者姓名"

git config --global user.email "操作者的email"
```

以上配置项还可以写在安装程序中

```
git config --system user.name "姓名"

git config --system user.email "email"
```

> 也就是说git config的选项可以写入任意i一个config配置文件中，--global 表示home directory中的.gitconfig配置文件，-system 表示git中的-etc\gitconfig 配置文件。

如果要删除配置项目则执行

```

git config --unset user.name
```


> git 指令的长短，例如git commit -m 的完整指令是git commit --message= ,而git config -l的完整写法是git config --list


下边这一指令表示自定义长指令
```
git config alias.指令的别名“正式的指令和选项”
```

##### 3、修改默认的文本编辑器和文本对比程序

> 使用背景 ：在commit的时候输入message过长可以使用文本编辑器


程序默认的编辑器是vm编辑器

可以将起换成win自带的记事本命令如下:

```
git config --global core.editor notepad

```

如果想换成其他的编辑器，只要把nodepad换成其他程序的路径，如果路径中有空格可以用单引号或者双信号括起来，并加上启动程序的选项。

```
git config --global core.editor "'c:/program Files (x86) /Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

```

对比文件

```
git diff
```

以下指令是对比文件所用的软件，需要自行配置
```
git difftool
```

##### 三、把文件传入git仓库

。。。未完待续