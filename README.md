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

## Redis的安装
**1** 先下载压缩包 ` wget https://download.redis.io/releases/redis-7.2.4.tar.gz ` ,然后解压并且执行` make&&make install `,前提` yum install -y gcc tcl `
**2** 进入到文件夹中。备份一个**redis.conf** ，`cp`,
**3** `# 监听的地址，默认是127.0.0.1，会导致只能本地访问，修改为0.0.0.0则可以在任意IP访问，生产环境不要设置为0.0.0.0
bind 0.0.0.0
daemonize yes
requirepass 123321 `
**4** 在conf的目录下启动` redis-server redis.conf ,输入` redis-cli `,` AUTH 密码 `
**5** 将redis设置为开机自启
`vi /etc/systemd/system/redis.service`,` [Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/bin/redis-server /home/redis-7.2.0/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target `,`  systemctl daemon-reload `

## Mycat的安装
**1** 官网下载压缩包 ` https://download.topunix.com/MySQL/Software-Cluster/Software-Mycat/ `
**2** 上传压缩包到服务器，然后解压缩` tar -zxvf Mycat-server-1.6.7.4-release-20200105164103-linux.tar.gz `
**3** 添加` export MYCAT_HOME=/usr/local/mycat `到` /etc/profile/`
**4** 执行` source /etc/profile`
**5** 进入到bin目录，启动`./mycat start`,并且查看状态`./mycat status`,如果显示正在running则表示安装成功.

## MongoDB的安装
**1** 先下载安装的压缩包 ` curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.3.tgz ` ***建议*** 切换到`/usr/local/`的目录下执行
**2** 解压缩` tar zxvf mongodb-linux-x86_64-rhel70-4.0.3.tgz`
**3** 将安装目录加载到全局`vim /etc/profile`,然后输入`export MONGODB_HOME=/usr/local/mongodb
export PATH=$PATH:$MONGODB_HOME/bin`，最后同样的常规操作执行`source /etc/profile`
**4** 安装两个存储数据的文件夹`mkdir -p /data/mongodb`和`mkdir -p /data/mongodb/log`，并且在第二个log的文件夹中创建一个文件`touch /data/mongodb/log/mongod.log`
**5** 切换到bin目录下，执行`./mongod --port=27017 --dbpath=/data/mongodb --logpath=/data/mongodb/log/mongod.log --bind_ip=0.0.0.0 --fork`
**6** 执行` ps -ef |grep mongodb`查看是否正常运行
**7** 启动MongoDB ` ./mongo`
**贴士** MongoDB和其他的数据库一样可以用可视化界面进行操作.

## SQLite的安装
目前，几乎所有版本的 Linux 操作系统都附带 SQLite。所以，只要使用下面的命令来检查您的机器上是否已经安装了 SQLite。

## Nodejs的安装
**1** 先到官网下载压缩包 ` https://nodejs.org`，找到你要下载的版本，这里选择linux版x86版
**2** 将压缩包上传到服务器
**3** 执行` xz -d node-v9.3.0-linux-x64.tar.xz` ***注意***这里的版本一般安装最新的，因为很多应用在低版本中无法运行
**4** `tar -xf node-v9.3.0-linux-x64.tar`
**5** 最后执行`ln -s  /opt/nodeJs/bin/node /usr/bin/node
ln -s /opt/nodeJs/bin/npm /usr/bin/npm
ln -s /opt/nodeJs/bin/npm /usr/bin/npx
`
**6** 最后执行`node `看到版本号就成功了。


