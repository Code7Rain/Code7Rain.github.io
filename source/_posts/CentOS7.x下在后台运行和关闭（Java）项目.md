---
title: 'CentOS7.x下在后台运行和关闭（Java）项目'
copyright: true
date: '2022-11-12 19:10'
tags: '运维'
categories: 'categories'
---

## 需求

在一般情况下，在服务器通过 java -jar xxx.jar 来运行一个jar包。但是如果退出了控制台，那么这个程序就将被关闭。因此让jar包后台运行十分必要。


## 解决方案

### 运行

方式一：

```
java -jar xx.jar & 
```
&代表在后台运行

方式二：

nohup java -jar xx.jar &

方式三(推荐):

```
nohup java -jar xxx.jar  >log.file  2>&1 &
```

上面的意思如下:

- 0    标准输入（一般是键盘）
- 1    标准输出（一般是显示屏，是用户终端控制台）
- 2    标准错误（错误信息输出）
- `>log.file` 将运行的jar 错误日志信息输出到log.file文件中来,如果不指定，默认该项目所有输出被重定向到nohup.out的文件中。可查看运行的日志文件，查看jar包启动有没有报错
- `2>&1`就是表示将错误重定向输出到标准输出上
- 最后一个&,表示在后台运行。


推荐后两种方式，因为前者是直接后台运行jar包，并没有进入到java的dos窗口。
但假如我们的java程序需要我们进入到它的dos窗口，输入一些参数来运行的话，前两种是不可取的。因为可以在运行jar包后进入java的dos窗口来输入一些程序需要的参数，随后退出dos窗口让其在后台运行。


### 关闭后台运行的Java jar包项目

方法一

直接杀死进程（根据端口）
```
sudo fuser -k -n tcp 8888
```
方法二

根据pid 停止运行

1.查看进程命令为
```
ps aux|grep myblog-0.0.1-SNAPSHOT.jar
```
2.将会看到此jar的进程信息
```
root      9150  0.0  0.0 112708  1012 pts/1    S+   19:05   0:00 grep --color=auto blog-api-0.0.1-SNAPSHOT.jar
```
3.其中9150则为此jar的pid，杀掉命令为
```
kill -9 9150
```
