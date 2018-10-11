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
