## Redis

#### Redis的安装过程

> **1** 先下载压缩包 ` wget https://download.redis.io/releases/redis-7.2.4.tar.gz ` ,然后解压并且执行` make&&make install `,前提` yum install -y gcc tcl `
> **2** 进入到文件夹中。备份一个**redis.conf** ，`cp`,
> **3** `# 监听的地址，默认是127.0.0.1，会导致只能本地访问，修改为0.0.0.0则可以在任意IP访问，生产环境不要设置为0.0.0.0
bind 0.0.0.0
daemonize yes
requirepass 123321 `
> **4** 在conf的目录下启动` redis-server redis.conf ,输入` redis-cli `,` AUTH 密码 `
> **5** 将redis设置为开机自启
`vi /etc/systemd/system/redis.service`,
> **6** 输入一下内容

```[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/bin/redis-server /home/redis-7.2.0/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target `,`  systemctl daemon-reload ```