
# 如何解决scanLocation在iOS 13.0中被废弃的问题？

当Swift新项目或者是老项目升级出现了Scanner 'scanLocation' was deprecated in iOS 13.0的问题，“scanLocation”在iOS 13.0中被废弃了。


scanLocation Warning的代码
```swift

convenience init(hexString: String) {
        let scanner = Scanner(string: hexString)
        scanner.scanLocation = 0   // 'scanLocation' was deprecated in iOS 13.0
        var rgbValue: UInt64 = 0
        scanner.scanHexInt64(&rgbValue)
}

```


### 解决办法：

您可以使用currentIndex而不是scanLocation

```swift
scanner.currentIndex = hexString.startIndex
```


**最终的代码如下：**

```swift

convenience init(hexString: String) {
        let scanner = Scanner(string: hexString)

        if #available(iOS 13.0, *) {
            scanner.currentIndex = hexString.startIndex
        } else {
            scanner.scanLocation = 0
        }

        var rgbValue: UInt64 = 0
        scanner.scanHexInt64(&rgbValue)
}

```





