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
6. 配置：固态硬盘240G+机械硬盘3T, GPU:2080Ti(两个)
    分区：固态硬盘上 swap(交换空间) 60000MB(逻辑分区 空间起始位置 用于swap area)
	                              /boot 1000MB (逻辑分区 空间起始位置 用于EXT4日志文件系统)
								  固态硬盘上剩下的空间全给 / (主分区 空间起始位置 用于EXT4日志文件系统 挂载点 /)
               机械硬盘上 /home (逻辑分区 空间起始位置 ext4日志文件系统 挂载点/home)
	安装引导启动器的设备：固态硬盘上（或者/boot的位置）
   