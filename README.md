🌍 English | [简体中文](README-zh_CN.md)| [日本語](README-jp_JP.md) | [Українською](README-uk_UA.md)
<br>

<div align="center">
	<a href="https://charmve.github.io/L0CV-web">
		<img src="https://github.com/Charmve/CppMaster/blob/main/src/header.svg" width="50%" alt="Click to see the more details">
	</a>
    <br>
    <p>C++ Master Learning Roadmap</p>
    <p align="center" alt="CircleCI">
      <a href="https://circleci.com/gh/Charmve/CppMaster">
        <img src="https://circleci.com/gh/Charmve/computer-vision-in-action.svg?style=svg" alt="CircleCI" title="CircleCI">
      </a>
      <a href="https://github.com/Charmve/vallox-api/actions">
        <img alt="Actions Status" src="https://github.com/Charmve/CppMaster/workflows/CI/badge.svg">
      </a>
      <a href="https://standardjs.com">
        <img alt="JavaScript Style Guide" src="https://img.shields.io/badge/code_style-standard-brightgreen.svg">
      </a>
      <a href="https://dependabot.com">
        <img alt="Dependabot Status" src="https://api.dependabot.com/badges/status?host=github&repo=danielbayerlein/dashboard">
      </a>
      <a href="https://deploy.now.sh/?repo=https://github.com/danielbayerlein/dashboard">
        <img alt="Deploy to now" src="https://deploy.now.sh/static/button.svg" height="20">
      </a>
    </p>
    <p align="center">
        <a href="https://github.com/Charmve/CppMaster/tree/main/code">Quickstart</a> •
        <a href="https://github.com/Charmve/CppMaster/tree/main/notebooks">Notebook</a> •
        <a href="https://github.com/Charmve/CppMaster/issues">Community</a>  •
        <a href="https://charmve.github.io/CppMaster/">Docs</a> 
    </p>
</div>


----
<b>Note: Please raise an issue for any suggestions, corrections, and feedback.</b>

The goal of this repo is to buid a advanced C++ programing tech stack for a higher salary.

<br>

### Table of Content

- [⭐️ JD Cases](#%EF%B8%8F-jd-cases)
- [➕ C/C++](#-c)
- [📦 STL](#-stl)
- [💻 操作系统](#-操作系统)
- [☁️ 计算机网络](#%EF%B8%8F-计算机网络)
- [💾 数据库](#-数据库)
- [📏 设计模式](#-设计模式)
- [⚙️ 链接装载库](#%EF%B8%8F-编译链接与调试)
- [🐳 容器化技术](#容器化技术)
- [📚 书籍](#-书籍)
- [👍 内推](https://www.nowcoder.com/discuss/786270)
- [👬 贡献者]()
- [📜 License](LICENSE)

----

<br>

## ⭐️ JD Cases

| | | |
|--|--|--|
|![](/src/imgs/C++开发工程师-Momenta.jpg) |![](/src/imgs/C++资深软件工程师-Momenta.jpg) |![](/src/imgs/嵌入式开发工程师-Momenta.jpg) |
|![](/src/imgs/嵌入式软件工程师-百度.jpg) |![](/src/imgs/嵌入式软件开发工程师-蔚来.jpg) |![](/src/imgs/智能驾驶软件开发工程师-蔚来.jpg) |
|![](/src/imgs/高级嵌入式开发工程师-小马智行.jpg) |![](/src/imgs/高精度定位融合-腾讯.jpg) |  |


<br>

## ➕ C++

- [📦 STL](http://c.biancheng.net/stl/)，
- 智能指针
- [shared_ptr](https://blog.csdn.net/shaosunrise/article/details/85228823) 和 unique_ptr
- auto
- iterator 迭代器

<br>

## 高性能优化
- [profiling](https://zhuanlan.zhihu.com/p/362575905)


<br>

## 💻 操作系统
### 操作系统

#### 文件系统

#### I/O
#### [内存管理](https://github.com/Jeloys/HelloWorld/blob/master/操作系统/内存管理问题合集.md)
##### 虚拟内存
##### [共享内存](https://blog.csdn.net/ypt523/article/details/79958188)
#### [进程和线程](https://github.com/Jeloys/HelloWorld/blob/master/操作系统/进程与线程问题合集.md)
##### 多线程/线程池
##### 时间轮转片
##### 并行计算 GPU/NPU 
- [OpenCL & Cuda]()
- 
##### [Socket问题合集](https://github.com/Jeloys/HelloWorld/blob/master/网络/Socket问题合集.md)


### Linux

- [信号 signal()]()
- [常用命令](https://www.jianshu.com/p/73556e1a1236)
- 环境变量
- 动态链接/静态链接
- [正则表达式](https://www.runoob.com/regexp/regexp-metachar.html)
- [目录挂载](https://blog.csdn.net/dear_little_bear/article/details/108474499)

#### [vim](https://www.jianshu.com/p/fbb00627163c)

#### git

#### ⚙️ 编译、链接与调试
- [链接问题合集](https://github.com/Jeloys/HelloWorld/blob/master/操作系统/链接问题合集.md)
  - [C语言调用so动态库的两种方式](https://blog.csdn.net/shaosunrise/article/details/81161064)
- [Cmake](https://www.hahack.com/codes/cmake/) - [Makefile](https://www.jianshu.com/p/442e71755643)，[CMakeLists.txt](https://blog.csdn.net/shaosunrise/article/details/121103842)
  - [跟我一起写Makefile](https://github.com/seisman/how-to-write-makefile)
- [GDB/CGDB](https://www.jianshu.com/p/8d0278ae7e07)
- [gtest](https://blog.csdn.net/linhai1028/article/details/81675724)

##### [Shell/bash](https://www.runoob.com/linux/linux-shell.html)

##### Bootloader

### RTOS/FreeRTOS

### [ROS](http://wiki.ros.org/cn/ROS/Tutorials)

### QNX

### 容器化技术
- [Docker](https://vuepress.mirror.docker-practice.com/)
- K8S

### ARM x86

### Xavier
- [CUDA编程之快速入门](https://www.cnblogs.com/skyfsm/p/9673960.html)

<br>

## ☁️ 计算机网络

### [网络基础问题合集](https://github.com/Jeloys/HelloWorld/blob/master/网络/网络基础问题合集.md)
### [HTTP问题合集](https://github.com/Jeloys/HelloWorld/blob/master/网络/HTTP问题合集.md)

<br>

## 📏 设计模式
- [OOP设计和设计模式](https://blog.csdn.net/weixin_45748233/article/details/106808059)
-

<br>

## 💾 数据库

关系型与非关系型

### [MySQL问题合集.md](https://github.com/Jeloys/HelloWorld/blob/master/数据库/MySQL问题合集.md)
### [MongoDB](https://www.runoob.com/mongodb/mongodb-tutorial.html)

<br>

## CI/CD
### .yaml

<br>

## 📚 书籍

![image](https://user-images.githubusercontent.com/29084184/140617018-db60fcb7-34dd-4657-9b3c-5c2aaddd8c4b.png)

链接:https://github.com/Charmve/PaperWeeklyAI/tree/master/00_GuideBooksPDF(English%2BChinese)

<br><br>

## 职位要求

1. 熟练使用 C/C++ 编程语言，有良好的编码习惯，掌握语言级别的程序性能优化技巧
2. 掌握至少一种脚本语言的使用 python/shell
3. 熟悉编译过程，熟练使用 CMake 编译脚本，熟悉跨平台交叉编译（x86/ARM）
4. 熟悉 GDB 调试、Profiling 工具使用，对于代码和性能优化有经验
5. 了解 GPU/NPU 等并行计算芯片的使用
6. 熟悉常见关系型数据库、非关系型mongoDb、redis、消息队列等组件，并了解其基本原理 
7. 有高并发服务设计和实现经验、对分布式系统，微服务有深刻的了解，有良好的可靠性意识，包括不限于监控，容灾等
8. 有良好的业务抽象能力和业务建模能力


## 参考

[1] interview. https://github.com/huihut/interview

[2] @Jeloys/HelloWorld. https://github.com/Jeloys/HelloWorld
