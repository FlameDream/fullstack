
## IOS获取App版本号

在 iOS 开发中，获取App版本号是常见的操作。下面我将详细介绍如何获取APP版本号。
</br>

在App项目中，可以通过访问infoDict字典对象并使用键"CFBundleShortVersionString"来获取App的版本号。例如，您可以使用以下代码获取版本号：

**代码如下**

````objectivec

import Foundation
func getAppVersion() -> String {  
    let appInfo = Bundle.main.infoDictionary!  
    let appVersion = appInfo["CFBundleShortVersionString"] as! String  
    return appVersion  
}
print(getAppVersion()) 

```

这段代码首先导入 Foundation 框架，然后定义一个函数 getAppVersion()，在该函数中，通过访问 Bundle.main.infoDictionary 来获取 App 的版本信息，其中"CFBundleShortVersionString"是苹果官方规定的一个键，对应的值就是我们要获取的 App 版本号。最后，通过 print() 函数打印出获取到的版本号。





