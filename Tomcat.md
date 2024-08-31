## Tomcat

#### Tomcat的安装过程

> 先到官网安装压缩包 `https://archive.apache.org/dist/tomcat/tomcat-8/`，然后点击`bin`，找到压缩包下载方式,也就是下载后缀为`tar.gz`的压缩包，这里可以将鼠标放在这个压缩包上然后复制这个链接
> 
> 到服务器上执行`wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.92/bin/apache-tomcat-8.5.92.tar.gz`
>
> tar -zxvf apache-tomcat-8.5.92.tar.gz
>
> 进入到`bin`目录下
> 
> 执行`./startup.sh`
>
> 你可以执行`curl http://localhost:8080`或者直接在地址栏中输入`你的服务器地址+8080`，如果没有出现报错则表示安装成功