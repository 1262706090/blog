---
title: "编译原理"
subtitle: ""
date: 2024-08-02T19:25:34+08:00
lastmod: 2024-08-16T19:25:34+08:00
draft: false
author: "YK"
authorLink: ""
license: ""

tags: ["Compiler"]
categories: ["Note"]

featuredImage: ""
featuredImagePreview: ""

summary: "编译原理" # 文章简单描述，会展示在主页

hiddenFromHomePage: false
hiddenFromSearch: false

toc:
    enable: true
    auto: true

mapbox:
share:
    enable: true
comment:
    enable: true

outdatedInfoWarning: true
---

# 1. 概述

**作用：**：从一种语言到另一种语言

![alt text](<images/2024-08-03 101608.png>)

过程：

![alt text](<images/2024-08-03 102043.png>)

![alt text](<images/2024-08-03 102252.png>)

![alt text](<images/2024-08-03 102349.png>)

![alt text](<images/2024-08-03 103207.png>)

![alt text](<images/2024-08-03 103422.png>)

![2024-08-03-11-09-59.png](images/2024-08-03-11-09-59.png)

![2024-08-03-11-11-00.png](images/2024-08-03-11-11-00.png)

![2024-08-03-11-12-00.png](images/2024-08-03-11-12-00.png)

![2024-08-03-11-13-17.png](images/2024-08-03-11-13-17.png)

![2024-08-03-11-13-36.png](images/2024-08-03-11-13-36.png)

# 2. ANTLR 4 词法分析器

环境：win11 + IDEA + ANTLR 插件

## 2.1 使用 ANTLR 4

### 2.1.1 安装 ANTLR 4 插件

IDEA->Settings->Plugins->
![2024-08-04-16-49-43.png](images/2024-08-04-16-49-43.png)

### 2.1.2 编写 ANTLR 4 文件

1. 新建 Maven 项目
   ![2024-08-04-16-52-55.png](images/2024-08-04-16-52-55.png)
2. 在`pom.xml`里中添加 antlr 的依赖项，注意修改自己的 antlr 版本

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>untitled1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>13</maven.compiler.source>
        <maven.compiler.target>13</maven.compiler.target>
    </properties>

    // 配置位置
    <dependencies>
        <dependency>
            <groupId>org.antlr</groupId>
            <artifactId>antlr4-runtime</artifactId>
            <version>4.10.1</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.antlr</groupId>
                <artifactId>antlr4-maven-plugin</artifactId>
                <version>4.10.1</version>
                <executions>
                    <execution>
                        <id>antlr</id>
                        <goals>
                            <goal>antlr4</goal>
                        </goals>
                        <phase>none</phase>
                    </execution>
                </executions>
                <configuration>
                    <outputDirectory>src/test/java</outputDirectory>
                    <listener>true</listener>
                    <treatWarningsAsErrors>true</treatWarningsAsErrors>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```

1. 在 `src/main/java` 新建 `xxxx.g4` 文件，注意要以".g4"结尾
2. 编写代码

```antlr
// 声明语法名称 simpleexpr。语法名称应该与文件名
grammar SimpleExpr;

// 在生成的代码文件的开头插入一些代码
@header {
package simpleexpr;
}

prog : stat* EOF;

stat : expr ';'
     | ID '=' expr ';'
     | 'if' expr ';'
     ;

expr : expr ('*'|'/') expr
     | expr ('+'|'-') expr
     | ID
     | INT
     ;

SEMI : ';' ;
ASSIGN : '=' ;
IF : 'if' ;
MUL : '*' ;
DIV : '/' ;
ADD : '+' ;
SUB : '-' ;

ID : (LETTER | '_') (LETTER | DIGIT | '_')* ;

INT : '0' | [1-9] [0-9]* ;

WS : [ \t\r\n]+ -> skip ;

SL_COMMENT : '//' .*? '\n' -> skip ;
ML_COMMENT : '/*' .*? '*/' -> skip ;

fragment LETTER : [a-zA-Z] ;
fragment DIGIT : [0-9] ;

```

5. 测试代码

光标放到`prog : stat* EOF;`一行，右键测试

![2024-08-04-17-07-37.png](images/2024-08-04-17-07-37.png)

![2024-08-04-17-10-24.png](images/2024-08-04-17-10-24.png)

6. 配置输出路径

右键 xxx.g4 文件，选择 Configure ANTLR…

## 2.2 词法分析

![2024-08-04-17-23-02.png](images/2024-08-04-17-23-02.png)

![2024-08-04-17-24-42.png](images/2024-08-04-17-24-42.png)

![2024-08-04-17-24-55.png](images/2024-08-04-17-24-55.png)

![2024-08-04-17-26-28.png](images/2024-08-04-17-26-28.png)

![2024-08-04-17-28-04.png](images/2024-08-04-17-28-04.png)

**语言是串的集合**

![2024-08-04-17-29-30.png](images/2024-08-04-17-29-30.png)

![2024-08-04-17-31-36.png](images/2024-08-04-17-31-36.png)

# 3. lexer-re-automata

![2024-08-07-20-56-52.png](images/2024-08-07-20-56-52.png)

_RE、NFA、DFA 三者是可以相互转化的，从某种意义上讲，三者是等价的。_

## 3.1 语言

**语言**：语言是字符串构成的集合。

![2024-08-07-21-49-50.png](images/2024-08-07-21-49-50.png)

![2024-08-07-21-50-04.png](images/2024-08-07-21-50-04.png)

![2024-08-07-21-51-32.png](images/2024-08-07-21-51-32.png)

![2024-08-07-21-53-43.png](images/2024-08-07-21-53-43.png)

![2024-08-07-21-55-02.png](images/2024-08-07-21-55-02.png)

## 3.2 正则表达式

![2024-08-07-21-58-37.png](images/2024-08-07-21-58-37.png)

![2024-08-07-21-59-00.png](images/2024-08-07-21-59-00.png)

![2024-08-07-22-02-50.png](images/2024-08-07-22-02-50.png)

![2024-08-07-22-03-17.png](images/2024-08-07-22-03-17.png)

## 3.3 自动机

![2024-08-07-22-04-51.png](images/2024-08-07-22-04-51.png)

_约定：所有没有对应出边的字符默认指向“空状态”_

（非确定性）有穷自动机是一类极其简单的**计算**装置，他可以**识别**（接受/拒绝）$\Sigma$ 上的字符串。

**Definition(接受(Accept))：**<br/>
（非确定性）有穷自动机 $A$ 接受字符串 $x$ ，当且仅当**存在**一条从开始状态 $s_0$ 到**某个**接受状态 $f \in F$ ，标号为 $x$ 的路径。

因此，$A$ 定义了一种语言 $L(A)$ ：它能接受的所有字符串构成的集合。

**Definition(DFA(Deterministic Finite Automaton))**<br/>
确定性有穷自动机 $A$ 是一个五元组 **$A=(\Sigma,S,s_0,\delta,F)$** ：<br/>
(1) 字母表 $\Sigma (\epsilon \notin \Sigma)$<br/>
(2) 有穷的**状态集合** $S$<br/>
(3) **唯一**的初始集合 $S$<br/>
(4) ** 状态转移函数** $\delta$

$$
\delta:S\times\Sigma\rightarrow S
$$

<br/>
(5) 接受状态集合 $F\subseteq S$

![2024-08-16-16-56-12.png](images/2024-08-16-16-56-12.png)

<div style="text-align: center;">
    用 NFA 描述语言，用 DFA 实现词法分析器<br/>
    <span style="color:red">RE ==> NFA ==> DFA ==>词法分析器</span>
</div>

## 3.4 它们之间关系

![2024-08-16-17-05-50.png](images/2024-08-16-17-05-50.png)

### 3.4.1 RE ==> NFA

#### 3.4.1.1 Thompsons 构造法

Thompsons 构造法的基本思想：**按结构归纳**

Definition(正则表达式)

给定字母表 Σ, Σ 上的正则表达式由且仅由以下规则定义：<br/>
(1) ϵ 是正则表达式;<br/>
(2) ∀a ∈ Σ, a 是正则表达式;<br/>
(3) 如果 s 是正则表达式, 则 (s) 是正则表达式;<br/>
(4) 如果 s 与 t 是正则表达式, 则 s|t, st, s∗ 也是正则表达式。<br/>

$N(r)$ 的**性质**以及 $Thompsons$ 构造法**复杂度分析**：

1. $N(r)$ 的开始状态与接受状态均唯一。
2. 开始状态没有入边，接受状态没有出边。
3. $N(r)$ 的状态数 |S| ≤ 2 × |r|。(|r| : r 中运算符与运算分量的总和)
4. 每个状态最多有两个 ϵ-入边与两个 ϵ-出边。
5. ∀a ∈ Σ,每个状态最多有一个 a-入边与一个 a-出边。
