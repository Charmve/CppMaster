🌍 English | [简体中文](README-zh_CN.md)| [日本語](README-jp_JP.md) | [Українською](README-uk_UA.md)
<br>

<div align="center">
  <!--
	<a href="https://charmve.github.io/L0CV-web">
		<img src="https://github.com/Charmve/CppMaster/blob/main/src/header.svg" width="50%" alt="Click to see the more details">
	</a>
  -->
  <a href="https://charmve.github.io/L0CV-web">
		<img src="src/one-logo.jpg" width="36%" alt="Click to see the more details">
	</a>
    <br>
    <p>C++ Master Learning Roadmap</p>
    <p align="center" alt="CircleCI">
      <a href="">
        <img alt="Actions Status" src="https://github.com/danielbayerlein/dashboard/workflows/CI/badge.svg">
      </a>
      <a href="https://codecov.io/github/richelbilderbeek/travis_qmake_gcc_cpp11_boost_test_gcov?branch=master">
        <img src="https://codecov.io/github/richelbilderbeek/travis_qmake_gcc_cpp11_boost_test_gcov/coverage.svg?branch=master" alt="codecov.io">
      </a>
      <a href="https://google.github.io/styleguide/cppguide.html">
        <img alt="Cpp Style Guide" src="https://img.shields.io/badge/code_style-standard-brightgreen.svg">
      </a>
      <a href="https://confluence.momenta.works/pages/viewpage.action?pageId=157516066">
        <img alt="Docs Released" src="https://img.shields.io/badge/docs-released-green.svg">
      </a>
      <a href="">
        <img alt="Dependencies" src="https://img.shields.io/badge/dependencies-up%20to%20date-red.svg">
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

## Waking-Up
> 大多数人都高估了他们一天能做的事情，但低估了他们一年能做的事情


<br><a href=""><img align="right" alt="Go for it!" src="src/i_magic_box.png" height="260" title="Do what you like, and do it best!"/></a>

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

[Index](#table-of-content)

<br>

## ➕ C++


1、面向对象的三大特性：封装、继承、多态

2、类的访问权限：private、protected、public

3、类的构造函数、析构函数、赋值函数、拷贝函数

4、移动构造函数与拷贝构造函数对比

5、深拷贝与浅拷贝的区别

6、空类有哪些函数？空类的大小？

7、内存分区：全局区、堆区、栈区、常量区、代码区

8、C++与C的区别

9、struct与class的区别

10、struct、union 内存对齐

11、new/delete与malloc/free的区别

12、内存泄露的情况分析

13、sizeof与strlen对比

14、指针与引用的区别

- C语言的指针和引用和c++的有什么区别？

15、野指针产生与避免

16、多态：动态多态、静态多态

17、虚函数实现动态多态的原理、虚函数与纯虚函数的区别

18、继承时，父类的析构函数是否为虚函数？构造函数能不能为虚函数？为什么？

19、静态多态：重写、重载、模板

20、static关键字：修饰局部变量、全局变量、类中成员变量、类中成员函数

- C 语言的关键字static和 C++ 的关键字static有什么区别

21、const关键字：修饰变量、指针、类对象、类中成员函数

22、extern关键字：修饰全局变量

23、volatile关键字：避免编译器指令优化

- 一个参数可以既是const又是volatile吗

24、四种类型转换：static_cast、dynamic_cast、const_cast、reinterpret_cast

25、C++11 部分新特性，比如右值引用、完美转发等

- 什么是右值引用，跟左值又有什么区别？

- 完美转发

26、std::move函数

27、四种智能指针及底层实现：auto_ptr、unique_ptr、shared_ptr、weak_ptr

28、shared_ptr中的循环引用怎么解决？（weak_ptr）

- [shared_ptr](https://blog.csdn.net/shaosunrise/article/details/85228823) 和 unique_ptr


29、vector与list比较

- vector的底层原理
- list的底层原理
- vector中的reserve和resize的区别
- vector中的size和capacity的区别
- vector中erase方法与algorithn中的remove方法区别
- 正确释放vector的内存(clear(), swap(), shrink_to_fit())
- vector迭代器失效的情况
- 什么情况下用vector，什么情况下用list，什么情况下用 deque

30、priority_queue的底层原理

31、STL部分容器的实现原理，如 vector、deque、map、hashmap、set、list

- map与unordered_map对比
- [set\map机制](https://blog.csdn.net/solstice/article/details/8521946)
- map 、set、multiset、multimap的底层原理
- map 、set、multiset、multimap的特点
- 为何map和set的插入删除效率比其他序列容器高
- 为何map和set每次Insert之后，以前保存的iterator不会失效？
- 当数据元素增多时（从 10000 到 20000），map的set的查找速度会怎样变化？
- 为何map和set的插入删除效率比其他序列容器高，而且每次insert 之后，以前保存的iter
- 为何map和set不能像vector一样有个reserve函数来预分配数据?
- set的底层实现实现为什么不用哈希表而使用红黑树？
- hash_map与map的区别？什么时候用hash_map，什么时候用map？

32、set与unordered_set对比

33、STL容器空间配置器

- [📦 STL](http://c.biancheng.net/stl/)，
- STL线程不安全的情况

34、变量的声明和定义有什么区别

35、简述``strcpy``、``sprintf``与``memcpy``的区别

36、请解析`(*(void (*)( ) )0)( )`的含义

37、设置地址为``0x67a9``的整型变量的值为0xaa66

38、简述指针常量与常量指针的区别

39、请你来说一下 C++ 中struct和class的区别

40、简述`#ifdef`、`#else`、`#endif`和`#ifndef`的作用

41、`typedef`和`define`有什么区别

- 写一个 “标准”宏MIN

42、写出int 、bool、 float、指针变量与 “零值”比较的if语句

43、结构体可以直接赋值吗

44、谈谈你对拷贝构造函数和赋值运算符的认识

45、sizeof和strlen的区别

46、关键字 override
- 简述类成员函数的重写、重载和隐藏的区别

47、C++ 自己实现一个String类

48、用两个栈实现一个队列的功能

49、高级数据结构

- 红黑树
- B B+树
- 图

50、编译链接机制、内存布局（memory layout）、对象模型

> 参考书籍：《C++ Primer》（第5版）、《STL源码剖析》、

[Index](#table-of-content)

<br>

## 高性能优化
- 分析工具 gpertool、[profiling](https://zhuanlan.zhihu.com/p/362575905)
- 掌握多线程优化方法，熟悉基本的资源调度方法；

### Xavier
- [CUDA编程之快速入门](https://www.cnblogs.com/skyfsm/p/9673960.html)

## 高性能计算

- CUDA 并行编程模型及常用优化方法，熟悉基于 TensorRT 编程方法；
- 熟练掌握CUDA程序性能分析、问题定位及调试的能力，掌握对应 CUDA 工具的使用；
- 熟悉 PTX/SASS，有编译优化经验；

[Index](#table-of-content)

<br>

## 💻 操作系统

1、进程与线程区别

2、线程同步的方式：互斥锁、自旋锁、读写锁、条件变量

3、互斥锁与自旋锁的底层区别

4、孤儿进程与僵尸进程

5、死锁及避免

6、多线程与多进程比较

7、进程间通信：PIPE、FIFO、消息队列、信号量、共享内存、socket

8、管道与消息队列对比

9、fork进程的底层：读时共享，写时复制

10、线程上下文切换的流程

11、进程上下文切换的流程

12、进程的调度算法

13、阻塞IO与非阻塞IO

14、同步与异步的概念

15、静态链接与动态链接的过程

16、虚拟内存概念（非常重要）

17、MMU地址翻译的具体流程

18、缺页处理过程

19、缺页置换算法：最久未使用算法、先进先出算法、最佳置换算法

> 参考书籍：《Unix环境高级编程》、《Linux多线程服务器端编程》

[Index](#table-of-content)

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

- [信号 signal](https://blog.csdn.net/qq_27085429/article/details/95041443)
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

##### Bootloader/Uboot/buildboot

### RTOS/FreeRTOS

### [ROS](http://wiki.ros.org/cn/ROS/Tutorials)

### [QNX](https://blackberry.qnx.com/en)

[Index](#table-of-content)

### 容器化技术
- [Docker](https://vuepress.mirror.docker-practice.com/)
- K8S

### ARM x86

[Index](#table-of-content)

<br>

### 虚拟化技术
- [Qemu]()
- KVM
- Hypervisor

[Index](#table-of-content)

<br>

### 缓存/并发技术

- [Kafka](https://zhuanlan.zhihu.com/p/446774729)

## ☁️ 计算机网络

#### [网络基础问题合集](https://github.com/Jeloys/HelloWorld/blob/master/网络/网络基础问题合集.md)
#### [HTTP问题合集](https://github.com/Jeloys/HelloWorld/blob/master/网络/HTTP问题合集.md)

[Index](#table-of-content)

<br>

## 网络编程

Linux 下网络编程核心的包括<b>系统编程</b>和<b>网络 IO </b>两个部分：

1、进程间通信方式：信号量、管道、共享内存、socket 等

2、多线程编程：互斥锁、条件变量、读写锁、线程池等

3、五大 IO 模型：同步、异步、阻塞、非阻塞、信号驱动 区别/联系

4、线程池

5、高性能 IO 两种模式：Reactor 和 Proactor（ 但是 Linux 下由于缺少异步 IO 支持，基本没有 Proactor)

6、IO多路复用：select、poll、epoll的区别（非常重要，几乎必问，回答得越底层越好，要会使用）

7、手撕一个最简单的server端服务器（socket、bind、listen、accept这四个API一定要非常熟练）

8、边沿触发与水平触发的区别


> 参考书籍：《Unix网络编程》

[Index](#table-of-content)

<br>

## 📏 设计模式
- [OOP设计和设计模式](https://blog.csdn.net/weixin_45748233/article/details/106808059)
-
[Index](#table-of-content)

<br>

## 💾 数据库

关系型与非关系型

#### [MySQL问题合集.md](https://github.com/Jeloys/HelloWorld/blob/master/数据库/MySQL问题合集.md)
#### [MongoDB](https://www.runoob.com/mongodb/mongodb-tutorial.html)

<br>

[Index](#table-of-content)

## CI/CD
### .yaml

[Index](#table-of-content)

<br>

## 📚 书籍

![image](https://user-images.githubusercontent.com/29084184/140617018-db60fcb7-34dd-4657-9b3c-5c2aaddd8c4b.png)

链接:https://github.com/Charmve/PaperWeeklyAI/tree/master/00_GuideBooksPDF(English%2BChinese)

> 更多免费电子书，<b>公众号：迈微AI研习社</b>回复 ``“电子书”`` ，可免费获取。

[Index](#table-of-content)

<br><br>

## 职位要求
(初级 -> 高级)

1. 熟练使用 C/C++ 编程语言，有良好的编码习惯，掌握语言级别的程序性能优化技巧
2. 掌握至少一种脚本语言的使用 python/shell
3. 熟悉编译过程，熟练使用 CMake 编译脚本，熟悉跨平台交叉编译（x86/ARM）
4. 熟悉 GDB 调试、Profiling 工具使用，对于代码和性能优化有经验
5. 了解 GPU/NPU 等并行计算芯片的使用
6. 熟悉常见关系型数据库、非关系型mongoDb、redis、消息队列等组件，并了解其基本原理 
7. 有高并发服务设计和实现经验、对分布式系统，微服务有深刻的了解，有良好的可靠性意识，包括不限于监控，容灾等
8. 有良好的业务抽象能力和业务建模能力

[Index](#table-of-content)

<br><a href="https://github.com/Charmve/CppMaster#table-of-content"><img align="right" alt="Go for it!" src="https://raw.githubusercontent.com/Charmve/computer-vision-in-action/dd292873828228a753a9bd2de4576dbf8cc3902c/res/ui/footer-rocket.svg" height="220" title="Do what you like, and do it best!"/></a>


## C++ 面经

- [如果你是一个C++面试官，你会问哪些问题？](https://www.zhihu.com/question/451327108/answer/2359217596)
- 我的专栏 [大厂后端/算法面经分类整理](https://blog.csdn.net/charmve/category_9622929.html)
- [华为、美团、微软、字节、阿里、360 、乐鑫科技研发校招编程测试题（四）试题及答案参考](https://blog.csdn.net/charmve/category_9622929.html)
- [竞赛科创 | 电子信息创新设计项目实践](https://blog.csdn.net/charmve/category_9577245.html)
- [计算机视觉实战 | 练手项目，开放源码](https://blog.csdn.net/charmve/category_10595130.html)

## 参考

[1] interview. https://github.com/huihut/interview

[2] @Jeloys/HelloWorld. https://github.com/Jeloys/HelloWorld
