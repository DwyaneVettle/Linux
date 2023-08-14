# 第二章 Linux系统-系统接口管理

​	操作系统接口时架构在硬件上的第一层软件，时计算机底层硬件和用户之间的接口，利用操作系统才能使用应用程序（或用户）对系统硬件的访问。任何操作系统都会想上层提供接口，操作系统接口是方便用户使用计算机系统的关键。操作系统的接口分为用户接口和程序接口两大类，用户接口又包括命令接口和图形接口。

- **命令接口：**操作系统提供的一组连接命令接口，用户通过输入相关命令，获得操作系统的服务，控制用户程序的执行。
- **图形接口：**通过突变、窗口、菜单等形成直观易懂、使用方便的计算机操作环境，以鼠标驱动的方式使用系统的用户界面。
- **程序接口：**有一组系统调用命令组成的，这些命令可供应用程序使用，使程序员访问系统资源，系统调用是操作系统提供给应用程序访问系统资源的唯一接口，每个系统调用都是一个能完成功能的子程序。



## 1.Shell命令接口

​	Shell是Linux操作系统的最外层，也称为外壳。一方面它可以作为操作系统的命令接口，以交互的方式解释和执行用户输入的命令，或自动解释和执行预先设定好的一连串命令，实现用户与计算机的交互。另一方面，Shell也能用作解释性的编程语言。**Linux下的Shell命令接口由一组命令和命令解释程序Shell组成**。

​	Shell来源于UNIX系统，在UNIX诞生之初，只配有一个命令解释器，它用于解释和执行用户的命令。1979年，贝尔实验室的Bourne开发出第一个Shell程序---B Shell（bsh），20世纪80年代，Bill Joy开发了C Shell（csh）。在此后很长一段时间，人们用B Shell来编程，C Shell来实现交互。后来贝尔实验室的大卫.科恩开发了K Shell，它融合了B Shell和C Shell的特点，广受用户的欢迎。

​	还有一种Shell版本尤为著名，就是Bourne Again Shell（bash）。bash是GNU计划的一部分，用于替代B Shell，它用于基于GNU的Linux系统。常见的Shell版本有：

- bsh：最经典的Shell，每种Linux、UNIX都可用；

- csh：其语法与C语言相似，交互性更好；

- ksh：结合了csh和bsh的优点；

- tcsh：csh的扩展；

- bash：bsh的扩展，结合了csh和ksh的优点；

- zsh：结合了bash、tcsh的许多功能。

  大多数的Linux系统默认使用bash。Linux常用的shell可以通过/etc/shells文件查看：

```shell
cat /etc/shells
```

<img src="C:/Users/HP/Desktop/2023-08-14_213807.png" style="zoom:50%;" />



## 2.GNOME桌面环境

​	1999年，墨西哥程序员Miguel开发了Linux下的桌面GNOME1.0。GNOME是基于GPL的完全开放的软件，可以让用户容易地使用和配置计算机。GNOME遵照GPL许可发行，得到Red Hat等公司的大力支持，成为了众多Linux发行版默认安装的桌面环境，GNOME即GNU网络对象模型环境（GNU Network Object Model Environment）。

​	GNOME的官方网站为：www.gnome.org。Ubuntu20使用了GNOME3.38版本作为默认的桌面环境。在GNOME模式下，桌面主要由3部分组成：状态栏、dock面板（任务栏）、桌面区。

![2023-08-14_220109](C:/Users/HP/Desktop/2023-08-14_220109.png)

