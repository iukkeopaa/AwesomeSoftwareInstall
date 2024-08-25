## JDK

#### JDK的安装过程

> 先到JDK的官网上下载压缩包，地址为```https://www.oracle.com/cn/java/technologies/downloads/```，这里选择`x64`下的`tar.gz`的压缩包
>
>**这里假设安装到云服务器上**
>
>将刚刚下载的压缩包上传到云服务上，然后解压```tar -zxvf jdk-22_linux-x64_bin.tar.gz```
>
>解压之后，将JAVA环境环境变量配置到全局
>
>输入```vim /etc/profie```
>
>在这个profile文件中输入
>
>```JAVA_HOME=/usr/local/jdk-22.0.2 ```**这里JAVA的要根据你下载的位置进行调整**
>```PATH=$PATH:$JAVA_HOME/bin export PATH JAVA_HOME``` **这个变量可以保持不变**
>
>配置完了之后执行```source /etc/profile```
>
>你可以执行```java --version```来检查是否安装成功，如果没有出现```-bash: java: command not found```,或者正确的显示了JAVA的版本号，则表示安装成功.