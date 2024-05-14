
# How to resolve 'scanLocation' was deprecated in iOS 13.0


When trying to use a Scanner I am getting the warning that 'scanLocation' was deprecated in iOS 13.0. Since being able to scan from the next location is rather fundamental to scanning a String, wondering what to use instead of scanLocation. Apple's documentation for Scanner does not even mention the deprecation, let alone suggest what has taken the place of scanLocation.


Example of using scanLocation, which is deprecated:


```swift

convenience init(hex: String) {
        let scanner = Scanner(string: hex)
        scanner.scanLocation = 0
        
        var rgbValue: UInt64 = 0
        
        scanner.scanHexInt64(&rgbValue)
        
        let r = (rgbValue & 0xff0000) >> 16
        let g = (rgbValue & 0xff00) >> 8
        let b = rgbValue & 0xff
        
        self.init(
            red: CGFloat(r) / 0xff,
            green: CGFloat(g) / 0xff,
            blue: CGFloat(b) / 0xff, alpha: 1
        )
   }

```



**Solution:  (use startIndex replace scanLocation)**

```swift


convenience init(hex: String) {
        let scanner = Scanner(string: hex)
        if #available(iOS 13.0, *) {
            scanner.currentIndex = hex.startIndex
        } else {
            scanner.scanLocation = 0
        }
        
        var rgbValue: UInt64 = 0
        
        scanner.scanHexInt64(&rgbValue)
        
        let r = (rgbValue & 0xff0000) >> 16
        let g = (rgbValue & 0xff00) >> 8
        let b = rgbValue & 0xff
        
        self.init(
            red: CGFloat(r) / 0xff,
            green: CGFloat(g) / 0xff,
            blue: CGFloat(b) / 0xff, alpha: 1
        )
    }

```

