# 第四章  Linux常用命令

## 1.Linux命令

​	要使用命令，必须先启动Shell程序。用户可以通过桌面右键打开终端，或使用`Ctrl+Alt+T`组合启动Shell，当然也可以从左侧dock面板上找到终端图标打开，打开后如下图：

![image-20230828152526654](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022314.png)

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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022315.png" alt="image-20230828153650593" style="zoom:50%;" />

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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022316.png" alt="image-20230828155614783" style="zoom:50%;" />

### 2.3.pwd命令

​	上图示例中我们使用的`pwd`命令用于显示当前目录的绝对路径。Linux的目录结构复杂，层次相当多，用户很容易混淆所在的目录，造成误删除、误修改的操作，因此使用`pwd`命令能有效的帮助用户清楚目前所在的目录。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022318.png" alt="image-20230828155921729" style="zoom:67%;" />

### 2.4.mkdir命令

​	`mkdir`是`make directory`的缩写，表示创建一个新的目录，语法如下：

```shell
mkdir [选项] 目录名
```

| 选项    | 作用                                           |
| ------- | ---------------------------------------------- |
| -m 权限 | 对新建目录设置存取权限，权限可用数字777，755等 |
| -p      | 一次性建立多级目录，即以递归形式创建目录。     |

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022319.png" alt="image-20230828160414040" style="zoom:50%;" />



### 2.5.rmdir命令

​	`rmdir`命令是`remove directory`的缩写，表示删除目录，它和`mkdir`一样也有且只有一个选项`-p`，即递归删除各级空目录。其语法格式如下：

```shell
rmdir [-p] 目录名
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022320.png" alt="image-20230828160956493" style="zoom:50%;" />

​	**注意：**我们从上图可发现，如果该目录非空，使用`rmdir`是不能删除的，如果要删除非空目录，可以使用`rm`命令来执行删除。



## 3.文件操作命令

### 3.1.touch命令

​	`touch`命令用来创建文件，如果文件不存在则创建一个新的空文件，且该文件不包含任何格式，大小为0。语法格式如下：

```shell
touch 文件名
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022321.png" alt="image-20230828162619895" style="zoom:50%;" />



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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022322.png" alt="image-20230828163211067" style="zoom:50%;" />

​	`cat`命令除了上面最基本的用法外，还有以下几种用法：

- **重复输出输入的内容**：在没有参数的情况下直接输入`cat`命令，会接收用户输入的内容，并且重复显示出来，知道使用`Ctrl+D`退出。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022324.png" alt="image-20230828164240887" style="zoom: 67%;" />

- **重定向创建一个新文件**：使用重定向符号“>”接收用户输入的内容到新创建的文件中，使用`Ctrl+D`可以结束输入，这样可以更快更方便地创建一个有内容地文件，语法如下：

```shell
car > 新文件名
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022325.png" alt="image-20230828164652430" style="zoom:50%;" />

- **实现文件地合并**：使用重定向符号“>”也可以快速的将两个文件的内容合并到第三个文件中，语法如下：

```shell
cat 文件名1 文件名2 > 文件名3
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022326.png" alt="image-20230828165034378" style="zoom:50%;" />

- **向文件中追加内容**：使用双重定向符号“>>”可以向文件中追加内容，语法如下：

```shell
cat 文件名2 >> 文件名1
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022327.png" alt="image-20230828165233381" style="zoom:50%;" />

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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022328.png" alt="image-20230828165826152" style="zoom:50%;" />

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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022329.png" alt="image-20230828171004512" style="zoom:50%;" />

​	除了上述操作外，`rm`命令也可以使用通配符来删除目录或文件，也可以指定多个目录或文件删除：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022330.png" alt="image-20230828171255187" style="zoom:50%;" />



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

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022331.png" alt="image-20230828171835329" style="zoom:50%;" />

### 3.6.chmod命令

​	`chmod`是`change modifier`的缩写，它是一个非常重要的命令，用于修改文件的权限和文件的属性。我们之前使用`ls -l`命令查看文件时就发现了第一部分由10个字符组成，表示文件类型和权限，如果要对文件的权限进行修改，就需要利用chmod命令。其语法如下：

```shell
chmod [<文件使用者> +/-/= <权限类型>] 文件名1 文件名2 ...
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301022332.png" alt="image-20230828172841114" style="zoom:50%;" />	

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



`chmod`命令中的选项及作用：

| 选项  | 作用                       | 选项  | 作用                       |
| ----- | -------------------------- | ----- | -------------------------- |
| a+rw  | 为所有用户增加读、写权限   | o-rwx | 取消其他用户的所有权限     |
| a-rwx | 取消所有用户读写执行的权限 | ug+r  | 为所有者和组用户增加读权限 |
| g+w   | 为组用户增加写权限         | g=rx  | 只允许组用户读、执行       |

**示例：**

1. 用`ll`命令查看`test.txt`文件权限；
2. 对该文件取消所有用户读写权限；
3. 为文件所有者添加读、写、执行权限；
4. 为组用户增加读、写权限；
5. 为其他用户增加读权限。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041452828.png" alt="image-20230904145230610" style="zoom:33%;" />

​	另外，也可以用数字来表示权限。其中**4表示读权限，2表示写权限，1表示执行权限，0表示没有权限**。如`rwx`权限用数字表示为4+2+1=7，`rx`权限用数字表示为2+1=3。语法格式如下：

```shell
chmod [mode数字] 文件名	
```

- `mode数字：`由3个0~7的八进制数值组成，分别代表`user、group、other`的权限。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041457276.png" alt="image-20230904145745181" style="zoom:50%;" />

## 4.文件处理命令

### 4.1.grep命令

​	**`grep`命令用于在文本文件中查找并显示包含指定字符串的所在行**。通过该命令。我们可以从杂乱的信息中找到所需要的部分。。语法格式如下：

```shell
grep [选项] 关键字 文件名
```

```shell
# 例如:在/etc/passwd中查找包含“root”字符串的行，grep会将匹配到的字符串标记为红色。
grep 'root' /etc/passwd
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041503277.png" alt="image-20230904150305152" style="zoom:50%;" />

​	**注意:**grep命令不支持"*"和"?"这些普通意义的通配符，而是通过正则表达式来设置所要查找的条件。正则表达式定义了很多不同意义的符号，如**符号"^"表示以什么字符开头，符号`$`表示以什么字符结尾。如`^word`表示以word开头，`word$`表示以word结尾**。

​		需要说明的是，如果grep所使用的查找关键字中不包含正则表达式或是空格等特殊符号，那么关键字是否加引号都无所谓，如果关键字出现了这些符号，建议给这些关键字加上引号。

```shell
例如：在/etc/password查找以“root”开头的行
```

![image-20230904150535861](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041505946.png)

**`grep`命令常用选项：**

- `-n`：输出符合查找条件的行及其行号：

```shell
grep -n 'root' /etc/passwd
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041507920.png" alt="image-20230904150707791" style="zoom: 50%;" />

- `-v`：反转查找，输出与查找条件不符合的行：

```shell
grep -v "^#" /etc/passwd				# 查找所有不是以#开头的行
-----------------
grep -v "^$" /etc/ssh/sshd/sshd_config	# 查找不是空白行的内容
```

- `-i`：不区分大小写：i=ignore

```shell
grep -i 'a' test.txt				# 在文件中查找不区分大写小写有a的行
```

- `-w`：精确匹配单词：

```shell
echo "The num is 10" > test2.txt		# 写内容进test2.txt
cat test2.txt
echo "The number is 10" >> test2.txt	# 追加
grep -w 'num' test2.txt
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041511000.png" alt="image-20230904151104849" style="zoom:50%;" />

### 4.2.head和tail命令-查看文件开头或末尾的部分内容

​	`head`和`tail`命令用于显示文件的局部内容。默认条件下，head显示前10行内容，tail显示后10行内容。

```shell
# 例如：查看/etc/passwd文件的前10行和后10行内容
head /etc/passwd
tail /etc/passwd
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041513522.png" alt="image-20230904151337305" style="zoom:33%;" />

**命令选项：**

- `-n`：展示指定几行数字的内容：

```shell
例如：查看/etc/passwd文件前3行的内容
head -n 3 /etc/passwd
也可以写成：head -3 /etc/passwd
```

- `-f`：实时显示文件内容的增量：在生产环境下，tail命令更多的是查看日志文件，以便观察访问数据，服务器信息等。配合“-f”选择跟踪日志文件末尾的变化，实时显示更新内容。

  为了更方便大家的理解，我们可以打开两个shell窗口，执行如下命令查看具体变化：

  ```shell
  # 1.在窗口1中
  echo 'Hello' > test.txt				# 向test.txt文档中执行增加内容Hello
  # 2.在窗口2中
  tail -f test.txt					# 查看test.txt
  # 3.在窗口1中
  echo 'World' >> test.txt			# 再次向test.txt中增加内容
  # 4.在窗口2中
  tail -f test.txt					# 再次查看test.txt中的变化
  ```

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041521307.png" alt="image-20230904152141130" style="zoom:50%;" />



### 4.3.cat命令

​	`cat(Concatenate)`命令是用来查看文本文件内容的。使用该命令时，只需要指定文件名作为参数即可。语法格式如下：

```shell
cat [文本文件]
```

```shell
例如：查看/proc/version文件中的内容，获知系统的版本号。
cat /proc/version
```

![image-20230904152535613](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041525756.png)

**cat常用的命令选项：**

- `-n`：显示行号，包括空白行：

```shell
查看/etc/passwd中的内容，了解Linux中的用户信息
cat -n /etc/passwd
```

### 4.4.wc命令

​	`wc(word count)`命令是用来统计指定文件中的行数，单词数，字节数的。语法格式如下：

```shell
wc [选项] 文件名
```

​	`wc`命令选项如下：

| 选项 | 作用       |
| ---- | ---------- |
| -l   | 显示行数   |
| -w   | 显示单词数 |
| -m   | 显示字符数 |

```shell
wc -l /etc/resolv.conf
wc -w /etc/resolv.conf
wc -c /etc/resolv.conf
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041530901.png" alt="image-20230904153051765" style="zoom:50%;" />

### 4.5.sort命令

​	`sort`命令对文件内容或查询结果排序。语法格式如下：

```shell
sort [选项] 文件名
```

​	常用选项如下：

| 选项 | 作用                                     |
| ---- | ---------------------------------------- |
| -f   | 忽略大小写                               |
| -r   | 反向排序                                 |
| -t   | 指定分隔符                               |
| -i   | 只考虑可以打印的字符，忽略任何非显示字符 |

**`sort`命令是根据从指定的行抽取一个或多个关键字来进行排序的。比较原则是从首字符向后依次按ASCII码进行比较**

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041541537.png" alt="image-20230904154121394" style="zoom:67%;" />

### 4.6.find命令

​	`find`命令可以实现文件的精确查找，但是用法也是相对复杂。语法格式如下：

```shell
find [查找起始路径] [选项] [查找条件] [处理动作]
```

- **查找起始位置：**可以根据需要指定，默认为当前路径，如果指定为"/"，就表示在整个硬盘中查找；
- **查找条件：**指定查找的标准，可以根据文件名，文件大小，文件类型，从属关系，权限等；
- **处理动作：**对符合查找条件的文件进行操作，例如删除。

**find命令的常用选项：**

- `-name`：按名称查找，允许使用通配符：

```shell
find /etc -name passwd
find /etc -name "net*.conf"				# 在/etc中查找以net开头，.conf结尾的文件
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041545487.png" alt="image-20230904154523278" style="zoom:50%;" />

- `-iname`：按名称查找，不区分大小写：

```shell
find /etc -iname "*net*"				# 在/etc下查找含有net的目录和文件，不区分大小写
```

- `empty`：查找空文件或目录：

```shell
find /root -empty						# 在/root文件中查找空文件
```

- `-type`:按文件类型查找。文件类型指普通文件(f)、目录(d)、符号链接文件(l)、块设备文件(b)、字符设备文件(c)等。

```shell
find /boot -type d					# 在/boot中查找所有的子目录
find /etc -type l					#查找/etc目录下的符号链接文件
find /etc -type l -ls				#查找详细动作--处理动作
```

- `-size`:按文件大小查找。一般使用"+"、"-"来设置超过或小于指定大小作为查找条件，常用的容量单位包括k,M,G

```shell
find /etc -size +1M						# 在/etc/目录下查找大于1MB的文件
find /boot -size -10k					# 在/boot目录下查找小于10k的文件
```

- `-not`:取反：

```shell
find /boot -not -type f -ls				# 在/boot目录下查找不是普通文件的文件，并显示详细信息
```

- 按时间戳查找：find命令还可以根据用户的需求按时间戳来查找，可以指定以“天”或是“分钟为查找单位”。**如果以“天”为查找单位，则相应的选项为：-atime(访问时间),-mtime(更改时间),-ctime(改动时间)；如果以“分钟”为单位，则相应的选项为：-amin(访问时间)，-mmin(更改时间)，-cmin(改动时间)。通"-size"选项一样，也可以用"+","-"来设置**。

```shell
find /tmp -atime +7						# 查找7天内没有被访问过的文件
find /etc -mtime -1						# 查找一天没没有更改过的文件
find /root -cmin  -60					# 一小时内灭有改动过的文件
find /etc -cmin -180 -type f 			# 最近3小时内被修改过状态的文件
find / -mtime 2							# 查找两天前当天被修改过的文件
```

- `-exec`:对查找到的结果进行进一步的处理。`-exec`选项后面要跟上进一步处理所要执行的命令，在命令中可以使用"{}"表示find命令查找到的结果，而且最后必须添加`\`表示命令结束（注意前后有空格）。

```shell
find /boot -name "init*" -exec cp {} /tmp \;   	# 查找init开头的文件并复制到/tmp中
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041553185.png" alt="image-20230904155319991" style="zoom:50%;" />

​	exec选项最主要的作用就是将find命令查找出来的结果当作文件去处理，而默认情况下，find命令找到的结果会当作文本信息来处理。

- 同时指定多个查找条件：

```shell
find /boot -size +1024k -name "init*" 				# 查找以init开头并且大小大于1024kb的文件
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041554032.png" alt="image-20230904155437876" style="zoom:50%;" />

### 4.7.xargs命令

​	当find命令在用-exec对查找的结果做进一步处理时，也有可能出现问题。这是将-exec查找到的结果一次性的交给后面来处理，有时候find会找到大量的文件，查出后面命令参数所能执行的范围，就会发生溢出错误，错误信息通常为“参数列太长”或“参数列溢出”。这时就可以使用xargs命令。xargs虽然本身时一个独立的命令，但通常都被用来配合find命令使用。通过xargs命令，可以将find命令查找出来的结果分批次的送给之后的命令进行处理，从而避免参数列溢出的问题。

​	xargs命令需要通过管道与find命令配合使用，语法格式为：

```shell
| xargs commands
```

​	我们先准备一个测试文件：

```shell
mkdir /tmp/pass
echo "password=123" >> /tmp/pass/test.txt
```

​	假设在/tmp目录中存放了大量的文件，在其中某个文件存放了密码，关键字为“password”，我们现在希望将这个存放密码的文件找出。

​	如果执行find命令的-exec选项的命令为：

```shell
find /tmp -name "*.txt" -exec grep "password" {} \;
# password=123
```

​	使用xargs命令执行应该为：

```shell
find /tmp -name "*.txt" | xargs grep "password"
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041602006.png" alt="image-20230904160207804" style="zoom:50%;" />

**示例：**

```shell
find /etc -type f | wc -l				# 查看/etc目录下的普通文件有多少条--1587
# 如果要用-exec现象去这个目录下查找关键词为PermitRootLogin的命令为
find /etc -type f -exec grep "PermitRootLogin" {} \;        # 执行此命令会有明显的卡顿
-----
# 使用xargs命令会很快
find /etc -type f | xargs grep "PermitRootLogin"
# /etc/ssh/sshd_config:#PermitRootLogin yes
# /etc/ssh/sshd_config:# the setting of "PermitRootLogin without-password".
```

### 4.8.which命令

​	在Windows中，强大的搜索功能可以使用户方便的找到自己需要的文件。在Ubuntu中也提供了强大的查找命令，其中`which`命令提供了按路径进行查找的功能。`which`命令按PATH变量所规定的路径查找相应的命令，显示该命令的绝对路径。语法如下：

```shell
which 命令名
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041610738.png" alt="image-20230904161050542" style="zoom:50%;" />



### 4.9.whereis命令

​	`whereis`命令不但能查找命令，而且能查找Ubuntu资料库里记载的文件。语法格式如下：

```shell
whereis [选项] 文件名
```

​	常用选项如下：

| 选项 | 作用                     |
| ---- | ------------------------ |
| -b   | 只查找二进制文件         |
| -w   | 只查找manual路径下的文件 |

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041614164.png" alt="image-20230904161424988" style="zoom:50%;" />

### 4.10.locate命令

​	`locate`命令将所有与被查询的文件名相同的文件查找出来。语法格式如下：

```shell
locate 文件名
```

```shell
locate sshd_config
```

​	locate命令只能实现模糊查找，它会将查找信息的目录和文件全部查找出来。因而,locate命令无法精确查找。**locate命令的查找结果依赖于事先构建好的索引数据库。**而索引数据库默认情况下主要由系统根据周期性任务计划来自动更新，因而locate命令只能查找索引数据库更新之前的文件。

**例如：**新建一个文件，locate命令无法查找：

```shell
touch /tmp/net.bak
locate net.bak						# 无法查找
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041618883.png" alt="image-20230904161805723" style="zoom:50%;" />

### 4.11.diff命令

​	`diff`命令用于对比多个文件之间的差异，这是系统安全防范中非常重要的。比如黑客入侵系统后，往往会修改一些配置，从而留下一些后门。所谓系统运维人员最好将重要文件备份，然后定期执行diff命令进行对比，从而发现是否被改动过。

```shell
cp .bashrc .bashrc.bak					# 备份
ls -a									# 查看包括隐藏文件的所有文件
echo "cd/tmp" >> .bashrc				# 写内容进去
diff .bashrc .bashrc.bak				# 对比
100d99
< cd/tmp
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041639294.png" alt="image-20230904163923109" style="zoom:50%;" />

​	**显示的结果中"a","d","c"分别表示添加、删除、修改的操作。其中以”<“开始的行属于文件1，以”>“开始的行属于文件2。**



## 5.压缩备份基本命令

### 5.1.bzip2命令和bunzip2命令

​	`bzip2`命令和`bunzip2`命令是一对压缩和解压命令。

- 压缩文件时命令格式如下：

```shell
bzip2 文件名1 [文件名2 ...]
```

- 解压文件时命令格式如下：

```shell
bunzip2 文件名1 [文件名2 ...]
```

​	说明：在利用`bzip2`命令进行文件的压缩后，压缩前的原始文件消失，系统会生成一个新的压缩文件，文件的**扩展名为`.bz2`**。另外，利用`bzip2`命令生成的压缩文件必须利用`bunzip2`命令才能解压，恢复原始文件。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041647719.png" alt="image-20230904164704507" style="zoom:50%;" />

​	另外，也可以在一条命令中同时对多个文件进行压缩操作，文件名之间用空格隔开。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041648970.png" alt="image-20230904164853765" style="zoom:50%;" />

### 5.2.gzip命令

​	`gzip`命令是Linux中最常用的压缩/解压命令之一，它能同时完成解压和压缩两个动作。其语法格式如下：

```shell
gzip [-选项] 文件名
```

​	常用选项如下：

| 选项 | 作用              |
| ---- | ----------------- |
| -d   | 解压              |
| -n   | 指定压缩级别(1~9) |

​	利用`gzip`命令可以把普通文件压缩为**扩展名为`.gz`**的压缩文件。压缩完成后，原始文件消失。在压缩式还可以指定压缩的级别，该命令的压缩级别范围是1~9，默认的级别是6。1的压缩级别最低，但速度最快；9的压缩级别最好，但速度最慢。

​	`gzip`命令的解压操作是针对扩展名为`.gz`的压缩文件进行的，它可以把压缩文件还原为普通文件。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041657730.png" alt="image-20230904165723543" style="zoom:50%;" />

### 5.3.zip命令和unzip命令

​	`zip`命令和`unzip`命令可以压缩和解压扩展名为`.zip`的文件。

​	压缩的语法格式为：

```shell
zip [-选项] 文件名
```

​	解压的语法格式为：

```shell
unzip [-选项] 文件名
```

​	共有的常用选项：

| 选项 | 作用                                                         |
| ---- | ------------------------------------------------------------ |
| -d   | 将文件压缩/解压到指定目录中                                  |
| -n   | 不压缩/覆盖已经存在的同名文件                                |
| -v   | 显示指令执行过程或显示版本信息，但不压缩/解压                |
| -o   | 以压缩/解压文件内拥有最新更改时间的文件为准，将压缩/解压文件的更改时间设成和该文件相同 |
| -q   | 不显示指令执行过程                                           |
| -r   | 递归压缩/解压文件                                            |

```shell
zip -vr etc.zip /etc					# 将/etc目录压缩成etc.zip，并显示压缩过程
unzip -v etc.zip 						# 只查看压缩文件，但不解压
unzip -n etc.zip -d /root/test/			# 将etc.zip解压到/root/test目录中
```





### 5.4.zcat命令和bzcat命令

​	`zcat`命令和`bzcat`命令都是用来查看压缩文件内容的，语法格式如下：

```shell
zcat 文件名
bzcat 文件名
```

​	`zcat`命令和`bzcat`命令的不同之处是：`zcat`命令针对扩展名为`.gz`的压缩文件进行查看，而`bzcat`针对的是扩展名为`.bz2`的压缩文件进行查看。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041724790.png" alt="image-20230904172432550" style="zoom:50%;" />

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202309041725745.png" alt="image-20230904172536555" style="zoom: 33%;" />

### 5.5.tar命令

​	`tar`命令对文件或目录进行打包备份和解包操作，打包备份与压缩的含义不同，打包备份是指把多个不同的文件放在一个大文件里，并没有压缩，这个大文件以`.tar`为扩展名。利用`tar`命令打包后，原始文件并没有消失。而压缩是对单一文件进行的，无论是`gzip`命令还是`bzip2`命令都只能生成单个文件的压缩文件。当然，**`tar`命令也可以通过选项参数的设置，将打包和压缩操作一次性完成。另外，它也可以实现解包操作**。其语法格式为：

```shell
tar [-选项] [备份包的文件名] [要打包（解包）的文件或目录]
```

​	`tar`命令的常用选项有：

| 选项 | 作用                                               |
| ---- | -------------------------------------------------- |
| -c   | 创建新的打包文件                                   |
| -x   | 抽取.tar文件里的内容                               |
| -z   | 打包后直接用gzip命令压缩或者解压文件               |
| -j   | 打包后直接用bzip2命令压缩或者解压文件              |
| -t   | 查看打包文件里的文件目录                           |
| -f   | 使用文件或设备，**该选项必须放到选项组的最后一位** |
| -v   | 在打包或解压后将文件的详细清单显示出来             |

​	最典型的操作如下：

```shell
tar -cf filename.tar file1 file2 file3		# 把file1,file2,file3打包，文件名为filename.tar
tar -tf filename.tar 						# 查看filename.tai打包文件中的内容
tar -xvf filename.tar						# 抽取filename.tar里的内容，文件保持不变
```

```shell
tar -cvf etc.tar  /etc							# 将/etc目录下的所有文件打包成etc.tar
tar -zcf etc.tar.gz /etc						# 调用gzip将/etc目录下的所有文件打包为etc.tar.gz
----------------
tar -jcf etc.tar.bz2 /etc						# 调用bz2来打包/etc目录 名字为etc.tar.bz2
----------------
tar -Jcf etc.tar.xz /etc						# 调用xz来打包/etc目录 名字为etc.tar.xz

du -h etc.*										# 查看etc开头文件的大小

------------------

tar -xf etc.tar									# 解包

tar -xf etc.tar.gz								# 将etc.tar.gz解压到当前目录
--------------------
tar -zxf etc.tar.gz -C /tmp						# 将etc.tar.gz解压到/tmp目录下
--------------------
tar -tf etc.tar.bz2								# 不解压，直接查看内容
```



## 6.其他命令

