# Common-tools


## Nginx的安装过程
**1** 先安装相关的依赖 `yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel` ,
**2** 切换到安装文件的目录并且解压安装的压缩包 `tar -zxf nginx-1.26.2.tar.gz `,
**3** 进入到解压后的文件中找到其中的**configure**文件 执行 `./configure`,并且进行编译安装`make&&make install` ,
**4** 然后查找nginx的应用程序所在的位置 `whereis nginx`并且进入到这个文件中 并且进入到其中的**sbin**文件就可以找到nginx，直接运行`./nginx`如果没有报错就代表nginx安装成功 ,
**5** 这里我们也可以进行检查一下看看nginx能够正常运行 `curl http://localhost:80` .

## JDK的安装过程
**1** 先到JDK的官网上下载压缩包，这里给出[JDK网址](https://www.oracle.com/cn/java/technologies/downloads/),然后选择x64下的tar.gz的压缩包，
**2** 将这个压缩包放入服务器上然后解压 ` tar -zxvf jdk-22_linux-x64_bin.tar.gz `，
**3** 解压后，将Java环境变量部署到全局，先输入 `vim /etc/profile `，
**4** 然后将下面的配置加入到文件中
` JAVA_HOME=/usr/local/jdk-22.0.2  
  PATH=$PATH:$JAVA_HOME/bin
  export PATH JAVA_HOME `，这里注意JAVA_HOME下的值放的是你解压后文件所在地方，***切记***一定要记得修改，
**5** 最后执行` source /etc/profile `，
**6** 这里可以用` java -version `来检查是否安装成功，如果没有出现` -bash: java: command not found `，或者正确的显示了java的版本号，则表示安装成功.

## RabbitMQ的安装过程
**1** 先到RabbitMQ的官网下载rpm包 ` https://www.rabbitmq.com/docs/download `,
**2** 然后到` https://www.rabbitmq.com/docs/download `下载erlang的rpm包，并且将文件上传到Linux服务器上,
**3** 执行 `rpm -ivh erlang-26.2.1-1.el7.x86_64.rpm ` 和` yum install socat -y `以及` rpm -ivh rabbitmq-server-3.12.12-1.suse.noarch.rpm `,
**4** 然后设置开机自启动 ` chkconfig rabbitmq-server on `,
**5** 查看RabbitMQ的状态 `/sbin/service rabbitmq-server status`，**注意**这里就在rpm包的目录下执行即可,
**6** 启动RabbitMQ ` /sbin/service rabbitmq-server start `,
**7** 停止RabbitMQ ` /sbin/service rabbitmq-server stop `,
**8** 安装操作界面 ` rabbitmq-plugins enable rabbitmq_management `,
**9** 如果无法访问，可能是防火墙的原因，直接停止就可 `sytemctl stop firewalld `,
**10** RabbitMQ的登陆是需要账号的，所以这里设置一下账号 `rabbitmqctl list_users ` `rabbitmqctl add_user admin 123 ``rabbitmqctl set_user_tags admin administrator ``rabbitmqctl set_permissions -p "/" admin ".*" ".*" ".*"`.
**注意** 访问的时候应该为http://而不是https://，因为加了**s**之后会被置为无效连接.
## Sentinel的安装
**1** 先保证安装了java环境，没有的话参考之前的[JDK的安装过程](JDK的安装过程),
**2** 到官网安装压缩包 ` https://github.com/alibaba/Sentinel/releases/tag/1.8.8 `,
**3** 将文件上传到服务器，然后执行` https://github.com/alibaba/Sentinel/releases/tag/1.8.8 `,
**4** 启动完成后访问8080端口，初始账号和密码都是sentinel.

## Mysql的安装
**1** `sudo yum -y install wget `,`sudo yum update -y `,`sudo yum install -y gcc `,
**2** 到官网下载rpm包 ` wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm `,或者直接访问网站 `https://repo.mysql.com/ `,
**3** 将文件上传到服务器，并且 `rpm -ivh mysql57-community-release-el7-8.noarch.rpm `,
**4** 然后执行`cd /etc/yum.repos.d `，只要看到mysql存在，
**5** 安装mysql`rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022 `,然后` yum -y install mysql-server `,`systemctl start mysqld `,
**6** 查看mysql的状态 ` ps -ef | grep mysql `,
**7** 修改密码 ` grep 'temporary password' /var/log/mysqld.log `,找到临时密码，然后执行`mysql -uroot -p `,随后输入这个临时密码，
**8** 在学习的环境下我们可以设置密码简单一点，方便后面的操作,`set global validate_password_policy=LOW; `，这里注意这里进入的是mysql的语句所以后面的这个分号（；）很重要，设置密码` set global validate_password_length=5；`,` ALTER USER 'root'@'localhost' IDENTIFIED BY 'root(你的密码输入的地方，这里我们假设的是root)'; `
**9** 然后退出，重新登陆`
mysql -uroot -proot `,执行`show databases;use mysql;select User,Host from user；update user set Host='%' where User='root';flush privileges; `
    


