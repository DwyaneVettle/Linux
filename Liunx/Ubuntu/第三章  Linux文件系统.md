# 第三章  Linux文件系统

​	文件系统是操作系统用于确定磁盘或分区上的文件的方法和数据结构，即文件在磁盘上的组织方法。文件系统由3部分组成：与文件管理有关的软件、被管理的文件以及实施文件管理所需的数据结构。



## 1.Ubuntu的文件系统

​	文件系统负责为用户建立、保存、读出、修改、转储文件，控制文件的读取，当用户不再使用时删除文件等。磁盘或分区和它所包含的文件系统的种类有很大关系。少数程序基于特定文件系统进行操作，在其他类型的文件系统中不能工作。一个分区或磁盘作为文件系统使用前，需要进行初始化，并将记录数据结构写到磁盘上，这个过程就称为**文件系统的建立**。下面介绍几种常见的文件系统类型：

- **FAT文件系统**

  FAT，全称File Allocation Table，即文件分配表，最早于1982年开始应用于MS-DOS中。FAT可允许Windows3-9x、MS-DOS等操作系统访问。FAT文件系统也是一种最初用于小型磁盘和简单文件夹结构的简单文件系统，用文件分配表映射和管理磁盘空间。它专门为单用户操作系统开发的，不保存文件的权限信息，除了隐藏、只读等公共属性以外，不具备高级别安全防护措施。FAT最大只支持2GB，FAT32可达到2047GB.

- **NTFS文件系统**

   NTFS，全称New Techanology File System，新技术文件系统，最早用于Windows NT/2000操作系统的文件系统。它支持文件系统故障恢复，尤其是大存储量的媒体和长文件名。NTFS是一个高度可靠、可恢复的文件系统，提供了FAT文件系统所没有的安全性、可靠性和兼容性。它提供了加密功能，大大提高了信息的安全性，可以赋予单个文件和文件夹访问权限，在NTFS分区上，可以为共享资源、文件夹以及文件设置访问权限。

  NTFS相较于FAT能更有效的利用磁盘空间，虽然NTFS文件可以读取FAT文件系统和HPFS（High Performance File System，高性能文件系统）文件系统的文件，但是不能被它们所读取，因此兼容性较差。



​	Linux操作系统采用的文件系统一般为Ext2、Ext3、Ext4等。Ext是Extended File System的缩写，意为扩展的文件系统。Linux作为开源的操作系统，其也可以支持FAT32和NTFS，**如果用户想在Linux操作系统中使用非Linux文件系统，就必须在操作系统中挂载这些文件系统到Linux内核中**。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308262230988.png" alt="image-20230826222957844" style="zoom:50%;" />

​	Linux文件系统各分层之间的功能：

- **设备驱动程序**：文件系统利用存储设备存储文件，因此，存储设备是文件系统的物质基础。Linux系统中各设备驱动程序都通过统一的接口与文件系统连接，文件系统向用户提供使用文件系统的接口，设备驱动程序则控制设备实现具体的文件I/O操作。
- **实际文件系统：**实际文件系统是以磁盘分区来划分的，每个磁盘分区由一个具体的文件系统管理，不同磁盘分区的文件系统可以不同。Linux默认的文件系统是Ext2、Ext3、Ext4.
- **虚拟文件系统：**Linux为了屏蔽各文件系统之间的差别，为用户提供访问文件的统一接口，在具体的文件系统之上增加了一个称为虚拟文件系统(Virtual File System,VFS)的抽象层。VFS是Linux对外接口，任何要使用文件系统的程序都必须经由这个接口来使用它。VFS是一个异构文件系统之上的软件粘合层。

​       VFS的原理示意图：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308262238190.png" alt="image-20230826223852099" style="zoom:50%;" />

​	有了VFS，用户察觉不到文件系统之间的差异，可以使用同样的命令和系统调用来操作系统不同的文件系统，并可以在它们之间自由的复制文件。**VFS的作用就是采用标准的Linux系统调用读写位于不同物理介质上的不同文件系统中的文件**。

- **缓存机制：**文件系统和存储设备进行数据传输时，采用缓存机制来提高存储设备的访问效率。缓存区实在内存中划分的特定区域，每次从外部设备读取的数据都暂时存放在这里。下次读取时首先搜索缓存区。如果缓存区没有，则再启动存储设备，读取相应的数据。写入的数据也要先存放在缓存区，然后再分批写入磁盘中。



### 1.1.Ext2文件系统

​	Ubuntu中使用的是Ext2文件系统，它的特点是存取文件的性能记号，对于中小型的文件更具优势，这主要得益于它的簇快取层的优良设计。其单一文件大小与文件系统本身的容量上限以及簇的大小有关。在x86计算机系统中，簇最大为4KB，则单一文件大小上限为2048GB，而文件系统的容量上限为16384GB。

​	Ext2文件系统采用多重索引结构，用inode中的索引表描述如下图：

<img src="https://img-blog.csdnimg.cn/20190905151810391.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dlbmd6aGlrdWkxOTky,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:50%;" />

<img src="https://img-blog.csdnimg.cn/20190901105304828.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dlbmd6aGlrdWkxOTky,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:50%;" />

![Ext2文件系统多重索引结构](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308271031216.png)

​	索引表中前12个表项是直接指针，直接指向文件的数据块，这些块称为直接块。第13个表项是一个一级间接指针，它指向一个索引块，这个索引块中存放的是间接索引表。索引表的第14和15项提高了一个二次间接指针和一个三次间接指针，可提供对更多的间接块索引。**提供多级间接指针的目的是为了表达大型文件的结构**。

​	Ext2文件系统**默认块的大小是1KB**，对于12KB以下的小文件，不需要使用间接索引，所有信息均在inode中，因此访问的速度非常快。较大的文件需要用到一个间接索引表，一个间接索引表含有256个间接指针，每个指针占4B，则1KB的块可以容纳256个指针，可以索引256个间接块。因此，大小12~268KB的文件西药依次间接索引，访问速度会有所降低。而对于大型文件，可以使用二次间接指针甚至三次间接指针，得到最大约16GB的文件。

​	Ext2的核心是两个内部数据结构，即**超级块（superblock）和inodo**。

​	超级块是一个包含文件系统重要信息（如标签、大小、inode的数量等）的表格，它是对文件系统结构的基础性、全局性描述，因此，没有超级块的文件系统将不再可用。由于这个原因，Ext2文件系统中不同位置存放着超级块的多个副本。

​	inode是基本的文件级数据结构，文件系统中的每一个文件都可以在一个inode中找到它的描述。inode描述的文件信息包括文件的创建和修改时间、文件大小、实际存放文件数据的块列表等。对于较大的文件，块列表可能包含附加数据块列表的磁盘位置（即间接块），甚至有可能出现二级或三级间接块列表。文件名字通过目录项关联到inode，目录项由文件名和inode构成。Ext2文件系统的数据结构如下：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308271052958.png" alt="Ext2文件系统数据结构" style="zoom:50%;" />

​	Ext2文件系统以引导扇区(boot sector)开始，紧接着是块组(block group)。因为inode表和存储用户数据的数据块(data block)可以位于磁盘相邻位置，这样就可以减少寻道时间。为了性能的提升，整个文件系统被分为多个块组：

- **超级块**：存储文件系统信息，必须位于每个块组的顶部。
- **块组描述符**：存储块组的相关信息。
- **块位图**：用于管理未使用的数据块。
- **inode位图**：用户管理未使用的inode。
- **inode表**：每个文件都有一个相应的inode表，用来保存文件的元数据，例如文件模式、uid、gid、atime、ctime、mtime、dtime和数据块指针。
- **数据块**：存储实际的用户数据。



### 1.2.Ubuntu的目录结构

​	Linux文件系统采用**树状分层结构**，且只有一个根节点。每个目录中均包含以句点(.)和双句点(..)命名的两个特殊的目录文件，分别表示当前目录和其父目录。这两个特殊目录把文件系统中的各级目录有机地联系在一起。**“.”是当前目录的别名，要访问当前目录中的文件时都可以直接使用"."，而不必明确给出当前目录名。“..”是当前目录的父目录的别名，从任何目录位置开始，都可以使用“..”逐层攀升到文件系统层次的最上层**。

​	与Windows相同，Linux中的文件也分为相对路径和绝对路径。Ubuntu的目录众多，但所有目录都在根目录下，所以安装时一定要有一个与根目录相对应的磁盘分区才能安装系统。有序的组织结构有助于用户访问、管理和Ubuntu系统。Linux目录结构的描述如下：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308280926821.png" alt="image-20230828092641692" style="zoom:50%;" />

| 目录        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| /           | Linux文件系统的根目录                                        |
| /bin        | 存放系统中最常用的可执行文件(二进制文件)。系统所需要的基本命令位于此目录下，也是最小系统所需要的命令，如ls、cp、mkdir等。/usr/bin目录中的文件是普通用户可以使用的命令 |
| /boot       | 存放Linux内核和系统启动文件，包括grud、lilo启动程序          |
| /dev        | 存放所有设备文件，包括硬盘分区、键盘、鼠标、USB、tty等       |
| /etc        | 存放系统所有配置文件，例如，passwd存放用户账户信息，hostname存放主机名。/etc/fstab用户开机自动挂载一些分区，在里面写入一些分区的信息，就能实现开机挂载分区 |
| /home       | 用户主目录的默认位置                                         |
| /initrd     | 存放启动时挂载initrd.img映像文件以及所需设备模块的目录       |
| /lib        | 存放共享的库文件，包含许多被/bin和/sbin中的程序使用的库文件  |
| /lost+found | 在Ext2或Ext3文件系统中，当系统意外崩溃或意外关机时产生的一些文件碎片放在这里。在系统启动的过程中，fsck工具会检查这里，并修复已经损坏的文件系统。有时系统发生问题，很多文件被移到这个目录中，可以用手工的方式修复文件或将其移到原来的位置上 |
| /media      | 在这个目录下自动创建即插即用型存储设备的挂载点。例如U盘系统自动挂载后，会在这个目录下产生一个目录；CD-ROM/DVD-ROM自动挂载后，也会在这个目录下创建一个目录，存放临时读入的文件 |
| /mnt        | 通常用于作为被挂载的文件系统的挂载点                         |
| /opt        | 作为可选文件和程序的存放目录，有些自定义软件包也会被安装在这里，用户自己编译的软件包也可以安装在这个目录中 |
| /proc       | 存放所有标识为文件的进程，它们通过进程号或其他的系统动态信息进行标识。例如CPU、硬盘分区、内存信息等就存放在这里。 |
| /root       | 根用户的主目录                                               |
| /sbin       | 存放涉及系统的管理命令，也就是root用户可执行的命令。这个目录和/usr/bin、/usr/X11R6/sbin、/usr/local/sbin目录是相似的 |
| /srv        | 存放系统所提供的服务数据                                     |
| /sys        | 用于将系统设备组织成层次结构，并向用户提供详细的核心数据信息 |
| /tmp        | 临时文件目录。/var/tmp目录与之相似                           |
| /usr        | 用于存放与系统用户直接有关的文件和目录，如应用程序及支持系统的库文件。其主要的子目录如下：<br /><br />/usr/X11R6：X Windows系统<br /><br />/usr/bin：用户管理员的标准命令<br /><br />/usr/include：C/C++等开发工具语言环境的标准include文件<br /><br />/usr/lib：应用程序及程序包的链接库<br /><br />/usr/local：系统管理员安装的应用程序<br /><br />/usr/local/share：系统管理员安装的共享文件<br /><br />/usr/sbin：用户和管理员的标准命令<br /><br />/usr/share：使用手册等共享文件<br /><br />/usr/share/dict：词表的<br /><br />/usr/share/man：系统使用手册<br /><br />/usr/share/misc：一般数据<br /><br />/usr/share/sgml：SGML数据<br /><br />/usr/share/xml：XML数据 |
| /var        | 通常用于存放长度可变的文件，例如日志文件和打印机文件。其主要子目录如下：<br /><br />/var/cache：应用程序缓存目录<br /><br />/var/crash：系统错误信息<br /><br />/var/games：游戏数据<br /><br />/var/lib：各种状态数据<br /><br />/var/lock：文件锁定记录<br /><br />/var/log：日志记录<br /><br />/var/mail：电子邮件<br /><br />/var/opt：/opt目录的变量数据<br /><br />/var/run：进程的标识数据<br /><br />/var/spool：存放电子邮件、打印任务等的队列<br /><br />/var/tmp：临时文件目录 |

​	**注意：**与Windows不同，在Ubuntu中是严格区分大小写的。并且在Windows中，后缀名用来表示这个文件的文件类型，而在Linux中，后缀名和文件类型没有直接关系，**Linux中一切皆为文件**。



## 2.创建、挂载与卸载文件系统

### 2.1.创建文件系统

​	在安装Linux操作系统时，系统会要求用户进行分区，在磁盘等存储设备分区后即可着手创建文件系统。创建文件系统时主要有两种方法：

- **mkfs命令：**在选定的磁盘分区中创建指定的文件系统；
- **利用各种特定工具：**如mke2fs、mkfs.ext2等，在选定的磁盘分区上直接创建特定类型的文件系统。



​	创建文件系统时，最基本的方法就是使用mkfs命令。在Linux中，mkfs命令实际上只是各种文件系统创建程序的一个总控程序，根据指定的文件系统类型，mkfs将会调用特定文件系统的创建程序mkfs.fs，其中fs可以时ext2、ext3或vfat等。因此在创建一个具体的文件系统时，可以使用特定的文件系统创建命令。例如，在创建一个具体的文件系统时，可以使用特定的文件系统创建命令，也可以使用等价的mke2fs命令。对于Ext2、Ext3文件系统而言，mke2fs民老公是最基本的工具。

​	用于创建Ext2/Ext3文件系统的mkfs与mke3fs命令的语法格式如下：

- mkfs：

```shell
mkfs [-V] [-t fstype] [fs-option] device [size]
```

- mke2fs：

```shell
mke2fs [-c|-l filename] [-b block-size] [-f fragment-size]
	            [-i bytes-per-inode] [-I inode-size] [-J journal-options]
	            [-G meta group size] [-N number-of-inodes]
	            [-m reserved-blocks-percentage] [-o creator-os]
	            [-g blocks-per-group] [-L volume-label] [-M last-mounted-directory]
	            [-O feature[,...]] [-r fs-revision] [-E extended-option[,...]]
	            [-T fs-type] [-U UUID] [-jnqvFSV] device [blocks-count]
```

​	其中主要选项说明如下：

- `-b`：指定块大小，单位为字节
- `-c`：检查是否有损坏的块
- `-f`：指定不连续段的大小，单位为字节
- `-i`：指定没多少字节创建一个inode
- `-N`：指定要创建的inode数目
- `-L`：设置文件系统的标签名称
- `-m`：指定给管理员保留的块的比例，默认值是5%
- `-M`：记录最后一次挂入的目录
- `-r`：指定要建立的Ext2文件系统版本
- `-V`：显示命令的版本号



​	要明白mkfs命令的执行过程，我们先在虚拟机中添加一块20GB的未分区硬盘，添加完毕后重启系统生效。

- 设置中点击添加，选择硬盘点击下一步，然后选择硬盘接口类型SCSI：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281120769.png" style="zoom: 33%;" />

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281120149.png" alt="image-20230828112057079" style="zoom: 50%;" />

- 创建一个新的虚拟磁盘：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281121961.png" alt="image-20230828112131885" style="zoom:50%;" />

- 磁盘大小选择20GB,并将虚拟机磁盘存储为单个文件：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281123034.png" alt="image-20230828112313952" style="zoom:50%;" />

- 重启生效。



​	此时，我们使用`fdisk -l`命令查看新增硬盘的信息。其中Disk/dev/sdb即为新增的硬盘，因为没有床架那文件系统，所以没有包含任何有效的分区表。

![image-20230828113233572](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281132700.png)



​	接下来，我们使用`mkfs -t ext2 /dev/sdb`命令对其进行创建文件系统的操作：

![image-20230828113415045](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281134180.png)



​	最后要说明的是，在使用mkfs命令创建文件系统时，如果未使用`-L`选项指定文件系统的卷标，在创建文件系统后，也可以使用`e2label`命令指定文件系统的卷标。`e2label`命令的主要功能就是显示和命名未安装文件系统的卷标，其语法格式如下：

```shell
e2label device [newlabel]
```

​	其中device为磁盘分区的设备名称，例如/dev/sda6；newlabel表示文件系统的卷标。如果未指定newlabel，`e2label`命令将输出文件系统的卷标。需要指出的是，卷标不能超过16个字符。下面将刚才创建的文件系统的卷标命名为datal：

![image-20230828114248108](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281142190.png)

**注：**卷标是一个磁盘的一个标识，不唯一。由格式化自动生成或人为设定。仅仅是一个区别于其他磁盘的标识而已。



### 2.2.挂载文件系统

​	在Ubuntu系统中，对于一个文件系统或分区而言，如果想要使用它，必须先对其进行挂载操作。挂载就是把新建的文件系统安装到Linux文件系统目录层次结构的某个挂载点上，然后才能使用新建的文件系统。也就是说，挂载点必须是目录，可以将挂载看成一个链接动作。

​	例如，如果想使用/dev/sdb分区，需要对该分区进行读写数据的操作，但是不能直接对其进行操作，需要建立一个目录，使用挂载操作建立它与分区的对应关系。而这个目录就代表了/dev/sdb分区，挂载后对于目录的数据读写操作本质上就是对/dev/sdb分区的读写操作。与之对应，卸载就是断开目录与/dev/sdb分区之间的对应关系，但并不删除目录，/dev/sdb分区也继续存在，如果要读写数据，需要再次进行挂载擦操作。

​	**1.挂载文件分区的命令是`mount`，其语法格式如下：**

```shell
mount [-t vfstype] [-o 选项] device dir
```

​	各选项说明如下：

- `-t`：vfstype指定文件系统类型。通常不必执行，`mount`命令会自动选择正确的类型。常用的类型如下：

| vfstype中的各选项 | 作用                      |
| ----------------- | ------------------------- |
| iso9660           | 光盘或光盘镜像            |
| msdos             | DOS FAT16文件系统         |
| vfat              | Windows 9x FAT32文件系统  |
| ntfs              | Windows NT NTFS文件系统   |
| smbfs             | Mount Windows文件网络共享 |
| nfs               | UNIX（Linux）文件网络共享 |

- `-o`：用来描述设备或文档的挂载方式。常用的选项参数如下：

| -o选项    | 作用                                   |
| --------- | -------------------------------------- |
| loop      | 用来把一个文件当成硬盘分区挂载在系统上 |
| ro        | 采用只读方式挂载设备                   |
| rw        | 采用读写的方式挂载设备                 |
| iocharset | 指定访问文件系统所用的字符集           |
| device    | 要挂载的设备                           |
| dir       | 设备在系统上的挂载点                   |

​	**挂载点的目录必须是事先已经存在的目录。**需要注意的是：**如果挂载点是一个有文件或目录的目录,那么里面的数据会自动转移到分区中。**

```shell
mkdir /data								# 创建/date目录
mount /dev/sdb /data					# 将/date作为/dev/sdb1的挂载点
df
-----------
ls /home								# 查看/home里的数据
mount /dev/sdb /home					# 将/dev/sdb5挂载到/home下
ls /home								# 此时/home下没有数据
umount /home							# 取消挂载，恢复数据
df 
ls /home 
```

​	**2.查看当前系统挂载的设备用命令df命令。**

```shell
df
```

​	<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281442072.png" alt="image-20230828144214913" style="zoom:50%;" />

​	**3.卸载一个文件系统，它的使用权限是超级用户或/etc/fstab中允许的用户，使用`umount`命令，它的使用方式和参数和`mount`是一样的**。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281443933.png" alt="image-20230828144335843" style="zoom:50%;" />

​	**4.`du`命令：用于查看`当前目录`下所有文件及目录信息。**

```shell
du [选项]
```

| 选项 | 作用                               |
| ---- | ---------------------------------- |
| -a   | 列出所有文件及目录大小             |
| -h   | 以GB或MB为单位显示文件或目录的大小 |
| -b   | 显示目录和文件的大小，以B为单位    |
| -c   | 最后加上总计                       |
| -s   | 只列出个文件大小的综合             |
| -x   | 只计算属于同一个文件系统的文件     |

**5.fsck命令：硬盘 检测，该命令只能由root用户执行。**

```shell
fsck 分区名
```

![image-20230828144938054](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308281449146.png)



### 2.3.自动挂载

​	我们使用mount命令实现挂载可以立即生效，但是无法永久生效。一旦将系统挂机或重启功能就失效了，而如果通过修改配置文件的方式来实现该功能就可以实现永久有效，但是无法立即生效。

​	修改/etc/fstab文件实现自动挂载。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308301024840.png" alt="image-20230828145521498" style="zoom:50%;" />

```shell
blkid /dev/sdb								# 查看sdb的UUID及文件系统类型
```

