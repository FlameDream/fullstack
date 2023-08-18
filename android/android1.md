# Android Studio 安装APP后不自启动问题

开发新项目过程中突然碰到该问题，虽然对项目影响不大，但是在有着完美强迫症的情况下，百度和自己找原因小久下终于解决：


.将Launch Options的Launch项改为Default Activity；（成功解决）

步骤：

点击打开




找到Launch Options，将Launch选择项Nothing改为Default Activity


问题解决。