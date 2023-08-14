# CentOS安装MySQL

## 1.安装前准备

查看当前自带mariadb

```shell
rpm -qa | grep mariadb
```

![image-20230614164511292](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202306141645409.png)

卸载：

```shell
rpm -e --nodeps 文件名
```

卸载完成后检查是否卸载干净：

```shell
rpm -qa|grep mariadb
```



## 2.安装MySQL

本次采用wget下载方式：

```shell
yum install -y wget					# 下载wget
wget https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.30-el7-x86_64.tar
```



解压：

```shell
cd /usr/local/
tar -xvf mysql-8.0.30-el7-x86_64.tar
tar -zxvf mysql-8.0.30-el7-x86_64.tar.gz
mv mysql-8.0.30-el7-x86_64/ mysql				# 重命名

```

