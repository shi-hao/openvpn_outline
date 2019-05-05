# OpenSSL  
  
  
  
  
## Troubleshooting  
1.通过源码升级系统的OpenSSL  
因为要升级OpenVPN的密码库，所以在ubuntu18.04系统上安装了自己重新编译的OpenSSL库，即，    
将系统本身的OpenSSL全部删除，包括bin和lib，然后安装了新的OpenSSL。结果系统几款软件都崩溃了。    
(1)ssh无法使用，提示找不到OpenSSL库。    
(2)apt也异常，报错。    
  
问题分析：    
因为Ubuntu系统的好多软件都用到了OpenSSL，而系统的这些软件是官方使用特定的OpenSSL版本去    
编译的，而升级了系统的OpenSSL之后，这些软件无法动态链接OpenSSL库。    
大体的调用关系如下：    
OpenSSL --> ssh --> apt(openssh-server)    
ssh使用了OpenSSL，apt则使用了ssh的openssh-server，算是连锁问题吧。    
  
  
问题解决办法：    
重新编译openSSH，覆盖安装。    
  
  
遇到的问题：    
从官网下载了几个版本的OpenSSH和OpenSSL，安装哪个版本是个问题。    
(1)安装了最新版本的OpenSSL，却发现在编译OpenSSH时，提示不支持最新版本。    
(2)安装相对较老的OpenSSL，OpenSSH编译通过了，但是apt在调用OpenSSH-server时，老是提示服务启动    
失败。    
(3)最后，根据Ubuntu18.04的发布时间，也就是2018年4月，选择了2017年的OpenSSH版本，编译通过     
问题解决。    
  
  
