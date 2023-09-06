在Android开发中，系统版本和SDK版本的管理是非常重要的。系统和应用程序类似，系统版本和打包系统的targetSdkVersion版本一致，App在Android手机上可以调用所对应SDK中的API。以下是关于compileSdkVersion、minSdkVersion和targetSdkVersion的详细解释：

## 一、compileSdkVersion

compileSdkVersion字面意思为“编译SDK版本”。这是build.gradle通过compileSdkVersion告诉gradle使用哪个SDK来编译APP程序。

在SDK更新过程中，可能会出现一些API被弃用（为了维护SDK的稳健性和避免冗余等）。在新的系统版本中，这些方法调用可能会出现失效的问题。compileSdkVersion就是为了处理APP出现这个问题而存在。

compileSdkVersion版本会在项目编译的过程中，把deprecated的一些API以警告或者报错的形式显示出来。

compileSdkVersion版本应尽量与最新的SDK保持一致。（这样可以避免在新版本手机上出现功能缺失）

## 二、minSdkVersion

minSdkVersion是应用可以运行的Android SDK的最低版本。它用于判断用户设备是否可以安装某个应用。

如果APP使用的Library有自己的minSdkVersion，那么APP本身的minSdkVersion必须大于或等于这些库的minSdkVersion。

maxSdkVersion是应用可以运行的Android SDK的最高版本。一般不指定，因为系统升级时如果超过maxSdkVersion可能会出现APP被移除的问题。

## 三、targetSdkVersion

targetSdkVersion直观翻译是“目标版本”，它的作用是兼容旧的API。targetSDKVersion的版本大小可以决定是否采用新的特性还是维持老的特性。因为在手机系统升级之后，Android SDK在提供新特性的同时会兼容一下老特性，会根据APP targetSDKVersion的版本号来选择使用哪个特性。只要targetSDKVersion没有变化，即使手机系统升级了，还是采用老特性。

举个例子，Android 8.0/8.1系统规定了透明的activity不能固定方向，否则抛出异常。假设我们的app使用了透明的activity，且固定了方向，在Android 8.0版本以下运行正常，运行在Android 8.0/8.1系统上，结果会直接crash。对于我们来说，这结果当然不能接受。因此，google想出了一个办法，那就是通过targetSdkVersion字段来区分同一API在不同系统上的行为。

## 总结：

对于同一个API（方法），新版本的系统更改了它的内部实现逻辑，新逻辑可能会影响之前调用此API的App。为了兼容此问题，引入targetSdkVersion。当targetSdkVersion>=xx（某个系统版本）时采用新修改的逻辑，否则还是沿用之前的逻辑。换句话说：如果你更改了targetSdkVersion值，说明你已经测试过兼容性问题了。

**maxSdkVersion >= buildToolsVersion >= compileSdkVersion >= targetSdkVersion >= minSdkVersion**
