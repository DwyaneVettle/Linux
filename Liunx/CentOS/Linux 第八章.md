# Linux 第八章 软件包的管理

​	软件资源丰富及安装便捷是Windows系统的优势，在Linux系统中安装软件相对来说要复杂一些。Linux安装软件有三种方式：源码安装、RPM软件包安装、YUM安装。比较常见且易于安装的方式是YUM安装。



## 1.文件的打包和压缩

​	如果我们从网上下载一些Linux系统中使用的软件，往往下载的是一些后缀名为".gz",".bz2",".xz"或是".tar.gz",".tgz"之类的压缩文件，这些文件需要解压后才能安装使用。

​	Linux系统打包压缩命令是tar命令，我们也可以使用du命令来查看磁盘的空间占用情况，以对压缩前后的文件大小做对比。

### 1.1.du命令-查看文件或目录占用磁盘的大小

​	du(disk usage)命令统计指定目录或文件所占磁盘空间的大小。

​	常用选项：

- **-h**:人性化显示,以k,M,G为单位显示
- **-s**:查看目录本身的大小。s是sum求和的意思，如果不加这个选项，会显示指定目录下所有的子目录和文件的大小。

```shell
du -h /etc/ssh/sshd_config						# 查看sshd_config的大小
# 4.0K    /etc/ssh/sshd_config					4k是一个块的大小=512b*8个扇区
du -hs	 /etc									# 查看etc的大小
# 43M     /etc
du -hs /*										# 查看根目录下的子目录的占用空间情况
df -hT											# 挂载占用情况
```



### 1.2.tar命令-文件打包与压缩

​	Linux系统的打包和压缩是两个独立的操作。常用的打包命令是tar(tape archive)，常用的压缩文件有三个：gzip,bzip2,xz，用gzip通常使用的后缀".gz"，用bzip2通常使用的后缀".bz2"，用xz通常使用的后缀".xz"。

​	这三个压缩工具通常都是对单个文件进行压缩与解压，所以通常都是通过tar命令将多个文件或目录打包成一个包文件，然后再用某种压缩工具压缩。如后缀为".tar.gz",".tgz"和".tar.bz2"的文件都是先打包再压缩的文件。

​	在实际的使用中，**一般都是通过tar命令来调用gzip,bzip2或xz进行压缩或解压**，而很少去单独使用这些命令。

#### 1.2.1.打包压缩

​	用tar命令打包压缩的格式为:

```shell
tar [选项] 打包或压缩的文件名 需要打包的源文件或目录
```

```shell
tar -cvf etc.tar  /etc							# 将/etc目录下的所有文件打包成etc.tar
```

​	tar命令中用到的选项的含义：

- **-c:**创建".tar"格式的包文件，该选项不会对包文件进行压缩
- **-v:**显示命令的执行过程。该选项非必须，可根据情况选用
- **-f:**指定要打包或解包的文件名称，**该选项必须放到选项组的最后一位**
- **-z:**调用gzip来压缩文件，后缀名.gz
- **-j:**调用bzip2来压缩包文件，后缀名.bz2
- **-J:**调用xz来压缩包文件，后缀名.xz

```shell

tar -zcf etc.tar.gz /etc						# 调用gzip将/etc目录下的所有文件打包为etc.tar.gz
----------------
tar -jcf etc.tar.bz2 /etc						# 调用bz2来打包/etc目录 名字为etc.tar.bz2
----------------
tar -Jcf etc.tar.xz /etc						# 调用xz来打包/etc目录 名字为etc.tar.xz

du -h etc.*										# 查看etc开头文件的大小
```

#### 1.2.2.解包压缩包

​	用tar命令来进行解包或者解压缩的格式为：

```shell
tar [选项] 打包或压缩文件名 [-C 目录名]
```

​	常用选项有：

- **-x**:  tar格式的包文件
- **-C：**指定解压后文件存放的目的位置
- **-t:**在不解压的情况下可以查看压缩文件包含哪些内容

```shell
tar -xf etc.tar									# 解包

tar -xf etc.tar.gz								# 将etc.tar.gz解压到当前目录
--------------------
tar -zxf etc.tar.gz -C /tmp						# 将etc.tar.gz解压到/tmp目录下
--------------------
tar -tf etc.tar.bz2								# 不解压，直接查看内容
```



## 2.Linux中的软件安装

### 2.1.源码安装

​	早期想要在Linux系统中安装软件，只能采用源码安装，这非常困难，且耗费精力。这是由于Linux系统中使用的软件绝大多数都是开源的，软件作者在发布的时候直接提供的就是软件源代码，用户在取得软件的源码后，需要自行编译并解决依赖问题，因此源码安装需要用户有很多的相关的知识，高超的技能，充沛的精力才能安装成功。在安装、升级、卸载时还要考虑与其他程序的依赖问题，所以源码安装是一件难度非常大的操作。

​	源码安装的优势：

- 可移植性好：可以在任何Linux系统中安装使用，而rpm软件包只能用于RedHat类的Linux系统；

- 运行效率高：可灵活定制软件功能。使用源码安装会有编译的过程，因此软件可以更好的使用安装主机的系统环境；

- 版本新：Linux系统中大部分软件都是开源的，这些软件总是以源码的形式发布，之后才会形成rpm封装包。

  Linux中安装的软件包一般都是C语言开发的，所以我们需要安装gcc编译器，编译软件。

  ```shell
  yum install gcc -y									# 安装gcc编译器
  ```

  源码安装的基本流程包括解包、配置、编译、安装这四个步骤来完成：

  <img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656874.png" alt="image-20211221214153874" style="zoom:50%;" />



​		源码安装相对复杂，这里不再演示，更多的是采用以下两种安装方式：

### 2.2.RPM安装

​	RPM(Redhat Packet manager)安装包管理系统由红帽系统提供，**rpm是一种已经编译并封装好的软件包，用户可以直接安装使用。**rpm软件包是由CentOS中软件的基本组成单位，每个软件都是由一个或多个rpm软件包组成。通过RPM，用户可以非常轻松的管理系统中的所有软件。

​	**rpm软件包只能在使用RPM机制的Linux系统中使用，如CentOS、RHEL、Suse等。**	在Linux世界里，还有另外的一种软件管理方式DEB，可以在Debian、Ubuntu上使用。相比较而言，rpm安装包应用更加广泛，已成为Linux系统事实上的标准。但是rpm也有一个很大的缺点，即rpm软件包之间可能存在复杂的依赖关系，有时候下载一个软件需要下载其他的很多依赖软件。

​	使用RPM机制封装的软件包文件拥有约定俗称的命名格式，一般使用“软件名-软件版本-发布号。硬件平台类型.rpm”的文件形式命名：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656875.png" alt="image-20211221203410646" style="zoom: 67%;" />

​	软件包放在"/mnt/cdrom/Packages"下。

```shell
ls /mnt/cdrom/Packages
```

![image-20211221203726419](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656876.png)



#### 2.2.1.安装\卸载软件

​	利用rpm命令安装软件首先要进入到存放rpm软件包的目录，安装软件包使用的命令是"**rpm -ivh**"。

```shell
rpm -ivh
```

​	选项的含义：

​	-i---安装软件包；-v---显示安装过程；-h---显示安装进度，安装每进行2%就会显示一个#号。

​	如：利用rpm安装vsftpd程序（按Tab补全程序名字）：

```shell
cd /mnt/cdrom/Packages							# 进入到rpm软件包存放目录
rpm -ivh vsftpd-3.0.2-28.el7.x86_64.rpm			# 安装vsftpd程序
```

![image-20211221204539461](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656877.png)

```shell
rpm -e vsftpd									# 卸载vsftpd
```

#### 2.2.2.查询软件包

​	安装软件推荐使用yum方式，rpm命令如今主要是用来查询软件包，用到的相关选项是"-q"(query)。

```shell
rpm -q openssh
# openssh-7.4p1-21.el7.x86_64
rpm -q httpd
# 未安装软件包 httpd
rpm -qa | grep ssh 								# 列出所有的名字含ssh的软件，-a选项表示列出所有
```

​	**rpm -q命令查询时，必须指定软件的完整名字。**

​	**通过“-qi”选项可以查询某个已安装软件包的详细信息。**不同于yum info命令，如果软件未安装，则无法用该选项。

```shell
rpm -qi openssh									# 查看openshh软件包的信息。
```

#### 2.2.3.ql选项-查询软件安装包所安装的文件

​	一个典型的Linux应用程序通常由以下几部分组成：

- 普通可执行程序：存放于“/usr/bin”，普通用户即可执行；
- 管理程序文件：存放于“/usr/sbin”，有管理员权限才能执行；
- 配置文件：存放于“/etc”，配置文件较多时会创建相应的子目录；
- 日志文件：存放于"/var/log"；
- 程序参考文档：存放于"/usr/share/doc"；
- 可执行文件及其man文件手册：存放于“/usr/share/man"。

```shell
rpm -ql openssh									# 查询openssh在系统什么位置安装了程序文件
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656878.png" alt="image-20211221212800424" style="zoom:50%;" />

#### 2.2.4.qc选项-查询软件包所安装的配置文件

​	通过"-qc"选项可以查看某个软件包所安装的配置文件：

```shell
yum install vsftpd								# 安装vsftpd
rpm -qc vsftpd									# 查询vsftpd的配置文件
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656879.png" alt="image-20211221213127458" style="zoom:50%;" />

#### 2.2.5.qf选项-查询某个文件所属的软件包

```shell
rpm -qf /usr/bin/find
```



### 2.3.YUM安装

​	YUM(Yellow dog Updater,Modifie)起初是由yellow dog这个发行版的发明者Terra Soft研发，用Python写成。YUM安装方式仍基于RPM包管理系统，但是它**可以自动解决rpm软件包之间的依赖问题**，从而更轻松的管理Linux中的软件。



#### 2.3.1.配置YUM源

​	采用YUM安装的方式，首先要配置好yum源 yum源也称为YUM仓库(yum repository)，其集中存放了大量的软件安装包，以及软件安装包相关的元数据，这些文件一般都放置在特定的名为repodata的目录下。设置YUM源需要配置定义文件，**定位文件必须存放在指定的"/etc/yum.repos.d/"的目录中，而且必须以".repo"作为文件后缀名。**

​	我们通常所用的YUM源有两种类型：一种是来自网络上的服务器，一种是来自本地系统的安装光盘。比如CentOS7系统的"/etc/yum.repos.d/"目录默认已经存放的后缀为.repo的yum源文件，以其中CentOS-BASE.repo为例，这是一种网上的服务器为yum源的配置文件，文件部分内容如下，其中http://mirrorlist.centos.org就是CentOS的官方服务器。

```shell
cat /etc/yum.repos.d/CentOS-Base.repo
```



![image-20211216094506975](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656880.png)

​	

​	在国内访问CentOS的官网速度可能会比较慢，因而推荐使用阿里云、网易云等镜像站作为yum源，为了避免系统中同时存在多个yum源而造成混乱，建议先将系统中默认的yum源全部删除。

```shell
rm -f /etc/yum.repos.d/*	
```

​	然后可以在https://mirrors.aliyun.com/centos/下载yum源配置文件，并存放到/etc/yum.repos.d/目录中。

​	在学习中有可能不方便联外网，这是可以将系统光盘配置为yum源，在CentOS的系统光盘中已经集成了绝大多数应用软件的rpm包，这些软件虽然不是最新的，但是是最稳定的。

​	首先挂载光驱：

```shell
df -hT | grep -v tmpfs							# 查看系统挂载情况
mkdir /mnt/cdrom
mount /dev/cdrom  /mnt/cdrom					# 将/dev/cdrom挂载到/mnt/cdrom	
df -hT | grep -v tmpfs							# 确认是否挂载成功
ls /mnt/cdrom/
ls /mnt/cdrom/Packages/  | wc -l
```

​	![image-20211216101132484](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656881.png)

查看光驱的目录结构，所有的rpm软件包都存放在"/mnt/cdrom/Packages"目录中，但在设置yum源时，**不能将这个目录指定为yum源路径，只能将存放元数据文件的repodata目录所在的位置指定为yum源（即/mnt/cdrom）**。

​	配置一个"dvd.repo"的yum源定义文件：

```shell
cd /etc/yum.repos.d/								# 进入到配置文件目录
vim dvd.repo										# 创建一个dvd.repo文件并编辑
# 新增以下内容---=左右两边不能有空格
[dvd]												# yum源文件的名称-名字唯一
name=CentOS7 dvd									# 对yum源进行描述，由用户自定义
baseurl=file:///mnt/cdrom							#指定yum源的访问路径，多个yum源可以设置多个
enable=1											# 是否启用当前yum源
gpgcheck=0											# 是都检测yum源来源的合法性
```

​	保存后，在根目录指定以下命令可以查看当前系统已安装和可安装的yum源软件：

```shell
yum list | more										# 查看yum的情况
yum list | wc -l									# 统计一共有多少yum源安装包
yum repolist										# 检测Yum源仓库列表
```



#### 2.3.2.常用的yum命令

- **yum info - 查看软件包信息**

  执行yum info命令可以查看指定软件包的简要信息，如果该软件包已经安装，命令执行后会显示“已安装的软件包”，尚未安装的软件包会显示“可安装的软件包”。

  ```shell
  yum info openssh								# 查看ssh协议
  yum info vsftpd									# 查看vsftpd软件包的信息
  ```

  ![image-20211221200948455](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171656882.png)

- **yum install - 安装软件**

  安装软件使用"yum install"命令，如果成功的话，会在最后出现“完毕！”或“complete！”提示。

  ```shell
  yum install vsftpd								# 安装vsftpd
  yum install gcc -y								# 确认安装gcc，不用在安装时按y确认
  ```

- **yum remove - 卸载软件**

  **用“yum remove”命令卸载一个软件是，同时会将所有依赖于该软件的其他软件包一并卸载。**所以用此命令卸载时一定要慎重。

  ```shell
  yum remove vsftpd								# 卸载vsftpd
  ```

- **yum clean all - 清除本地缓存**

  ```shell
  yum clean all
  ```




**安装jdk:**

```shell
yum install -y java-1.8.0-openjdk-devel.x86_64
java -version
```



**配置环境变量：**

```shell
vim /etc/profile
```

**在这个文件的最后一行添加内容：**

```shell
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.322.b06-1.el7_9.x86_64
export PATH=$JAVA_HOME$/jre/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

**加载配置文件：**

```shell
source /etc/profile
```

