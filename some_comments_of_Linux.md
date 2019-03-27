#### Some comments in Linux

**the size of file/folder**   
  `du -h file1/file.txt` or `du -sh file1/file.txt`      
**information of each hard disk**   
  `df -h`      
**the size of each folder/file in this path**  
  `du -h --max-depth=1`  
**copy file/folder**   
  `cp file1 file2`    
**move file/folder**   
  `mv file1 file2`    
**remove file**   
  `rm file.txt`    
**remove folder**   
  `rm -r folder`    
**list**   
  `ls` `ls -l`    
**how many folders/files in this folder**   
  `ls -l|wc -l`    
**set gpu id in pytorch**   
  `CUDA_VISIBLE_DIVICES=id python train1.py`    
**look up anaconda enviornment**  
  `conda env list`

  cite https://www.jianshu.com/p/54181deedd42
  
  **显示进程运行的CPU**  
  `taskset -p 21184`
  显示结果：pid 21184's current affinity mask: ffffff  
注：21184是redis-server运行的pid
      显示结果的ffffff实际上是二进制24个低位均为1的bitmask，每一个1对应于1个CPU，表示该进程在24个CPU上运行
  **指定进程在哪个cpu上运行**
  `taskset -pc 3 21184`
显示结果：
pid 21184's current affinity list: 0-23
pid 21184's new affinity list: 3

注：3表示CPU将只会运行在第4个CPU上（从0开始计数）。
**进程启动时指定CPU**
`taskset -c 1 ./redis-server ../redis.conf` 
