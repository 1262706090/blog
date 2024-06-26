---
title: "JavaWeb"
date: 2024-06-24T14:57:49+08:00
lastmod: 2024-06-25T14:57:49+08:00
author: ["YK"]

categories:
    - learningNotes

tags:
    - javaWeb

keywords:

description: "javaWeb" # 文章描述，与搜索优化相关
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
summary: "黑马程序员JavaWeb开发教程，实现javaweb企业开发全流程" # 文章简单描述，会展示在主页
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---

# Maven

## 简介

![Maven Overview](./images/maven-overview.png)

Maven 的本质是一个项目管理工具，将项目开发和管理过程抽象成一个项目对象模型（Project Object Model，POM）。

![Maven](./images/maven.png)

## 作用

Maven 是专门用于管理和构建 java 项目得工具，它的主要功能有：

1. 提供了一套标准化的项目结构
   ![standardized Project Structure](./images/standardized-project-structure.png)
2. 提供了一套标准化的构建流程（编译，测试，打包，发布……）
   ![Standardized Build Process](./images/standardized-build-process.png)
3. 提供了一套依赖管理机制
   ![Dependency Management](./images/dependency-management.png)

## 下载与安装

官网：[http://maven.apache.orp/](http://maven.apache.orp/)

## 环境变量配置

在系统变量中配置`MAVEN_HOME`,值为解压目录，然后在`Path`中配置`%MAVEN_HOME%\bin`。

在`cmd`中输入`mvn`命令能够识别，环境变量配置成功。

## 基础概念

### 仓库

私服可以是中央仓库的镜像，解决中央仓库访问慢的问题，也可以存储自己的私有资源，解决版权问题

![Blog](images/blog.png)

### 坐标

1. Maven 中的坐标用于描述仓库中 jar 包的位置
    - [https://repo1.maven.org/maven2/](https://repo1.maven.org/maven2/)
    - Maven Repository：[mvnrepository.com](mvnrepository.com)
2. Maven 坐标组成
    - groupId：定义 Maven 项目隶属组织名称 (通常是域名反写，例如：org.mybaatis)
    - artifactId：定义 Maven 项目名称 (通常是模块名称，例如：CRM、SMS)
    - version：定义项目版本号
3. packaging：定义项目的打包方式 (jar/war)

![Mvnrepository](images/mvnrepository.png)

图中 Maven 框中即为`javafx-controls`的 jar 包坐标

maven 坐标的作用：唯一的定位 jar 资源位置，由 maven 工具自动完成识别和下载

# web
