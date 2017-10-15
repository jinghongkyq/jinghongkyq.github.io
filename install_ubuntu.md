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
