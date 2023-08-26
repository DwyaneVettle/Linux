# CentOS离线配置Java环境

**环境：**

- 操作系统：Linux-CentOS 7
- Java版本：JDK17
- 远程连接工具：MobaXterm



## 1.JDK下载

官网下载：https://www.oracle.com/cn/java/technologies/downloads/#java17

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202305232123558.png" style="zoom: 33%;" />



​	因为MobaXterm自带Sftp，所以直接将下载后的JDK压缩包拖拽到Linux操作系统中即可（此处拖拽到/root目录下）



## 2.将jdk的压缩包解压到/usr/local

- 解压安装包到/usr/local

```shell
tar -zxvf jdk-17_linux-x64_bin.tar.gz -C /usr/local
```

tar命令各选项释义：

1. `-z`：--gzip，--gunzip，--ungzip 调用[gzip](https://baike.baidu.com/item/gzip?fromModule=lemma_inlink)执行压缩或解压缩；
2. `-x` ：--extract，--get 解开tar文件
3. `-v`： 详细报告tar处理的文件信息。如无此选项，tar不报告文件信息
4. `-f` ：使用档案文件或设备，这个选项通常是必选的
5. `-C`： --directory DIR，转到指定的目录			

**备注**：如Linux中没有安装解压和打包软件，可通过以下命令下载：

```shell
yum -y install zip     # 打包程序
yum -y install unzip   # 解压程序
```



- 为方便后续操作，通过以下命令修改JDK目录

```shell
cd /usr/local
ls
mv jdk-17.0.7 jdk
```

![](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202305232140867.png)



## 3.配置环境变量

Linux提供了两种环境变量的文件：

- 第一个是用户级别的环境变量，存放在：~/.bashrc
- 第二个是系统级别的环境变量，存放在：/etc/profile



输入命令`vim  /etc/profile` 进行编辑，`vim`命令小科普：

```shell
i：进入编辑
编辑好之后。
先按Esc，然后输入‘:’
wq保存退出
q！不保存退出
```

在`/etc/profile`文件末尾添加如下内容：

```shell
export JAVA_HOME=/usr/local/jdk
export PATH=$JAVA_HOME/bin:$PATH
```

编辑完后按`esc--:wq`保存。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202305232145080.png" style="zoom:50%;" />

**重要：以下命令重载环境变量文件（让文件生效）**

```shell
source /etc/profile
```



**检测Java环境：**

```shell
java -version
```



![](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202305232148078.png)



## 4.编写Java文件测试

在任一目录中编写Java文件，此处名为`Test.java`，命令和文件内容如下：

- 命令

```shell
vim Test.java
```

- Test.java内容：

```java
public class Test {

        public static void main(String[] args) {

                System.out.println("HelloWorld!");
        }
}
```

编辑后esc--:wq保存退出。



**用如下命令编译测试：**

```java
javac Test.java 				# 编译文件
java Test						# 运行文件
```

![](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202305232154311.png)





# yum安装配置Java环境

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



