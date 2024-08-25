## Mongodb

#### Mongodb的安装过程

> **1** 先下载安装的压缩包 ` curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.3.tgz ` ***建议*** 切换到`/usr/local/`的目录下执行
> **2** 解压缩` tar zxvf mongodb-linux-x86_64-rhel70-4.0.3.tgz`
> **3** 将安装目录加载到全局`vim /etc/profile`,然后输入`export MONGODB_HOME=/usr/local/mongodb
export PATH=$PATH:$MONGODB_HOME/bin`，最后同样的常规操作执行`source /etc/profile`
> **4** 安装两个存储数据的文件夹`mkdir -p /data/mongodb`和`mkdir -p /data/mongodb/log`，并且在第二个log的文件夹中创建一个文件`touch /data/mongodb/log/mongod.log`
> **5** 切换到bin目录下，执行`./mongod --port=27017 --dbpath=/data/mongodb --logpath=/data/mongodb/log/mongod.log --bind_ip=0.0.0.0 --fork`
> **6** 执行` ps -ef |grep mongodb`查看是否正常运行
> **7** 启动MongoDB ` ./mongo`
**贴士** MongoDB和其他的数据库一样可以用可视化界面进行操作.