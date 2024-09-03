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

```


## 资料参考

> https://www.cnblogs.com/Lin1031/p/15743385.html
>
> https://www.runoob.com/redis/redis-tutorial.html
>
> http://doc.redisfans.com/
>
> https://redis.io/docs/latest/commands/


## Redis中遇到的问题

`nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] still could not bind()`

> sudo netstat -tulnp | grep :80  或者 sudo lsof -i :80
> ./nginx -s stop
> ./nginx


`
Job for nginx.service failed because the control process exited with error code. See "systemctl status nginx.service" and "journalctl -xe" for details.
`

> nginx -t
> netstat -tnlp
> pkill -9 nginx
> ./nginx

## 使用第三方可视化软件的注意点

RESP

> 在URL中输入 `redis://你的地址:端口号`
>
> `连接设置` 有密码输入密码，没有不用输入，用户名一般为空，不用输入

Redis insight

> 切记！！！没用用户名不用输入
> 
> **这里在主从复制的时候有个很大的坑**
>
> `我们在配置好了主从复制的相关信息之后我们要执行kill 来结束进程，然后再重启`

