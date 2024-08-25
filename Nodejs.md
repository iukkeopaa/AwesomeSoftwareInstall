## Nodejs

#### Nodejs的安装过程


> **1** 先到官网下载压缩包 ` https://nodejs.org`，找到你要下载的版本，这里选择linux版x86版
> **2** 将压缩包上传到服务器
> **3** 执行` xz -d node-v9.3.0-linux-x64.tar.xz` ***注意***这里的版本一般安装最新的，因为很多应用在低版本中无法运行
> **4** `tar -xf node-v9.3.0-linux-x64.tar`
> **5** 最后执行`ln -s  /opt/nodeJs/bin/node /usr/bin/node
ln -s /opt/nodeJs/bin/npm /usr/bin/npm
ln -s /opt/nodeJs/bin/npm /usr/bin/npx
`
> **6** 最后执行`node `看到版本号就成功了。