---
title: 'Windows下Maven安装及配置教程'
copyright: true
date: '2022-06-30 20:51'
tags: 'Maven'
categories: '环境'
---

1. 下载(本文下载的是zip文件)

   官网下载：https://maven.apache.org/download.cgi

   下载完成后解压到指定目录下即可。

2. 配置

   - 配置本地仓库

     默认本地仓库是C盘，修改到指定文件夹下。注意Maven的核心配置文件：`conf/settings.xml`

     打开添加如图如下代码即可

     ![Snipaste_2022-05-13_09-06-50](Windows%E4%B8%8BMaven%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B/Snipaste_2022-05-13_09-06-50.png)

     ```
     <!--配置Maven本地仓库-->
     <localRepository>F:\ProDocument\common\maven-repository</localRepository>
     ```

   - 配置阿里云提供的镜像仓库

     注：Maven默认中央仓库的id 为 central。id是唯一的。因此使用< id>central< /id>覆盖了默认的中央仓库。

     ```
      <mirror>
          <id>nexus-aliyun</id>
          <mirrorOf>central</mirrorOf>
          <name>Nexus aliyun</name>
          <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
     ```

   - 配置java版本
     ```
     <profiles>
         <profile>
         	<id>jdk-1.8</id>
           	<activation>
             	<activeByDefault>true</activeByDefault>
                 <jdk>1.8</jdk>
           	</activation>
           	<properties>   		
                 <maven.compiler.source>1.8</maven.compiler.source>
                 <maven.compiler.target>1.8</maven.compiler.target>
                 <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
          	</properties>
         </profile>
     </profiles>
     ```
   - settings.xml

     ```
      <?xml version="1.0" encoding="UTF-8"?>
     
      <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
     
        <!--配置Maven本地仓库-->
        <localRepository>F:\ProDocument\common\maven-repository</localRepository>
       
        <mirrors>
          <!-- 阿里云镜像 -->
          <mirror>
            <id>nexus-aliyun</id>
            <mirrorOf>*</mirrorOf>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
          </mirror>
        </mirrors>
     
        <profiles>
          <!-- Java版本 -->
          <profile>
          	<id>jdk-1.8</id>
            	<activation>
              	<activeByDefault>true</activeByDefault>
                  <jdk>1.8</jdk>
            	</activation>
            	<properties>   		
                  <maven.compiler.source>1.8</maven.compiler.source>
                  <maven.compiler.target>1.8</maven.compiler.target>
                  <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
           	</properties>
          </profile>
          
        </profiles>
      </settings>
     ```

   - 配置环境变量

     首先Maven是一个用java语言开发的程序，它必须基于JDK来运行，需要通过JAVA_HOME来找到JDK的安装位置。因此需要配置好Java环境。

     其次配置`MAVEN_HOME`中

     ![Snipaste_2022-05-13_09-15-10](Windows%E4%B8%8BMaven%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B/Snipaste_2022-05-13_09-15-10.png)
     
     Path路径下配置%MAVEN_HOME\bin;
     
     ![Snipaste_2022-05-13_09-18-05](Windows%E4%B8%8BMaven%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B/Snipaste_2022-05-13_09-18-05.png)

3. 验证

    cmd 命令行输入`mvn -version`（-v缩写）出现如下情况即验证成功。

    ![Snipaste_2022-05-13_10-23-28](Windows%E4%B8%8BMaven%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B/Snipaste_2022-05-13_10-23-28.png)
    
    ```
    C:\Users\pc>mvn -version
    Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
    Maven home: D:\Environment\apache-maven-3.6.3\bin\..
    Java version: 1.8.0_281, vendor: Oracle Corporation, runtime: D:\Environment\Java\jdk1.8.0_281\jre
    Default locale: zh_CN, platform encoding: GBK
    OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
    ```
