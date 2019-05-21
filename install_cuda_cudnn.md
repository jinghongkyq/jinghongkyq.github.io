# UBUNTU16.04 安装CUDA9.0+CUDNN7.0

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


### 安装CUDNN

（参考[cite](https://blog.csdn.net/fdqw_sph/article/details/78745375)）
1. Ctrl+alt+F1进入的字符界面  
2. 解压 cudnn.tgz文件为cuda文件夹，即  
```
tar -zxvf cudnn-9.0-linux-x64-v7.0.tgz
cd cuda
sudo cp lib64/lib* /usr/local/cuda/lib64/    
sudo cp include/cudnn.h /usr/local/cuda/include/ 
```
3. 然后更新网络连接：  
```
cd /usr/local/cuda/lib64/  
sudo chmod +r libcudnn.so.7.0.3  # 自己查看.so的版本  
sudo ln -sf libcudnn.so.7.0.3. libcudnn.so.7  
sudo ln -sf libcudnn.so.7 libcudnn.so  
sudo ldconfig  
```
4. 重新启动图形化界面  
```
sudo service lightdm start
```
5. 按Ctrl+alt+F7退出Text Mode