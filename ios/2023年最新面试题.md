## iOS开发Post请求错误：Error Domain=NSCocoaErrorDomain Code=3840 JSON text did not start with array or ...

在IOS开发过程化，经常会遇到各种网络请求的错误，错误：Error Domain=NSCocoaErrorDomain Code=3840 JSON text did not start with array or ...是一个比较常见的错误类型。


## 问题：

iOS开发Post网络[AFNetworking](https://github.com/AFNetworking/AFNetworking)请求出现如下错误：

Error Domain=NSCocoaErrorDomain Code=3840 "JSON text did not start with array or object and option to allow fragments not set." UserInfo={NSDebugDescription=JSON text did not start with array or object and option to allow fragments not set.}


## 原因：

从报出的错误信息的字面意思是：“请求返回JSON Text解析错误”。


## 解决方案：

需要把AFHTTPSessionManager的responseSerializer类型改成AFHTTPResponseSerializer，返回的类型变成NSData。（使用AFJSONResponseSerializer返回的类型是NSDictory JSON类型的）
 
 ```objectivec
 	AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

// 修改前
 //  manager.responseSerializer = [AFJSONResponseSerializer serializerWithReadingOptions:NSJSONReadingMutableContainers];
 //  后者
 //  manager.responseSerializer = [AFJSONResponseSerializer serializer];
 

 // 修改后
    manager.responseSerializer = [AFHTTPResponseSerializer serializer];

 ```





