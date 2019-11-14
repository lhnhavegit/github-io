---
layout: post
categories:
  - ACM
  - Template
tags: MAVEN
date: 2019-10-17 14:10:33
---
## MAVEN将外部jar打包至Maven仓库

### Maven install命令理解
```text
每一个构建都需要唯一的坐标来标识位置，我们根据坐标位置就能够下载构建至本地仓库。那么如果我们是内部项目，自定义的构建并不公开至网络上，项目成员又想依赖他怎么办呢？想想maven找寻构建的步骤。 
先找寻本地仓库，本地仓库不存在，找寻远程仓库或者私服。 
我们只需把自定义的构建安装至私服或者本地仓库中就行了。这就需要maven的install命令。
```
### install
```text
把自定义的maven项目，安装至本地仓库。
```
### 图示
项目坐标如下
```yml
    <groupId>com.zzq.maven</groupId>
    <artifactId>maven-model</artifactId>
    <version>0.0.1SNAPSHOT</version>   
```
命令
切换至jar目录，然后打开cmd打开命令行，输入以下命令(将对应参数改成自己jar的参数)：
```text
mvn install:install-file -Dfile=icbc-api-sdk-cop-1.0.jar -DgroupId=com.icbc -DartifactId=icbc-api-sdk-cop -Dversion=1.0 -Dpackaging=jar
```

