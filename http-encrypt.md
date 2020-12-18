
# http中的加密
+ 浏览器获取网站的证书
+ 浏览器检查是否是可信证书，从证书中获取公钥
+ 浏览器生成对称加密密钥，用公钥加密对称加密密钥，发给服务器，这样只有服务器可以解开
+ 之所以用对称加密密钥，是因为数据量太大，对称加密可以节省算力

>    Your browser connects to the server and gets the webserver certificate

>    Your browser checks if it trusts the certificate issuer by checking if the issuer certificate is in its trust store. This trust store is managed by operating system and >browser updates. And on some corporate networks it is managed by the company. From the certificate the browser obtains the public key.

>    The browser now generates random bytes to be used to generate a symmetric key and encrypts this with the public key of the server. So only the server can decrypt it.

>    At the end of this process both the browser and the webserver will use the exchanged symmetric key (in the asymmetric key exchange process) to encrypt and decrypt messages >that are sent back and forth between the browser and the webserver.

# openssl 
+ 根据私钥得到公钥
openssl rsa -in private -pubout> pub
+ 根据公钥得到mod
公钥中包含n（modulus）和e，n是两个大素数的乘积
私钥中包含n和d
```shell 
openssl rsa -pubin -in pub  -text -modulus
Public-Key: (2048 bit)
Modulus:
    00:87:04:84:a1:ef:de:ff:a3:fa:45:c5:f9:a7:4b:
    d4:43:df:19:e8:5e:21:40:8c:53:ed:12:0c:d8:59:
    22:84:35:df:ab:50:ae:5a:29:b9:ad:84:46:67:da:
    4c:86:eb:e5:83:3c:49:43:be:3e:05:c0:05:05:6c:
    25:a7:59:f7:83:2f:54:2d:7c:7c:be:0d:21:27:bd:
    1a:42:77:4b:60:40:ff:af:b0:46:71:40:ee:74:a2:
    6a:7a:e6:39:53:d2:74:ec:51:6c:63:84:3e:1c:f3:
    7c:42:d6:5b:04:28:9a:a0:5b:b3:1e:ad:b2:11:6d:
    f2:4d:b6:47:ec:73:34:05:71:81:24:47:ee:ec:c0:
    0f:bf:77:d2:d5:1c:01:d4:74:a5:c5:0e:c7:4a:ae:
    71:95:59:59:8a:f4:d2:80:bf:49:6e:9e:9f:e8:f2:
    68:82:e0:f2:7c:d0:1a:06:a5:bb:2f:49:51:bc:7d:
    5c:e0:f2:11:b3:16:7b:e9:d9:6b:4f:b4:bf:eb:b6:
    3f:46:71:7e:ef:60:5d:3b:ac:d5:05:69:53:28:74:
    c5:0b:e3:b7:3e:d7:ac:b8:8f:6b:44:be:70:d6:7f:
    e7:b1:10:b0:60:45:9d:6d:25:06:e0:b9:53:36:3a:
    1a:0d:c9:5c:a5:a1:c7:81:33:f1:e7:e1:2a:90:fc:
    20:25
Exponent: 257 (0x101)
Modulus=870484A1EFDEFFA3FA45C5F9A74BD443DF19E85E21408C53ED120CD859228435DFAB50AE5A29B9AD844667DA4C86EBE5833C4943BE3E05C005056C25A759F7832F542D7C7CBE0D2127BD1A42774B6040FFAFB0467140EE74A26A7AE63953D274EC516C63843E1CF37C42D65B04289AA05BB31EADB2116DF24DB647EC73340571812447EEECC00FBF77D2D51C01D474A5C50EC74AAE719559598AF4D280BF496E9E9FE8F26882E0F27CD01A06A5BB2F4951BC7D5CE0F211B3167BE9D96B4FB4BFEBB63F46717EEF605D3BACD50569532874C50BE3B73ED7ACB88F6B44BE70D67FE7B110B060459D6D2506E0B953363A1A0DC95CA5A1C78133F1E7E12A90FC2025
writing RSA key
-----BEGIN PUBLIC KEY-----
MIIBITANBgkqhkiG9w0BAQEFAAOCAQ4AMIIBCQKCAQEAhwSEoe/e/6P6RcX5p0vU
Q98Z6F4hQIxT7RIM2FkihDXfq1CuWim5rYRGZ9pMhuvlgzxJQ74+BcAFBWwlp1n3
gy9ULXx8vg0hJ70aQndLYED/r7BGcUDudKJqeuY5U9J07FFsY4Q+HPN8QtZbBCia
oFuzHq2yEW3yTbZH7HM0BXGBJEfu7MAPv3fS1RwB1HSlxQ7HSq5xlVlZivTSgL9J
bp6f6PJoguDyfNAaBqW7L0lRvH1c4PIRsxZ76dlrT7S/67Y/RnF+72BdO6zVBWlT
KHTFC+O3PtesuI9rRL5w1n/nsRCwYEWdbSUG4LlTNjoaDclcpaHHgTPx5+EqkPwg
```
+ 私钥签名，签名后base64编码
openssl dgst -sign private -sha256 -out aftersign sign

