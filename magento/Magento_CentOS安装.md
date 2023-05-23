# Magento_CentOS安装

背景信息：

- 操作系统：CentOS 7
- 镜像：阿里云
- IP：公网IP

示例步骤使用以下软件版本：

- Apache：2.4.6
- Mysql：5.7
- PHP：7.0
- Composer：1.8.5
- Magento：2.1

## 1.安装并配置Apache

- 安装Apache

```shell
yum install httpd -y
httpd -v
```

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658840.png" alt="image-20221106201148988" style="zoom:50%;" />

- 配置Apache

```shell
vim /etc/httpd/conf/httpd.conf

在Include conf.modules.d/*.conf的下一行，添加LoadModule rewrite_module modules/mod_rewrite.so。具体步骤如下：
1.移动光标到Include conf.modules.d/*.conf下一行的行首。
2.按下i键进入编辑模式。
3.输入LoadModule rewrite_module modules/mod_rewrite.so。
```

![image-20221106201448330](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658841.png)

- 将下列内容中的`AllowOverride None`更改为`AllowOverride All`。

```shell
# AllowOverride controls what directives may be placed in .htaccess files.
# It can be "All", "None", or any combination of the keywords:
# Options FileInfo AuthConfig Limit
#
#在行首添加#注释掉本行内容
#AllowOverride None

#添加下列内容
AllowOverride All
```

![image-20221108165041357](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658842.png)

按下`ESC`然后`:wq`保存退出。

- 运行以下命令启动Apache服务：

```shell
systemctl start httpd
```

- 运行以下命令添加Apache服务开机自启动：

```shell
systemctl enable httpd
```



## 2.安装并配置Mysql

- 安装Mysql:

  - 运行以下命令添加Mysql yum源：

  ```shell
  rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
  ```

  - 运行以下命令安装Mysql:

  ```shell
  yum -y install mysql-community-server --nogpgcheck
  ```

- 运行以下命令启动Mysql:

```shell
systemctl start mysqld
```

- 运行以下命令设置Mysql开机自启动：

```shell
systemctl enable mysqld
```

- 配置Mysql：

  - 运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码。

  ```shell
  grep 'temporary password' /var/log/mysqld.log
  ```

  返回的结果是：

  ```shell
  2022-11-06T12:24:24.653288Z 1 [Note] A temporary password is generated for root@localhost: kut0yhNKjB,q
  ```

  - 运行下列命令配置MySQL的安全性。

  ```shell
  mysql_secure_installation
  ```

  安全性的配置包含以下五个方面：

  1.设置root的账号密码：Ztr940407!

  ```shell
  Enter password for user root: #输入上一步中获取的root用户密码
  The 'validate_password' plugin is installed on the server.
  The subsequent steps will run with the existing configuration of the plugin.
  Using existing password for root.
  Estimated strength of the password: 100 
  Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
  New password: #输入密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
  Re-enter new password: #再次输入密码
  Estimated strength of the password: 100 
  Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
  ```

  2.输入`Y`删除匿名用户账号。

  ```shell
  By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
  Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  #是否删除匿名用户，输入Y
  Success.
  ```

  3.输入`Y`禁止root账号远程登录。

  ```shell
  Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
  Success.
  ```

  4.输入`Y`删除test库以及对test库的访问权限。

  ```shell
  Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
  - Dropping test database...
  Success.
  ```

  5.输入`Y`重新加载授权表。

  ```shell
  Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
  Success.
  All done!
  ```

  ![image-20221107161620966](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658844.png)



## 3.安装并配置PHP

- 安装PHP

  - 运行以下命令添加ius源。

  ```shell
  yum install \
  https://repo.ius.io/ius-release-el7.rpm \
  https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
  ```

  - 运行以下命令添加Webtatic源。

  ```shell
  # 安装epel-release
  yum -y install epel-release
  rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
  ```

  - 运行以下命令安装PHP7及所需扩展。

  ```shell
  yum install php
  
  yum -y install php70w php70w-pdo php70w-mysqlnd php70w-opcache php70w-xml php70w-gd php70w-mcrypt php70w-devel php70w-intl php70w-mbstring php70w-bcmath php70w-json php70w-iconv
  ```

  - 运行以下命令查看PHP版本。

  ```shell
  php -v
  ```

  ![image-20221107164850308](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658845.png)

- 配置PHP

  - 运行以下命令打开PHP配置文件。

  ```shell
  vim /etc/php.ini
  ```

  - 移动光标至最后一行的行尾。具体操作步骤如下：
    - 输入:$并回车，光标将移动至文件最后一行。
    - 按下$移动光标至行尾。
  - 按下i键进入编辑模式。
  - 在文件最后添加关于内存限制和时区的配置。

```shell
; 允许为PHP脚本分配的最大内存值。您可根据实际情况增加或减少内存限制
memory_limit = 1024M
; 设置时区为上海
date.timezone = Asia/Shanghai
```

- 按下`ESC`后输入`:wq`退出，并重启Apache服务。

```shell
systemctl restart httpd
```



## 4.创建Magento数据库

- 运行以下命令使用root用户和密码登录MySQL。

```shell
mysql -u root -p
```

- 运行以下命令创建`magento`数据库。

```shell
mysql> CREATE DATABASE magento; #根据实际情况将magento替换为您需要创建的数据库名称
```

- 依次运行以下命令为`magento`数据库创建用户。

```shell
mysql> GRANT ALL ON magento.* TO <YourUser>@localhost IDENTIFIED BY '<YourPass>'; #替换<YourUser>和<YourPass>为您需要创建的账号和密码
mysql> FLUSH PRIVILEGES;
```

例如，创建账号为`magentoUser`、密码为`magentoUser1@3`的用户，运行的命令为：(该教程直接以下面用户名和密码进行使用)

```shell
mysql> GRANT ALL ON magento.* TO magentoUser@localhost IDENTIFIED BY 'magentoUser1@3';
mysql> FLUSH PRIVILEGES;
```

- 输入exit并回车以退出MySQL。

![image-20221107170248097](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658846.png)

- **可选：**验证新建的Magento数据库和用户是否可用。具体步骤如下：

  - 运行以下命令使用新建账号和密码登录MySQL。

  ```shell
  mysql -u <YourUser> -p   #替换<YourUser>为您创建的账号
  ```

  - 运行以下命令查看新建的`magento`数据库。

  ```shell
  mysql> show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | information_schema |
  | magento            |
  +--------------------+
  2 rows in set (0.00 sec)
  ```

  - 运行以下命令并回车以退出MySQL。

  ```shell
  mysql> exit
  ```

  ![image-20221107170401790](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171658847.png)



## 5.安装并配置Composer

Composer是PHP的一个依赖管理工具。Composer允许您申明项目所依赖的代码库，并帮您在项目中安装依赖的代码库。

- 运行以下命令安装Composer。

```shell
curl -sS https://getcomposer.org/installer | php
```

- 运行以下命令配置Composer全局使用。

```shell
mv /root/composer.phar /usr/bin/composer
```

- 运行命令`composer -v`查看Composer版本。返回结果如下，表示Composer安装成功。

```shell
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.8.5 2019-04-09 17:46:47
                        
```

- **说明** 因最新版Composer与Magento暂不兼容，所以您需要安装与Magento兼容的Composer版本。你可以使用以下命令来让最新版Composer转换至兼容版本。如Composer 1.8.5版本。

```shell
composer self-update 1.8.5
```



## 6.安装配置Magento

您可以使用不同的方法安装Magento，可以选择是否安装示例数据。

- 如果安装Magento仅用于测试，您可以选择安装示例数据。
- 如果安装Magento用于生产环境，建议您安装全新的Magento，从头开始配置。

我们使用Git下载Magento，并使用Composer安装Magento的操作步骤。

- 下载Magento

  - 运行以下命令安装Git。

  ```shell
  yum -y install git
  ```

  - 进入Web服务器的默认根目录。

  ```shell
  cd /var/www/html/
  ```

  - 下载Magento。

  ```shell
  git clone https://github.com/magento/magento2.git
  ```

- **可选：**运行以下命令将Magento切换到稳定版本。

```shell
cd magento2 &&  git checkout tags/2.1.0 -b 2.1.0
```

命令执行后的结果如下：

```shell
Switched to a new branch '2.1.0'
```

**说明** 默认情况下，Git下载安装的Magento是最新的开发版本。如果您在生产环境中使用，建议切换到稳定版本，否则未来将无法升级安装。

- 运行以下命令将安装文件移到Web服务器根目录下。

```shell
shopt -s dotglob nullglob && mv /var/www/html/magento2/* /var/www/html/ && cd ..
```

**说明** 运行此命令后，您可以通过`https://<ECS实例公网IP地址>`访问您的Magento站点。否则，您只能通过`https://<ECS实例公网IP地址>/magento2`访问。

- 依次运行下列命令为Magento文件设置适当的权限。

```shell
chown -R :apache /var/www/html

find /var/www/html -type f -print0 | xargs -r0 chmod 640

find /var/www/html -type d -print0 | xargs -r0 chmod 750

chmod -R g+w /var/www/html/{pub,var}

chmod -R g+w /var/www/html/{app/etc,vendor}

chmod 750 /var/www/html/bin/magento
```

- 运行命令**composer install**安装Magento。

```shell
composer install
```



## 7.配置Magento客户端

1. 打开浏览器。

2. 在浏览器地址栏中，输入`http://<ECS实例公网IP地址>/setup`。

   出现如下图所示页面，表示Magento安装成功。

   ![magento_3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p12145.png)

3. 单击**Agree and Setup Magento**开始配置Magento。具体步骤如下：

   1. 准备性检查。

      1. 单击**Start Readiness Check**。
      2. 检查完成后，单击**Next**。

      ![magento-check](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p44785.png)

   2. 添加数据库。

      1. 输入之前创建的数据库用户的账号和密码。本教程中创建的示例用户账号为`magentoUser`、密码为`magentoUser1@3`。
      2. 输入之前创建的数据库的名字。本教程中创建的示例数据库名字为`magento`。
      3. 单击**Next**。

      ![config-db](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p44786.png)

   3. 填写Web访问设置，并单击**Next**。

      ![config-web](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p44787.png)

   4. 填写定制商店，并单击**Next**。

   5. 填写管理员账号信息，并单击**Next**。

   6. 单击**Install Now**进行安装。

出现如下图所示界面，表示Magento配置完成。![magento_4](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p12146.png)

## 8.添加cron作业

完成以下操作，添加cron作业：

1. 运行**crontab -u apache -e**设置cron运行调度工作。

2. 按下i键进入编辑模式。

3. 输入下列配置信息。

   ```javascript
   */10 * * * * php -c /etc /var/www/html/bin/magento cron:run
   */10 * * * * php -c /etc /var/www/html/update/cron.php
   */10 * * * * php -c /etc /var/www/html/bin/magento setup:cron:run
   ```

4. 按下Esc键后，输入:wq并回车以保存并退出。

Magento上使用cron作业的更多详情，请参见[Magento官方文档](https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cron.html)。

## 常见问题

输入`http://<ECS实例公网IP地址>/admin`登录Magento后台，如果界面提示“One or more indexers are invalid. Make sure your Magento cron job is running.”的错误信息，请参考以下步骤解决问题。![123](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5250281561/p436240.png)

1. 远程连接Magento服务器。具体操作，请参见[连接方式概述](https://help.aliyun.com/document_detail/71529.htm#concept-tmr-pgx-wdb)。

2. 运行以下命令，将PHP的安装路径建立软连接至

   /usr/sbin/php

   目录下。

   ```bash
   ln -s /usr/local/php/bin/php /usr/sbin/php
   ```

3. 运行以下命令，刷新索引。

   ```bash
   cd /yjdata/www/wwwroot
   php bin/magento indexer:reindex
   ```

   回显信息类似如下所示，表示索引已刷新成功。

   ```sql
   [root@iZbp1h2mquu8nb0jz99**** wwwroot]# php bin/magento indexer:reindex
   Design Config Grid index has been rebuilt successfully in 00:00:00
   Customer Grid index has been rebuilt successfully in 00:00:00
   Category Products index has been rebuilt successfully in 00:00:00
   Product Categories index has been rebuilt successfully in 00:00:00
   Product Price index has been rebuilt successfully in 00:00:00
   Product EAV index has been rebuilt successfully in 00:00:00
   Stock index has been rebuilt successfully in 00:00:00
   Catalog Rule Product index has been rebuilt successfully in 00:00:00
   Catalog Product Rule index has been rebuilt successfully in 00:00:00
   Catalog Search index has been rebuilt successfully in 00:00:00
   ```

4. 刷新页面后，单击**Cache Management**。![daad](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5250281561/p436268.png)

5. 选中状态为**INVALIDATED**的**Cache Types**，并单击**Submit**。![456](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5250281561/p436272.png)当出现类似如下返回信息时，表示问题已经解决。![455](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5344512561/p437601.png)

## 后续步骤

- 访问`http://<ECS实例公网IP地址>`可以看到如下图所示的默认主页。![luma](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p12147.png)
- 访问`http://<ECS实例公网IP地址>/admin`，输入您在安装过程中设置的用户名和密码，成功登录管理面板后可看到如下界面。![dashboard](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5312649951/p12148.png)