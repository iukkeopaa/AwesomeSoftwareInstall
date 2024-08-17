# Common-tools


## Nginx的安装过程
**1** 先安装相关的依赖 `yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel` ,
**2** 切换到安装文件的目录并且解压安装的压缩包 `tar -zxf nginx-1.26.2.tar.gz `,
**3** 进入到解压后的文件中找到其中的**configure**文件 执行 `./configure`,并且进行编译安装`make&&make install` ,
**4** 然后查找nginx的应用程序所在的位置 `whereis nginx`并且进入到这个文件中 并且进入到其中的**sbin**文件就可以找到nginx，直接运行`./nginx`如果没有报错就代表nginx安装成功 ,
**5** 这里我们也可以进行检查一下看看nginx能够正常运行 `curl http://localhost:80` .
