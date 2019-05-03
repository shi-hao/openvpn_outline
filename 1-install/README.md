# OpenVPN软件安装    
linux源码安装软件，基本都是三步走，config，make，make install，即：配置，编译，安装。    
config配置时，可以使用config --help来查看帮助。    
编译时，如果系统缺少软件依赖的库，会报错，按需满足软件要求即可。软件在安装时主要做一件事情，  
将软件的可执行文件，库文件，头文件，说明文档复制到安装目录相应的bin（或者sbin），lib，include，man目录下。    

## 1.1 OpenSSL
Ubuntu本身系统有自带的OpenSSL库。  
查看当前系统的openssl版本:
<pre>
bleach@user-PC:~/myproject/openvpn_outline/doc$ openssl version
OpenSSL 1.0.2g  1 Mar 2016
</pre>
可以选择使用apt升级，也可以选择使用源码升级OpenSSL版本。    

**Ubuntu18下源码安装OpenSSL**  
(1)下载源码  
通过github下载源代码 https://github.com/openssl/openssl ，选择master分支的OpenSSL_1_1_1-stable版本，
下载zip包。

(2)配置源码  
**./config  shared  --prefix=/usr**     
shared参数表示生成共享库，也就是生成动态库，--prefix指定安装的路径。    

(3)编译安装  
**make**     
**make install**   
可能需要root权限，sudo make install，安装完毕后，系统/usr/local/bin和/usr/local/lib目录下会分别生成  
openssl执行文件和动静态库文件（libcrypto.a libssl.a和libcrypto.so libssl.so）。    
注意系统本身可能已经安装有openssl，一般会安装在目录/usr目录下（/usr/bin  /usr/lib），如果是Ubuntu的系统，  
可以使用apt-get remove掉安装的版本，也可以在编译时指定安装目录--prefix=/usr，安装后覆盖掉原先的文件。    
<pre>
./config shared --prefix=/usr
make 
make install
</pre>


## 1.2 OpenVPN
**Ubuntu18下安装OpenVPN2.4**  
(1)下载源码
通过github下载源码，https://github.com/OpenVPN/openvpn ，选择master分支的release/2.4版本，  
下载zip包。  

(2)配置源码  
OpenVPN2.4版本的源码下没有配置文件，需要生成，生成配置文件需要以下软件包。  
安装编译工具：  
sudo apt-get install build-essential autoconf pkg-config  
安装依赖包：  
sudo apt-get install liblzo2-dev libtool  libpam0g-dev libsystemd-dev  
OpenVPN同时依赖OpenSSL的2个动态库libssl和libcrypto，所以OpenSSL必须要正确安装。  

**aureconf -vif**   
生成配置文件。  
**./configure --prefix=/usr**  
配置源码  

(3)编译安装  
**make**    
**sudo make install**    
<pre>
aureconf -vif
./configure --prefix=/usr 
make 
make install
</pre>
