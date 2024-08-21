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
**3** 解压后，将Java环境变量部署到全局，先输入 `cd /etc/profile `，
**4** 然后将下面的配置加入到文件中
` JAVA_HOME=/usr/local/jdk-22.0.2  
  PATH=$PATH:$JAVA_HOME/bin
  export PATH JAVA_HOME `，这里注意JAVA_HOME下的值放的是你解压后文件所在地方，***切记***一定要记得修改，
**5** 最后执行` source /etc/profile `，
**6** 这里可以用` java -version `来检查是否安装成功，如果没有出现` -bash: java: command not found `，或者正确的显示了java的版本号，则表示安装成功。

## RabbitMQ的安装过程
**1** 先到RabbitMQ的官网下载rpm包 ` https://www.rabbitmq.com/docs/download `
**2** 然后到` https://www.rabbitmq.com/docs/download `下载erlang的rpm包，并且将文件上传到Linux服务器上
**3** 执行 `rpm -ivh erlang-26.2.1-1.el7.x86_64.rpm ` 和` yum install socat -y `以及` rpm -ivh rabbitmq-server-3.12.12-1.suse.noarch.rpm `
**4** 然后设置开机自启动 ` chkconfig rabbitmq-server on `
**5** 查看RabbitMQ的状态 `/sbin/service rabbitmq-server status`，**注意**这里就在rpm包的目录下执行即可
**6** 启动RabbitMQ ` /sbin/service rabbitmq-server start `
**7** 停止RabbitMQ ` /sbin/service rabbitmq-server stop `
**8** 安装操作界面 ` rabbitmq-plugins enable rabbitmq_management `
**9** 如果无法访问，可能是防火墙的原因，直接停止就可 `sytemctl stop firewalld `
**10** RabbitMQ的登陆是需要账号的，所以这里设置一下账号 `rabbitmqctl list_users ` `rabbitmqctl add_user admin 123 ``rabbitmqctl set_user_tags admin administrator ``rabbitmqctl set_permissions -p "/" admin ".*" ".*" ".*"`

    


