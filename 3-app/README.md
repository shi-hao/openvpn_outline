# OpenVPN Practical Configuration  

## client分配固定ip    
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


## client之间互联互通



## client和server所在子网互联互通
### client访问server端子网
(1)push server端子网到client 
在server配置文件中增加如下配置
**push "route  ip  mask"**
此语句的含义是，当client连接上server后，server推送路由配置给client。

(2)开启server端ip转发功能
打开/etc/sysctl.conf，打开注释，net.ipv4.ip_forward=1
运行如下指令，使配置生效。
sudo /sbin/sysctl -p
此操作的目的是，当server收到数据包后，将数据包转发出去。

(3)server端子网设备增加静态路由
