# 1.client分配固定ip    
根据client证书的名称，server给其分配固定的IP地址    
  
(1)创建client目录  
创建一个目录，用于存放连接到server的client的配置，如下。  
  
**/home/client_cnf**  
  
(2)修改server端配置  
在server端的配置文件中增加如下一行  
  
**client-config-dir /home/client_cnf**  
  
(3)查看客户端证书名称  
使用openssl指令查看证书名称信息。  
  
**openssl x509 -subject -noout -in client1.crt**  
**subject= /C=NL/O=Cookbook/CN=openvpnclient1/emailAddress=...**  

证书名称为openvpnclient1  
  
(4)创建client配置文件  
在路径/home/client_cnf下面创建文件与证书名称相同的文件openvpnclient1  
并将以下内容写入该文件。  
  
**ifconfig-push ip1  ip2**  

ip1和ip2分别是分配给client的虚拟设备的ip地址，如果是client是win客户端，那么ip1和ip2需要设置不同  
的ip  


## 2.client访问server端子网

