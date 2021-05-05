---
sidebar: auto
---
# QT学习笔记
## Qt概述
### 1. 什么是Qt?

- Qt是一个**跨平台**的C++图形**用户界面应用程序框架**。
- 它是**完全面向对象**的，很容易扩展，并且允许真正的组件编程。
- Qt是纯C++开发的。
- 可以使用脚本语言python，Ruby，Perl等开发基于Qt的程序。
- Qt支持大部分操作系统，如：Windows,Linux,Unix,Andriod,iOS等。
### 2. Qt的历史
- 1991年，由奇趣科技开发
- 1996年进入商业领域，它也是目前流行的Linux桌面环境KDE的基础
- 2008年 奇趣科技被诺基亚公司收购，Qt称为诺基亚旗下的编程语言
- 2012年 Qt又被Digia公司收购
- 2014年4月 跨平台的集成开发环境Qt Creator3.1.0发布，同年5月20日配发了Qt5.3正式版，至此Qt实现了对iOS、Android、WP等各平台的全面支持。
### 3. Qt的优点
- **简单易学**：Qt 封装的很好，几行代码就可以开发出一个简单的客户端，不需要了解 Windows API。
- **跨平台**：跨平台：如果你的程序需要运行在多个平台下，同时又希望降低开发成本，Qt 几乎是必备的。
- **独立安装**：Qt 程序最终会编译为本地代码，不需要其他库的支撑。
- **漂亮的界面**
- **资料丰富**
- **简化了内存回收机制**
- **可以进行嵌入式开发**
### 4. Qt的版本
Qt按照不同的版本发行，分为商业版和开源版
- **商业版**:为商业软件提供开发，他们提供传统商业软件发行版，并且提供在商业有效期内的免费升级和技术支持服务。
- **开源的LGPL版本**：为了开发自有而设计的开放源码软件，它提供了和商业版本同样的功能，在GNU通用公共许可下，它是免费的。


## Qt的运行环境

### 1.Qt的下载
Qt 官网有一个专门的资源下载网站，所有的开发环境和相关工具都可以从这里下载，
具体地址是：http://download.qt.io/


### 2. Qt用到的开发工具


Qt 不是凭空产生的，它是基于现有工具链打造而成的，它所使用的编译器、链接器、调试器等都不是自己的，Qt 官方只是开发了上层工具。



- GNU工具集

  |工具|说明|
  |---|---|
  |gcc|GNU C语言编译器|
  |g++|GNU C++语言编译器|
  |ld|GNU链接器，将目标文件和库文件链接起来，创建可执行程序和动态链接库。|
  |ar|生成静态库.a,可以编辑和管理静态链接库|
  |make|生成器，可以根据makefile文件自动编译链接生成可执行程序或库文件|
  |gbd|调试器，用于调试可执行程序|





- Qt工具集
  |工具|说明|
  |---|---|
  |qmake|核心的项目构建工具，可以生成跨平台的 .pro 项目文件，并能依据不同操作系统和编译工具生成相应的 Makefile，用于构建可执行程序或链接库|
  |uic|User Interface Compiler，用户界面编译器，Qt 使用 XML 语法格式的 .ui 文件定义用户界面，uic 根据 .ui 文件生成用于创建用户界面的 C++ 代码头文件，比如 ui_*****.h 
  |moc|Meta-Object Compiler，元对象编译器，moc 处理 C++ 头文件的类定义里面的 Q_OBJECT 宏，它会生成源代码文件，比如 moc_*****.cpp ，其中包含相应类的元对象代码，元对象代码主要用于实现 Qt 信号/槽机制、运行时类型定义、动态属性系统|
  |rcc|Resource Compiler，资源文件编译器，负责在项目构建过程中编译 .qrc 资源文件，将资源嵌入到最终的 Qt 程序里|
  |qt creator|集成开发环境，包含项目生成管理、代码编辑、图形界面可视化编辑、 编译生成、程序调试、上下文帮助、版本控制系统集成等众多功能， 还支持手机和嵌入式设备的程序生成部署|
  |assistant|Qt 助手，帮助文档浏览查询工具，Qt 库所有模块和开发工具的帮助文档、示例代码等都可以检索到，是 Qt 开发必备神器，也可用于自学 Qt|
  |designer|Qt 设计师，专门用于可视化编辑图形用户界面（所见即所得），生成 .ui 文件用于 Qt 项目|



### 3. Qt程序开发流程
  1. 创建工程目录
   - mkdir ProjectName
   - 每个Qt程序都要放在一个独立的工程目录下 
  2. 进入工程目录编写源代码
   - vi main.cpp
   - Qt中使用的是C++语言的语法，但Qt的类库不再是标准C++库
  3. 构建工程
   - qmake -project
   - 会生成工程文件 ProjectName.pro
   - 在 .pro 文件中添加构建选项，QT += widgets
  4. 创建Makefile
   - qmake
   - 根据工程文件自动生成Makefile
  5. 编译连接
   - make
   - 完成编译和链接
  6. 测试执行
   - ./ProjectName



## 信号和槽机制
### 1. 什么是信号和槽
- 实现对象之间的数据交互。
- 信号(Signal):在特定情况下被发射的事件。
- 槽(Slot):对信号响应的函数。槽就是一个函数，可以定义在类的任何部分，可以具有任何参数，也可以被直接调用。
- 槽函数与一般的函数不同的是：槽函数可以与一个信号关联，当信号被发射时，关联的槽函数被自动执行。


### 2.信号的定义
```cpp
class XX::public QObject
{
    Q_OBJECT
signals:
    void signal_func(...);
};
```
- 信号函数只需声明，不能写定义
- Q_OBJECT对应于moc(元对象编译器)，将QT语法转换为标准C++语法编译。


### 3.槽的定义
```cpp
class XX::public QObject{
    Q_OBJECT
public slots:
    void slot_func(...){...}//槽函数
};
```
- 槽函数可以连接到某个信号上，当信号被发射时，槽函数将被触发和执行，
- 另外槽函数也可当做普通的成员函数直接调用。


### 4.信号和槽的连接
```cpp
//函数原型
QObject::connect(const QObject* sender,const char* signal,
const QObject*receiver,const char* method);

//基本格式
QObject::connect(sender, SIGNAL(signal()), receiver, SLOT(slot()));
/*
参数：
    sender:信号发送指针(对象)
    signal:要发送的信号函数，可以使用"SIGNAL()"宏进行类型转换
    receiver:信号的接收指针
    method:接受信号后要执行的槽函数，可以使用"SLOT()"宏进行类型转换
*/
```
- SIGNAL 和 SLOT 是 Qt 的宏，用于指明信号和槽，并将它们的参数转换为相应的字符串。


### 5.信号函数和槽函数的选择
- 信号和槽都可以继承
- Qt中的组件都带有Qt类库自带的信号和槽函数，可以直接调用
- 可以自定义槽函数和信号

### 6. 信号和槽连接的语法要求
- 槽函数的参数从信号函数来获取
    ```cpp
    //一般情况下：信号和槽参数要一致（参数个数/数据类型）
    QObject::connect(A,SIGNAL(sigfun(int)),B,SLOT(slotfun(int)));    //ok
    QObhect::connect(A,SIGNAL(sigfun(int)),B,SLOT(slotfun(int,int)));   //error

    //例外的两种情况
    //一、带有缺省参数
    QObject::connect(A,SIGNAL(sigfun(int)),B,SLOT(slotfun(int,int=0)));     //  ok,槽函数参数带有缺省值
    //二、信号函数的参数可以多于槽函数，多余参数将被忽略
    QObject::connect(A,SIGNAL(sigfun(int,int)),B,SLOT(slotfun(int)));   //多余的    信号参数被忽略掉
    ```
### 7.信号和槽连接的应用
- 一个信号可以被连接到多个槽（一对多）:一个信号触发多个槽函数。但是，执行顺序不确定，执行顺序由系统决定。
- 多个信号也可以连接到同一个槽（多对一）：多个信号同时触发时，槽函数执行多次。
- 两个信号可以直接连接（信号级联）：
  ```cpp
  //一对多
  QObject::connect(A,SIGNAL(sigfun(int)),B1,SLOT(slotfun1(int)));
  QObject::connect(A,SIGNAL(sigfun(int)),B2,SLOT(slotfun2(int)));
  //多对一
  QObject::connect(A1,SIGNAL(sigfun1(int)),B,SLOT(slotfun(int)));
  QObject::connect(A2,SIGNAL(sigfun2(int)),B,SLOT(slotfun(int)));
  //信号级联
  QObject::connect(A1,SIGNAL(sigfun1(int)),A2,SIGNAL(sigfun2(int)));
  ```

