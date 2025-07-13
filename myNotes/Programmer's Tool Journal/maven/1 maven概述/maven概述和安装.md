# 什么是maven

## 是什么

Apache Maven 是一个项目管理和构建工具，它基于项目对象模型(POM)的概念，通过一小段描述信息来管理项目的构建、报告和文档

官网: http://maven.apache.org/

## 作用

- 标准化的项目结构
- 标准化的构建流程
- 方便的依赖管理

## 基本模型

![null](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736165911509-dd44a477-d3c1-4426-9777-24ecdfc273a6.png)

# 安装与基本配置

## 下载安装

下载链接： https://maven.apache.org/download.cgi
选择版本下载   windows中选择“apache-maven-3.8.4-bin.zip”版本
解压到当前文件夹

配置环境变量
    Maven是免安装版的,直接解压即可.注意:不要放在有空格和中文的路径里.解压后但为了使用方便,我们要把Maven配置到环境变量中.
    配置MAVEN_HOME(略)

![img](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736166363283-8724d816-6477-4ffe-afb0-ab2e18795923.png)
    配置Path(略)  增加%MAVEN_HOME%\bin

![img](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736166377674-12e2fe0c-b641-48a9-823a-5b9a1fabcd80.png)

验证：

![img](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736166415248-94f13107-c8ad-41c6-81fe-47307f32b11f.png)

## 目录结构

![img](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736166462182-f1ec467d-1f4c-4487-8d2c-64d92ac9c0bb.png)

bin:可执行命令文件夹
boot:类加载器(Maven是Java程序,要使用类加载器)
conf:配置文件
lib:Maven的核心程序

## 基本配置

### 配置本地仓库

不配置有默认值，在C盘。但一般自己配置
方法

```plain
修改 conf/settings.xml中的 <localRepository> 为一个指定目录
```

![img](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736166543288-c9f690e0-abb3-47a9-b441-23845830dde0.png)

### 配置阿里云私服

![null](E:\MyMindHive\MyCsNotesWorkSpace\myNotes\Programmer's Tool Journal\maven\1 maven概述\assets\1736165941512-b39d65e2-a666-4693-9a01-af9a585642ba.png)