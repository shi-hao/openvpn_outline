# 证书生成    
主要需要以下几个证书：    
根证书：用于签发客户端和服务端证书。    
服务端证书：使用根证书签发的服务端证书。    
客户端证书：使用根证书签发的客户端证书。    
每个证书都有对应的私钥，私钥必须妥善保存，不可泄露。    
  
## 2.1  Easy-rsa    
Easy-rsa是rsa证书生成工具，可以方便的生成rsa证书，生成方法可以查看Easy-rsa的github站点，或者百度。    
  
## 2.2  OpenSSL    
通过OpenSSL命令行脚本实现证书签发。    
  
### 2.2.1 rsa证书    
    
### 2.2.2 ecc证书    
    
### 2.2.3 sm2证书    
