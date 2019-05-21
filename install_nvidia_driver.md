# UBUNTU16.04 安装NVIDIA显卡驱动
* 下载NVIDIA Driver
![nvidia](http://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/data/nvidia.png)

* 把两个文件放在Downloads文件夹下，安装必要的库
```
sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev libgl1-mesa-glx
```

### Ubuntu 16.04安装NVIDIA Driver
显卡型号 GTX1080，先切换到撞断界面(Ctrl+Alt+F1)

* 卸载可能存在的旧版本 nvidia 驱动（对没有安装过 nvidia 驱动的主机，这步可以省略，但推荐执行，无害）
```
sudo apt-get remove --purge nvidia*
```

* 安装驱动可能需要的依赖(可选)
```
sudo apt-get update
sudo apt-get install dkms build-essential linux-headers-generic
```

* 把 nouveau 驱动加入黑名单
```
sudo nano /etc/modprobe.d/blacklist-nouveau.conf
```

* 在文件 blacklist-nouveau.conf 中加入如下内容：
```
  blacklist nouveau
  blacklist lbm-nouveau
  options nouveau modeset=0
  alias nouveau off
  alias lbm-nouveau off
```

* 禁用 nouveau 内核模块
```
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
sudo update-initramfs -u
```

* 重启，再次进入字符终端界面，并关闭图形界面
```
sudo service lightdm stop
```

* 安装驱动
```
sudo chmod u+x NVIDIA-Linux-x86_64-361.45.11.run
sudo ./NVIDIA-Linux-x86_64-361.45.11.run
```

**注意**
一路选continue和ok，到下面这个界面的时候选NO。
![no](http://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/data/no.png)

* 重启

* 安装完毕