## RabbitMQ

#### RabbitMQ的安装过程

>**1** 先到RabbitMQ的官网下载rpm包 ` https://www.rabbitmq.com/docs/download `,
>**2** 然后到` https://www.rabbitmq.com/docs/download `下载erlang的rpm包，并且将文件上传到Linux服务器上,
>**3** 执行 `rpm -ivh erlang-26.2.1-1.el7.x86_64.rpm ` 和` yum install socat -y `以及` rpm -ivh rabbitmq-server-3.12.12-1.suse.noarch.rpm `,
>**4** 然后设置开机自启动 ` chkconfig rabbitmq-server on `,
>**5** 查看RabbitMQ的状态 `/sbin/service rabbitmq-server status`，**注意**这里就在rpm包的目录下执行即可,
>**6** 启动RabbitMQ ` /sbin/service rabbitmq-server start `,
>**7** 停止RabbitMQ ` /sbin/service rabbitmq-server stop `,
>**8** 安装操作界面 ` rabbitmq-plugins enable rabbitmq_management `,
>**9** 如果无法访问，可能是防火墙的原因，直接停止就可 `sytemctl stop firewalld `,
>**10** RabbitMQ的登陆是需要账号的，所以这里设置一下账号 `rabbitmqctl list_users ` `rabbitmqctl add_user admin 123 ``rabbitmqctl set_user_tags admin administrator ``rabbitmqctl set_permissions -p "/" admin ".*" ".*" ".*"`.
**注意** 访问的时候应该为http://而不是https://，因为加了**s**之后会被置为无效连接.

> Rabbitmq的访问端口是15672
