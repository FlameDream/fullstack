# Android 获取gradle中versionName

Android项目中会配置当前APP的版本versionName，其中build.gradle配置如下：
</br>
```java

apply plugin: 'com.android.application'

android {
    compileSdkVersion 33

    defaultConfig {
        applicationId "com.example.myapplication_test"
        minSdkVersion 21
        targetSdkVersion 33
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}


```

</br>

**实现获取versionName代码如下**

```java

PackageInfo pInfo;
try {
    pInfo = sContext.getPackageManager().getPackageInfo("com.example.xxxx", 0);   // com.example.xxxx 替换成APP的applicationId
    String versionName = pInfo.versionName;  
}catch (PackageManager.NameNotFoundException e){

}
```
</br>
这段代码将获取到当前安装的 APP 的版本号。
</br>