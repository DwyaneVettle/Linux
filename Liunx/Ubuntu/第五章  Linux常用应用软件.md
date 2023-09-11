# 第五章  Linux常用应用软件

​		Ubuntu包含了日常所需的常用程序，集成了跨平台的办公套件LibreOffice和Mozila Firefox浏览器等。还提供了文本处理工具、图片处理工具等。



## 1.LibreOffice

​	LibreOffice免费开源，遵照GPL分发源代码，与OpenOffice相比增加了很多特色功能，支持的文本格式相当全面。

​	LibreOffice的安装实在系统级完成的，这意味着所有用户都可以访问它。在GNOME桌面继承了LibreOffice Writer（类似Word）、LibreOffice Impress（类似PowerPoint）、LibreOffice Cale（类似Excel）、LibreOffice Draw（类似绘图软件）。在系统中搜索LibreOffice将显示系统内置的这4个组件。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625401.png" alt="image-20230905094026205" style="zoom:50%;" />



## 2.vi文本编辑器

​	文本编辑器是对纯文本文件进行编辑、查看、修改等操作的应用程序。Linux下有两种编辑器：一种是基于图形化界面的编辑器，如Gedit；另一种是基于文本界面的编辑器，如vi。vi编辑器是Linux系统中最基本的文本编辑工具，它不仅适用于Linux系统，也适用于UNIX系统。

​	vi是`visual`的缩写。vi编辑器最初是为UNIX系统设计的，1978年由伯克利大学的Bill Joy开发完成。它出色的灵活性和强大的功能使它深受广大Linux用户的喜爱，长期立于不败之地。

​	在Linux中除了vi编辑器之外还有vim编辑器，它是`vi improved`的缩写，即vi编辑器的改进版。vim是一个开放源代码的软件，它在vi的基础上增加了很多新的功能，使用起来更加方便易用。在Ubuntu中使用的是vim，但通常也称为vi。

​	**在vi编辑界面中一共有三种不同的模式：命令模式、插入模式、末行模式。**不同模式下的功能是不同的。

- **命令模式**：启用vi编辑器后会默认进入命令模式。该模式主要完成光标移动、字符串查找、删除、赋值等操作。不论用户处于何种模式下，**只要按下Esc键，即可进入命令模式**。
- **插入模式**：在插入模式下，我们就可以修改文件的内容。**输入字母"i"就可以进入插入模式**。
- **末行模式**：在命令模式下，按下":"键即可进入末行模式。该模式下可以保存文件，退出编辑器，以及对文件内容进行查找、替换等操作。处于末行模式时，编辑器的最后一行会出现":"提示符。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625402.png" alt="image-20230905094934019" style="zoom:50%;" />

### 2.1.命令模式的基本操作

- **光标移动：**在命令模式下可以使用键盘方向键来是实现光标的移动，也可以使用PageUp 和Page Down向上向下翻页，另外还有一些常用的快捷键：

![image-20211118220322454](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655479.png)

- **复制、粘贴、删除：**快捷键如下：

![image-20211118220610301](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655480.png)

- **文件内容查找：**文件内容查找快捷键如下：

![image-20211118220844997](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655481.png)

- **撤销编辑：**撤销编辑快捷键如下：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655482.png" alt="image-20211118221123250" style="zoom:50%;" />

### 2.2.插入模式下的基本操作

​	从命令模式转入到插入模式有3种方法：

- **i :在光标处插入；**

- **a：在光标所在处下一个字符处插入；**

- **o:在光标所在处下方打开一个新行-另起一行。**

  **Esc可以返回至命令模式。**



### 2.3.末行模式下的基本操作

- **保存退出vim编辑器：**

![image-20211118221921606](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655483.png)

- **文件内容的替换 ：**格式如下：

```shell
: [替换范围] s/旧的内容/新的内容/[/g][/c]

# [/g][/c] 表示文件的操作，可有可无
# /g表示对替换范围内每一行所有的匹配结果都进行替换，省略"/g"时只表示替换到匹配结果的第一行
# /c表示每次替换前都要进行询问，要求用户确认
# 替换范围如果用"%"表示在整个文档中进行替换，也可以用"12,23"的形式，表示12-23行间替换
```

```shell
:%  s/ssh/SSH/gc					# 将整个文档中所有的ssh都替换成SSH
```

​	**替换举例：**

![image-20211118222340414](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655484.png)



## 3.Gedit文本编辑器

​	Gedit是个图形化的文本编辑器，其使用方便、直观，可以打开、编辑并保存纯文本文件。它还支持剪切和粘贴文本、创建新文本、打印等功能，是一个方便易用的编辑器软件。它的具体操作和Windows下的记事本十分相似。

​	启动Gedit有两种方式，一种是在系统搜索中直接搜索Gedit打开；还有一种是直接通过Shell命令`gedit`打开。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625403.png" alt="image-20230905100341053" style="zoom:50%;" />

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625404.png" alt="image-20230905100423935" style="zoom:50%;" />



## 4.Shotwell照片管理器

​	Shotwell是Linux下预装的照片管理器，适用于GNOME桌面环境。他是一个方便易用的照片管理工具，支持各种数字照相设备，用户只要连上手机或相机，就能轻松地传输、分享和存储照片。

​	Shotwell的启动也有两种方式：一种是系统搜索；另一种通过Shell命令`shotwell`打开。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625405.png" alt="image-20230905101020254" style="zoom:50%;" />

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309111625406.png" alt="image-20230905101235991" style="zoom:50%;" />

