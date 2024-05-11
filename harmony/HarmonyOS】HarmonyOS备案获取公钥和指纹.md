
## 【HarmonyOS】HarmonyOS备案获取公钥和指纹

通常移动端应用在各大平台使用云资源时，就需要在对应的平台进行应用备案，平台会要求提供应用对应的公钥和签名指纹的信息。

传统的Android应用可以直接通过keystore或jks签名文件获取签名信息。HarmonyOS签名方式与Android不同，所以给您科普一下如何获取HarmonyOS应用或元服务的公钥和签名指纹的信息。

以HarmonyOS应用在华为云备案为例，需要填写对应的公钥和签名MD5值。









这里的指纹是SHA1指纹，一般也可以通过这个值去备案。如果确实需要获取MD5指纹，那可以通过openssl命令获取。

D:\> openssl x509 -fingerprint -md5 -noout -in myapp.cer

md5 Fingerprint=55:9F:F7:FA:4A:0E:**:**:9E:E5:59:C9:9A:3A:08:8E

当然SHA1指纹也可以通过命令获取：

D:\> openssl x509 -fingerprint -sha1 -noout -in myapp.cer

sha1 Fingerprint=15:3E:C8:9D:A7:0E:**:**:**:59:DF:46:F1:53:AF:84:C9:BF:D0:61 

