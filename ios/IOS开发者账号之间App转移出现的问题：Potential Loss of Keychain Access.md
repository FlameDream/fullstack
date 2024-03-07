
# IOS开发者账号之间App转移出现的问题：Potential Loss of Keychain Access


开发者账户中的APP进行账户之间的转让，转让成功之后。upload包到新账号的时候，出现如下报错信息：（这个是一个警告消息，IPA包已经上传成功）

WARNING ITMS-90076: “Potential Loss of Keychain Access. The previous version of software has an application-identifier value of [xxxxxxx.com.example.myApp.testApp’] and the new version of software being submitted has an application-identifier of [yyyyyy.com.example.myApp.testApp’]. This will result in a loss of keychain access.”


出现上述问题的原因：

**由于两个账号记录同时出现了一个com.example.myApp.testApp。（Bundle Identifier 是唯一的）转出账户的记录并没有立即清除**


## 注意：

上述问题因为App转让引起的，实际上，对IPA包的上传并没有任何影响，当你登录到iTunesConnect后台查看的时候，你的包已经上传成功了，不需要重新上传，也不需要重新打包，进行上传操作。


