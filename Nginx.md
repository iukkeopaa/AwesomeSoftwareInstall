## Nginx


#### Nginx的安装过程

> 先安装相关的依赖 ```yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel```
> 
>下载压缩包 网站地址 ```https://nginx.org/en/download.html```
>
>切换到安装文件的目录 
>
>解压下载的安装包 ```tar -zxf nginx-1.26.2.tar.gz ```
>
>进入解压后的文件夹中找到其中的 **configure**文件，执行```./configure```
,并且进行编译安装```make&&make install```
>
>查找Nginx的应用程序所在的位置```whereis nginx```,然后进入到这个文件夹中，找到其中的```sbin```文件夹，到这个文件夹中就可以找到Nginx的可执行文件
>
>此时如果没有出现报错就代表Nginx执行成功
>
>执行```ps -ef | grep nginx```,查看系统的进程中有没有Nginx
>
>到这里，Nginx一般在80端口运行，你可以执行```curl http://localhost:80```来访问应用.

## 参考资料

> https://redis.io/docs/latest/commands/



