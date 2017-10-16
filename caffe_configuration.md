## 配置Caffe
[参考xiaobai1217.github.io](https://xiaobai1217.github.io/2017/04/18/caffe_configuration/)
[参考dangbiao1991](https://gist.github.com/dangbiao1991/7825db1d17df9231f4101f034ecd5a2b)

### 准备工作
* 下载CUDA
![cuda](http://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/data/cuda.png)

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

### 安装CUDA
```
cd Downloads
ls
sudo chmod +x cuda_9.0.176_384.81_linux.run
sudo ./cuda_9.0.176_384.81_linux.run
```
然后会先出现许可文件，按任意键一直滑到最后，然后会显示
Do you accept the previously read EULA?
输入 accept
然后会有一系列选项，第一项是Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 367.48?这个选项是问你是否安装cuda自带的显卡驱动，因为我们刚才已经安装过显卡驱动，所以这里输入no
剩下的选项都输入y或者回车表示用默认选项，如图所示
![cudaim](http://github.com/jinghongkyq/jinghongkyq.github.io/raw/master/data/cudaim.png)

安装完成后输入sudo service lightdm start 回到图形界面。

**配置环境变量**

ctrl+alt+t 打开终端，然后输入sudo gedit ~/.bashrc
在打开的文件最后添加如下两行
```
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
保存后关闭
终端中输入使环境变量生效 ```source ~/.bashrc```
然后终端中输入 ```sudo gedit /etc/ld.so.conf```
在文件最后添加这条语句 ```/usr/local/cuda/lib64``` 然后保存关闭
终端中输入 ```sudo ldconfig```
接着输入 ```sudo ldconfig -v|grep cuda```

### 安装编译`Caffe`
* Caffe依赖库安装
```
sudo apt-get install libatlas-base-dev
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler
```

* Caffe编译
1. 下载Caffe `git clone https://github.com/BVLC/caffe.git`
2. 修改 `Makefile.config` 文件
```
cd /home/你的用户名/caffe
cp Makefile.config.example Makefile.config
gedit Makefile.config
```

改这里

```
# This is required only if you will compile the matlab interface.
# MATLAB directory should contain the mex binary in /bin.
MATLAB_DIR := /usr/local/MATLAB/R2015b
# MATLAB_DIR := /Applications/MATLAB_R2012b.app

WITH_PYTHON_LAYER:=1
```

3. 编译
```
make all -j
make matcaffe
```
可能会出现gcc版本的问题无法编译`matcaffe`,系统自带gcc版本是4.8,而MATLAB2015b支持gcc4.7,参考[How to switch your gcc/g++ version in ubuntu](https://archerfmy.github.io/2017/04/12/How-to-switch-your-gcc-g-version-in-ubuntu/)切换到gcc4.7版本（4.8也在）。
注意gcc和g++版本要一致。
```
sudo apt-get install gcc-4.7 gcc-4.7-multilib g++-4.7 g++-4.7-multilib

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50  #后面数字是优先级
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.7 40
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.7 40

sudo update-alternatives --config gcc  #点Enter
sudo update-alternatives --config g++
```

重新编译caffe
```
make clean
make all -j
make matcaffe
make mattest
make pycaffe
```


