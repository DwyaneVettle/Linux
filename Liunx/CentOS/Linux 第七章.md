#        Linux 第七章

## 磁盘与文件系统管理

## 1.磁盘分区与格式化

​	在Linux中，当现有的硬盘分区不能满足要求时，就需要对硬盘中的分区进行重新的规划与调整，有时候还需要添加新的硬盘来扩展存储空间。

### 1.1.磁盘及分区的表示方法

​	操作系统中的所有数据都存储在磁盘分区中，在传统的分区中，磁盘分区包括主分区，扩展分区，逻辑分区三种类型。之所以这样分区，是因为在磁盘的主引导扇区MBR中用来存放分区信息的空间只有64字节(主引导扇区一共只有512字节空间)。而每个分区的信息都要占用16个字节，因而理论上，一块磁盘最多只能拥有4个分区，当然这4个分区都是主分区。随着后来磁盘空间越来越大，4个分区已经不能满足需求了，所以又引入了一个扩展分区的概念。扩展分区也是主分区，但它不能直接使用，它相当于是一个容器，可以在扩展分区中再创建新的分区，这些分区被称为逻辑分区。逻辑分区的空间不再受到主引导扇区的限制，像SCSI和SATA接口的磁盘再Linux中最多可以创建12个逻辑分区。

​	**Linux中的所有磁盘以及磁盘中的每个分区都是用文件的形式来表示的。所有的设备文件都统一存放在/dev目录中。**

​	不同类型的硬盘和分区的设备文件都有统一的命名规则，具体表述形势如下：

- 硬盘：对于SATA和SCSI接口的硬盘设备，采用"sdX"的形式命名，其中"X"为"a,b,c,d"等字母，例如，磁盘的第一款硬盘表示为"sda"，第二款硬盘表示为"sdb"。

- 分区：表示分区时，以硬盘设备的文件名作为基础，在后面加上该分区对应的数字序号。例如，第一块硬盘中的第一个分区表示为"sda1"，第二个分区表示为"sda2"。

  需要注意的是：主分区的数目最多只有4个因此主分区和扩展分区的序号就限制为1-4之间而逻辑分区的序号从5开始。

  ![image-20211208221049303](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655744.png)

  ​	另外，对于所有使用USB接口的移动存储设备，都一律使用/dev/sdX的设备文件，**光驱(光盘)的设备文件则一般默认为/dev/cdrom。**

  ![image-20211208221951011](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655745.png)

### 1.2.添加新的硬盘

添加新的硬盘需要在虚拟机的硬件设置中进行添加。

- 设置中点击添加，选择硬盘点击下一步，然后选择硬盘接口类型SCSI;

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655746.png" alt="image-20211208214757503" style="zoom:50%;" />

- 创建一个新的虚拟磁盘；

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655747.png" alt="image-20211208214906289" style="zoom:50%;" />

- 磁盘大小选择默认20G,并将虚拟机磁盘存储为单个文件；

  

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655748.png" alt="image-20211208215010519" style="zoom:50%;" />

- 下一步点击完成，新的硬盘就添加成功。

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655749.png" alt="image-20211208215111286" style="zoom:50%;" />

-  添加了新的磁盘，虚拟系统还没办法进行识别，所以需要重启系统

```shell
reboot						# 重启
shutdown -r now				# 重启
```

### 1.3.查看分区信息

​	在Linux中最基本的磁盘及分区管理工具是fdisk。

**格式：**

```shell
fdisk [-l] [设备名称]
```

```shell
fdisk -l						# 查看分区信息
fdisk -l /dev/sda				# 查看sda的分区信息
fdisk -l /dev/sdb				# 查看sdb的分区信息
```

![image-20211208222505428](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655750.png)

![image-20211208222700146](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655751.png)

我们可以看到/dev/sdb没有进行分区，我们就对这块磁盘进行分区：

- 执行如下命令及步骤：	

  ```shell
  fdisk /dev/sdb			# 对sdb分区
  n						# 新增分区
  p						# 采用主分区
  1						# 分区编号
  2048					# 起始扇区
  +10G					# 分区大小10G
  p						# 查看分区
  ```

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655752.png" alt="2021-12-08_223445" style="zoom:80%;" />

- 再次创建扩展分区：

继续上一步操作执行如下命令及步骤：

```shell
n					# 新增分区
e					# 添加扩展分区
2					# 序号
采用默认值enter
采用默认值enter
n					# 在创建分区
l					# 创建逻辑分区
采用默认值enter
采用默认值enter
+8G					# 设置8G大小
# 再次分区
n 
l
默认
p					# 查看信息
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655753.png" alt="2021-12-08_224151" style="zoom:80%;" />

- 最后输入w保存退出：

![image-20211208224442501](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655754.png)

```shell 
fdisk -l /dev/sdb					# 查看sdb的分区信息
```

![image-20211208224537357](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655755.png)

我们也可以通过如下命令查看分区是否生效：

```shell
cat /proc/partitions
# /proc存放的是内存的数据
-----------
# 如果没有生效可以执行强制刷新命令
partprobe /dev/sdb
```

- 删除分区用d选项

```shell
fdisk /dev/sdb
d						# 默认是从后往前删
q						# 不保存退出
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655756.png" alt="image-20211208225206207" style="zoom: 67%;" />

### 1.4.Linux的文件系统

​	文件系统是操作系统的重要组成部分，它决定了向磁盘分区中存放、读取文件数据的方式和效率。对于一块新的磁盘，在向其中存放数据之前必须先创建文件系统。文件系统在对磁盘分区进行格式化时创建，在系统中存在很多不同类型的文件系统，可以根据情况选择合适的文件系统类型。

​	在windows系统中，硬盘分区都是采用的都是FAT32或NTFS系统，而在Linux系统中，硬盘分区大都是采用ext系列或xfs文件系统。在CentOS7版本之前的系统都是采用ext系列文件系统，**从CentOS7开始则转向了xfs文件系统，这种系统通常被认为是更适合大数据环境。**Linux不支持NTFS的文件系统，如果一定要使用，需要安装一个ntfs-3g的软件。

​	在文件/etc/filesystems中存放的就是Linux中的文件类型。其中"iso9660"是指光盘所采用的文件类型：

```shell
cat /etc/filesystems
```

![image-20211212131447015](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655757.png)

​		另外，在Linux中还有一种文件系统叫swap，swap文件系统是专门给交换分区使用的。交换分区类似于windows系统中的虚拟内存，能够在一定程度上解决物理内存不足的问题。不同的是，在windows系统中采用的是pagefile.sys的系统文件作为虚拟内存使用，而在Linux	系统中则是采用了一个单独的分区作为虚拟内存，这个分区就被称之为交换分区。交换分区的大小一般设置为主物理分区的两倍，如主机物理内存大小为1GB，，交换分区大小设置为2GB则可。由于现在的服务器普遍配置的是大容量的内存，因而对于内存容量在8GB以上的服务器，交换分区的大小统一的设置为8GB即可。在安装Linux系统时，如果选择系统自动对内存分区，那么系统会自动创建swap分区，并为其分配适当的磁盘空间，我们一般也无需再分配。

```shell
swapon -s									# 查看交换分区
free -h										# 查看交换分区的大小
```

![image-20211213202759471](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655758.png)



### 1.5.格式化分区

​	分区创建好后，还必须经过格式化才能使用，格式化的主要目的是在分区中创建文件系统。CentOS7使用的文件系统时XFS，另外也支持EXT的文件系统。

​	格式化分区的命令是**mkfs**，使用**-t选项**是指明所要格式化文件系统的类型。

​	mkfs=make filesystem

​	**格式：**

```shell
mkfs -t 文件系统类型 分区设备
```

```shell
mkfs -t xfs /dev/sdb1						# 将/dev/sdb1格式化为xfs的文件系统
mkfs -t ext4 /dev/sdb5						# 将/dev/sdb5格式化为ext4的文件系统
```

**需要注意的是：格式化时会清除分区中的所有数据，所以执行格式化操作前要做好备份操作。**



### 1.6.挂载存储设备

​	通过之前的操作，我们已将磁盘进行分区，但是/dev/sdb2作为扩展分区是无法使用的，而其他的分区也无法直接被使用，要想使用这些分区，还必须完成最后 一步操作——挂载。挂载是Linux系统与Windows在存储设备操作方式上一个非常重要的区别。

​	在Linux系统中，对各种存储设备中的资源访问(如保存、读取等)都是通过目录结构进行的虽然系统核心可以通过设备文件的方式操纵各种设备，但是对于用户来说还需要一个挂载的过程，才能正常访问存储设备中的资源。

​	**挂载就是将指定系统中的一个目录作为一个挂载点，用户通过访问这个目录来实现对硬盘分区的数据存取操作，作为挂载点的目录就相当于是一个访问硬盘分区的入口。**挂载这个操作就是用来告诉Linux系统：现在有一个磁盘空间，请你把它放在某一个目录中， 好让用户可以调用里面的数据。挂载时，必须以设备文件指定所要挂载的设备。

​	例如把/dev/sdb5挂载到/tmp目录中，当用户在/tmp目录下执行数据存取操作时，Linux就知道要到/dev/sdb5上执行相关操作。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655759.png" alt="image-20211213205136060" style="zoom:50%;" />

​	挂载使用命令mount，命令格式为:

```shell
mount [-t 文件系统类型] 设备文件名 挂载点目录
```

​	其中，文件类型可以省略-由系统自动识别，设备文件名应区分开每种设备所对应的名字，也可以是网络资源的路径，挂载点则是用户指定挂载的目录。**挂载点的目录必须是事先已经存在的目录。**

​	需要注意的是：**如果挂载点是一个有文件或目录的目录,那么里面的数据会自动转移到分区中。**

​	卸载使用的命令是umount，需要指定挂载点目录或对应设备文件名作为参数，格式为：

```shell
umount 设备文件名|挂载点目录
```

```shell
mkdir /data								# 创建/date目录
mount /dev/sdb1 /data					# 将/date作为/dev/sdb1的挂载点
df
-----------
ls /home								# 查看/home里的数据
mount /dev/sdb5 /home					# 将/dev/sdb5挂载到/home下
ls /home								# 此时/home下没有数据
umount /home							# 取消挂载，恢复数据
df 
ls /home 
```

​	**查看当前系统挂载的设备用命令df命令**

```shell
df
```



### 1.7.自动挂载

​	**我们使用mount命令实现挂载可以立即生效，但是无法永久生效。一旦将系统挂机或重启功能就失效了，而如果通过修改配置文件的方式来实现该功能就可以实现永久有效，但是无法立即生效。**

​	 修改/etc/fstab文件实现自动挂载。

![](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171655760.png)

```sehll
blkid /dev/sda1								# 查看sda1的UUID及文件系统类型
```





## 2.练习

```shell
1.找到ls命令的程序文件路径，并人性化显示该文件的详细信息 which+ll -h
2.将/var/log/messages文件设置为只能向其中追加写入数据，但不能删除原有属性 chattr +a
3.找出/etc目录中1年没变更过的文件 find /etc -ctime +365
4.查看/etc/shadow文件被设置的扩展属性  lsattr 
5.找出/etc目录中的所有文件 find /etc -type f
6.在整个文件中查找所属者是张三的用户并过滤错误信息 find / -user 2> 
7.创建一个磁盘分区，并设置2个主分区，1个扩展分区，2个逻辑分区
8.将1主分区格式化文件格式为xfs，2主分区文件类型为xfs,并将它们分别挂载到/abc，/xyz
```

