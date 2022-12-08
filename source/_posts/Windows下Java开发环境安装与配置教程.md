---
title: 'Windows下Java开发环境安装与配置教程'
copyright: true
date: '2022-06-29 19:35'
tags: 'Java'
categories: '环境'
---

1. 下载安装包

   https://www.oracle.com/java/technologies/downloads/

2. 双击exe文件进入安装

3. 选择指定目录安装jdk

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193030780-141851887.png)

4. 选择指定目录安装jre

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193051710-860567096.png)

5. 安装完成

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193111863-1620087635.png)

6. 配置环境变量

   - 我的电脑右击，再点击属性找到高级系统设置，再点击环境变量进行配置。

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193139564-1366743433.png)

   - 配置
      ```
           变量名：JAVA_HOME
           变量值：D:\Environment\Java\jdk1.8.0_281   // 要根据自己的实际路径配置
      
           变量名：Path
           变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
      ```
      ![](Windows下Java开发环境安装与配置教程/2291368-20220629193204294-338728882.png)


7. 测试

   windows键+R键，键入cmd；

   键入命令: java -version、java、javac 几个命令，出现以下信息，说明环境变量配置成功；

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193230336-1133392836.png)

   ![](Windows下Java开发环境安装与配置教程/2291368-20220629193243736-1465458166.png)
