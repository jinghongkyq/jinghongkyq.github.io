# 安装UBUNTU教程
[Ubuntu 16.04 U盘安装图文教程](http://www.linuxidc.com/Linux/2016-04/130520.htm)

### 安装Ubuntu
1. 在windows下制作U盘操作系统安装工具
2. 打开电脑按DEL键（不同电脑不一样，也有可能是ESC，F1...）。进入BIOS里设置为U盘启动。
   BOOT -- Hard Disk Drives (USB)
           Boot Device Priority (USB)
   F10 保存。
3. 选Try Ubuntu without installing或Install Ubuntu.
4. 进入桌面后点 Install Ubuntu 16.04.3 LTS 开始安装。
5. 选语言（English）
   什么都不选 （选项有1. download updates while installing Ubuntu和Install third-party software for ----）
   Installation type 根据情况选，如果是windows和linux双系统，选something else.
   选时区 填名字 安装。
   
### 安装软件
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

* 安装配置git服务器
```
sudo apt-get install git
```

* 安装rar
```
sudo apt-get install rar
sudo apt-get install unrar
```

解压rar文件
```
rar e 11.rar  # 全部文件解压到当前路径，不保存文件夹结构
rar x 11.rar  # 解压到当前路径，保存文件夹结构
```

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

