# 第四章  Linux常用命令

## 1.Linux命令

​	要使用命令，必须先启动Shell程序。用户可以通过桌面右键打开终端，或使用`Ctrl+Alt+T`组合启动Shell，当然也可以从左侧dock面板上找到终端图标打开，打开后如下图：

![image-20230828152526654](C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828152526654.png)

​	Shell命令由命令名和多个选项及参数组成，各部分之间用空格分隔，并且Shell命令严格区分大小写。Shell命令的格式如下：

```shell
命令名  [-选项] [参数]
```

​	命令名通常为小写，选项是以“-”作为前缀，“-”代表选项的开始，一个命令可以有多个选项，多个选项时一般组合使用。



## 2.目录操作命令

### 	2.1.ls命令

​	ls命令用于查看某个目录下的所有命令，默认情况下，显示的条目按字母顺序排列。`ls`是`list`的缩写，其格式如下：

```shell
ls [选项] [文件名或目录名]
```

| 选项 | 作用                                                     |
| ---- | -------------------------------------------------------- |
| -s   | 显示每个文件的大小                                       |
| -S   | 按文件的大小排序                                         |
| -a   | 显示目录中的全部文件，包括隐藏文件                       |
| -l   | 使用长列表格式，显示文件详细信息                         |
| -t   | 按文件修改的时间排列显示                                 |
| -F   | 显示文件类型描述符。如，*为可执行的普通文件，/为目录文件 |

​	在使用`ls`命令显示文件及目录的信息时，会发现文件及目录列表中有多种颜色出现。Linux中不同的颜色代表不同的含义。

- 黑色（默认）：普通文件
- 绿色：可执行文件
- 红色：tar包文件，即压缩文件
- 蓝色：目录文件（文件夹）
- 水红色：图像文件
- 青色：链接文件（快捷方式）
- 黄色：设备文件

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828153650593.png" alt="image-20230828153650593" style="zoom:50%;" />

​	由上图我们可以看出，当`ls`命令使用长列表格式显示时，每个目录或文件是以一行的形式显示的，这一行一共分为7个部分：

- **第一部分：**表示文件的类型和权限，共10个字符。其中第一个字符表示该文件类型，共有4种情况："-"表示普通文件，“d”代表目录，“l”代表链接文件，“b”代表设备文件；后面9个字符每3个字符又分为一组，分别表示文件所有者、文件所有者所在的组、其他用户对文件拥有的权限。每组种3个字符代表读、写、执行的权限，所没有该权限则用“-”表示。读为`r`，写为`w`，可执行为`e`；
- **第二部分：**数字，表示当前目录下的目录文件数目。它是隐藏目录数目和普通目录数目之和；
- **第三部分：**表示这个文件所属的用户；
- **第四部分：**表示这个文件属猪的用户组；
- **第五部分：**表示这个文件的大小，以字节为单位；
- **第六部分：**表示这个文件修改的时间；
- **第七部分：**表示文件或目录名及映射关系。



### 2.2.cd命令

​	`cd`是`change directory`的缩写，表示切换路径，语法为：

```shell
cd [路径名]
```

​	它有几个特殊用法，"."代表当前目录，“..”代表上级目录，“~”代表当前用户的宿主目录，“~用户名”表示该用户的宿主目录，“/”表示根目录，“-”表示前一目录，即进入当前目录前操作的目录。

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828155614783.png" alt="image-20230828155614783" style="zoom:50%;" />

### 2.3.pwd命令

​	上图示例中我们使用的`pwd`命令用于显示当前目录的绝对路径。Linux的目录结构复杂，层次相当多，用户很容易混淆所在的目录，造成误删除、误修改的操作，因此使用`pwd`命令能有效的帮助用户清楚目前所在的目录。

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828155921729.png" alt="image-20230828155921729" style="zoom:67%;" />

### 2.4.mkdir命令

​	`mkdir`是`make directory`的缩写，表示创建一个新的目录，语法如下：

```shell
mkdir [选项] 目录名
```

| 选项    | 作用                                           |
| ------- | ---------------------------------------------- |
| -m 权限 | 对新建目录设置存取权限，权限可用数字777，755等 |
| -p      | 一次性建立多级目录，即以递归形式创建目录。     |

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828160414040.png" alt="image-20230828160414040" style="zoom:50%;" />



### 2.5.rmdir命令

​	`rmdir`命令是`remove directory`的缩写，表示删除目录，它和`mkdir`一样也有且只有一个选项`-p`，即递归删除各级空目录。其语法格式如下：

```shell
rmdir [-p] 目录名
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828160956493.png" alt="image-20230828160956493" style="zoom:50%;" />

​	**注意：**我们从上图可发现，如果该目录非空，使用`rmdir`是不能删除的，如果要删除非空目录，可以使用`rm`命令来执行删除。



## 3.文件操作命令

### 3.1.touch命令

​	`touch`命令用来创建文件，如果文件不存在则创建一个新的空文件，且该文件不包含任何格式，大小为0。语法格式如下：

```shell
touch 文件名
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828162619895.png" alt="image-20230828162619895" style="zoom:50%;" />



### 3.2.cat命令

​	`cat`命令是`concatenate（连接）`的缩写，用来显示文件的内容。语法格式如下：

```shell
cat [选项] [文件名]
```

| 选项 | 作用                                                   |
| ---- | ------------------------------------------------------ |
| -A   | 显示所有字符，包括换行符、制表符以及其他非打印字符     |
| -n   | 显示文件行号                                           |
| -b   | 除了空行不编号外，对文件中其他行都进行编号，并显示行号 |
| -s   | 将连续的空行压缩为一个空行                             |

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828163211067.png" alt="image-20230828163211067" style="zoom:50%;" />

​	`cat`命令除了上面最基本的用法外，还有以下几种用法：

- **重复输出输入的内容**：在没有参数的情况下直接输入`cat`命令，会接收用户输入的内容，并且重复显示出来，知道使用`Ctrl+D`退出。

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828164240887.png" alt="image-20230828164240887" style="zoom: 67%;" />

- **重定向创建一个新文件**：使用重定向符号“>”接收用户输入的内容到新创建的文件中，使用`Ctrl+D`可以结束输入，这样可以更快更方便地创建一个有内容地文件，语法如下：

```shell
car > 新文件名
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828164652430.png" alt="image-20230828164652430" style="zoom:50%;" />

- **实现文件地合并**：使用重定向符号“>”也可以快速的将两个文件的内容合并到第三个文件中，语法如下：

```shell
cat 文件名1 文件名2 > 文件名3
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828165034378.png" alt="image-20230828165034378" style="zoom:50%;" />

- **向文件中追加内容**：使用双重定向符号“>>”可以向文件中追加内容，语法如下：

```shell
cat 文件名2 >> 文件名1
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828165233381.png" alt="image-20230828165233381" style="zoom:50%;" />

### 3.3.cp命令

​	`cp`是`copy`的缩写，表示实现文件的复制操作。语法如下：

```shell
cp [-选项] <源文件> <目标文件>
```

| 选项 | 作用                                     |
| ---- | ---------------------------------------- |
| -i   | 选项表示已安全询问的方式进行源文件的复制 |
| -p   | 复制时保留源文件的属性不变               |
| -r   | 复制目录的操作                           |

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828165826152.png" alt="image-20230828165826152" style="zoom:50%;" />

```shell
mkdir /tmp/test								# 创建目录/tmp/test
cp /etc/issue /tmp/test						# 将文件/etc/issue复制到/tmp/test中
ls /tmp/test								# 查看复制后新生成的文件
---------------------
cp -r /home /tmp/test/						# 复制目录的操作，将/home复制到/tmp/test/
---------------------
ls -ld /home/teacher/			
drwx------. 3 teacher teacher 78 10月 29 13:33 /home/teacher/
cp -r /home/teacher/ /tmp/test
ls -ld /tmp/test
drwxr-xr-x. 4 root root 46 10月 29 20:43 /tmp/test
rm -rf /tmp/test/teacher
cp -rp /home/teacher/ /tmp/test
ls -ld /tmp/test/teacher
drwx------. 3 teacher teacher 78 10月 29 13:33 /home/teacher/
```

### 3.4.rm命令

​	`rm`命令`remove`的缩写，作用是删除指定的文件，语法如下：

```shell
rm [选项] [文件名或目录名]
```

| 选项   | 作用                                              |
| ------ | ------------------------------------------------- |
| -i     | 已安全询问的方式执行删除操作                      |
| -r、-R | 递归处理，将指定目录及其子目录中所有文件一一删除  |
| -f     | 强制删除文件或目录                                |
| -v     | 显示命令执行过程                                  |
| -d     | 直接把要删除的目录的硬连接数据修改为0，删除该目录 |

​	`rm`命令可以删除文件，也可以删除目录，同样也可以以安全询问方式删除：

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828171004512.png" alt="image-20230828171004512" style="zoom:50%;" />

​	除了上述操作外，`rm`命令也可以使用通配符来删除目录或文件，也可以指定多个目录或文件删除：

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828171255187.png" alt="image-20230828171255187" style="zoom:50%;" />



### 3.5.mv命令

​	`mv`是`move`的缩写，表示实现文件的移动，类似于Windows中的剪切操作。语法如下：

```shell
mv [选项] 源文件或目录 目标文件或目录
```

​	需要说明的是，如果第二个参数中的目标是一个目录，则mv命令会将源文件移动到该目录中。如果第二个参数中的目标是一个文件，则mv命令会将源文件进行重命名。

​	如果mv移动的是一个目录，并不会和"cp"命令一样加上"-r",而是直接移动。

```shell
例如：将/root/test目录中的文件test1.txt改名为test2.txt
touch /root/test/test1.txt
mv /root/test/test1.txt /root/test/test2.txt
------------------
例如：将/root/test/test2.txt移动到/tmp目录中
mv /root/test/test2.txt /tmp/
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828171835329.png" alt="image-20230828171835329" style="zoom:50%;" />

### 3.6.chmod命令

​	`chmod`是`change modifier`的缩写，它是一个非常重要的命令，用于修改文件的权限和文件的属性。我们之前使用`ls -l`命令查看文件时就发现了第一部分由10个字符组成，表示文件类型和权限，如果要对文件的权限进行修改，就需要利用chmod命令。其语法如下：

```shell
chmod [<文件使用者> +/-/= <权限类型>] 文件名1 文件名2 ...
```

<img src="C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20230828172841114.png" alt="image-20230828172841114" style="zoom:50%;" />	

​	`chmod`命令中的“**[<文件使用者> +/-/= <权限类型>]**”是一个整体，中间不加空格进行分隔。

- **文件的使用者分为4中类型**：
  - "u"：user，文件所有者；
  - "g"：group，文件所有者所在的组；
  - "o"：other，其他用户；
  - "a"：all，所有用户。

- **+/-/=的含义：**
  - "+"：表示增加权限；
  - "-"：表示取消权限；
  - "="：表示赋予指定权限。
- **权限的类型有：**
  - "r"：read，读权限；
  - "w"：write，写权限；
  - "e"：execute，执行权限。

