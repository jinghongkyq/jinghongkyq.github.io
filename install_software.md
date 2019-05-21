# Ubuntu安装软件
[Ubuntu 装机后必须要做的事情](http://gaobb.github.io/2016/07/20/ubuntu%E8%A3%85%E6%9C%BA%E5%BF%85%E5%B9%B2%E7%9A%84%E4%BA%8B%E6%83%85/)
* 更新与升级  
```
sudo apt-get update && sudo apt-get dist-upgrade  
```

* 安装Chrome浏览器  
下载chrome.deb安装包  
```
sudo dpkg -i chrome.deb
```

* 安装vim  
```
sudo apt-get -f install
sudo apt-get -f install vim
```

* 安装pdf阅读器  
```
sudo apt-get install okular
```

* 安装福昕阅读器  
```
chmod u+x foxit.run
./foxit.run
```

* 安装配置git服务器  
```
sudo apt-get install git
```

* 安装rar  
```
sudo apt-get install rar
sudo apt-get install unrar
```

* 解压rar文件  
```
rar e 11.rar  # 全部文件解压到当前路径，不保存文件夹结构
rar x 11.rar  # 解压到当前路径，保存文件夹结构
```

* 安装有道词典  
[ubuntu16.04有道词典安装方法](https://www.jianshu.com/p/815c8a7a75c8)

* 安装搜狗输入法  
[ubuntu16.04搜狗输入法安装方法](https://blog.csdn.net/Areigninhell/article/details/79696751)

* 安装MATLAB2015b
参考[xiaobai1217.github.io](https://xiaobai1217.github.io/2017/04/18/caffe_configuration/)
1. 将安装包'R2015b_glnxa64.iso'和'Crack'放在Downlows文件夹下
2. 在Downloads文件夹下新建文件夹`tmp`，并将镜像文件`R2015b_glnxa64.iso`挂载在`tmp`文件夹下
```
cd Downloads
sudo mount -o loop R2015b_glnxa64.iso ./tmp
```
3. 安装
```
./tmp/install
sudo chown -R 你的用户名 /usr/local/
sudo chgrp -R 你的用户名 /usr/local/
```
4. 打开matlab安装界面,首先选择文件秘钥安装方式,根据Crack文件夹下的readme填入秘钥.
5. 安装完成后将Crack文件夹中的`libmwservices.so`复制到安装路径下`/usr/local/MATLAB/R2015b/bin/glnxa64/`,替换该路径下的`libmwservices.so`.
6. 做一些配置工作,打开`~/.bashrc`
```
sudo gedit ~/.bashrc
```
找到下面几行
```
# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
```
在这几行之后添加一行`alias matlab='/usr/local/MATLAB/R2015b/bin/matlab' `然后保存关闭.重新打开一个命令行，然后输入matlab应该就可以直接开启matlab.

