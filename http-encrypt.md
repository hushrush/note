
# http中的加密
+ 浏览器获取网站的证书
+ 浏览器检查是否是可信证书，从证书中获取公钥
+ 浏览器生成对称加密密钥，用公钥加密对称加密密钥，发给服务器，这样只有服务器可以解开
+ 之所以用对称加密密钥，是因为数据量太大，对称加密可以节省算力

>    Your browser connects to the server and gets the webserver certificate

>    Your browser checks if it trusts the certificate issuer by checking if the issuer certificate is in its trust store. This trust store is managed by operating system and >browser updates. And on some corporate networks it is managed by the company. From the certificate the browser obtains the public key.

>    The browser now generates random bytes to be used to generate a symmetric key and encrypts this with the public key of the server. So only the server can decrypt it.

>    At the end of this process both the browser and the webserver will use the exchanged symmetric key (in the asymmetric key exchange process) to encrypt and decrypt messages >that are sent back and forth between the browser and the webserver.

