## Mycat 

#### Mycat的安装过程

> **1** 官网下载压缩包 ` https://download.topunix.com/MySQL/Software-Cluster/Software-Mycat/ `
> **2** 上传压缩包到服务器，然后解压缩` tar -zxvf Mycat-server-1.6.7.4-release-20200105164103-linux.tar.gz `
> **3** 添加` export MYCAT_HOME=/usr/local/mycat `到` /etc/profile/`
> **4** 执行` source /etc/profile`
> **5** 进入到bin目录，启动`./mycat start`,并且查看状态`./mycat status`,如果显示正在running则表示安装成功.
