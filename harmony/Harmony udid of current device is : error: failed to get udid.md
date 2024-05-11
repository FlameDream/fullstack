
## Harmony udid of current device is : error: failed to get udid


在Harmony开发过程中，会用到hdc来获取设备的uuid，使用“hdc shell bm get --udid”。

但是输入之后会出现：udid of current device is : error: failed to get udid错误信息


解决方案：

```bash

# 使用命令
HdcExternal shell bm get --udid

```

就可以直接获取设备的UUID信息


