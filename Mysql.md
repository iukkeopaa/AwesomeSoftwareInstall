## Mysql
#### Mysql的安装过程

> **1** `sudo yum -y install wget `,`sudo yum update -y `,`sudo yum install -y gcc `,
> **2** 到官网下载rpm包 ` wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm `,或者直接访问网站 `https://repo.mysql.com/ `,
> **3** 将文件上传到服务器，并且 `rpm -ivh mysql57-community-release-el7-8.noarch.rpm `,
> **4** 然后执行`cd /etc/yum.repos.d `，只要看到mysql存在，
> **5** 安装mysql`rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022 `,然后` yum -y install mysql-server `,`systemctl start mysqld `,
> **6** 查看mysql的状态 ` ps -ef | grep mysql `,
> **7** 修改密码 ` grep 'temporary password' /var/log/mysqld.log `,找到临时密码，然后执行`mysql -uroot -p `,随后输入这个临时密码，
> **8** 在学习的环境下我们可以设置密码简单一点，方便后面的操作,`set global validate_password_policy=LOW; `，这里注意这里进入的是mysql的语句所以后面的这个分号（；）很重要，设置密码` set global validate_password_length=5；`,` ALTER USER 'root'@'localhost' IDENTIFIED BY 'root(你的密码输入的地方，这里我们假设的是root)'; `
> **9** 然后退出，重新登陆`
mysql -uroot -proot `,执行`show databases;use mysql;select User,Host from user；update user set Host='%' where User='root';flush privileges; `
>
> 下面将解决远程登录mysql报1130错误，这个错误根本就是没有授权
> **1** use mysql
> **2** SELECT User, Host FROM user
> **3** update user set host ='%' where user ='root';
> **4** FLUSH PRIVILEGES;  这一步很重要不要忘记了
> **5** systemctl stop firewalld
> **6** systemctl disable firewalld

