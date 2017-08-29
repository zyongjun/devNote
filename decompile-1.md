

#### 列出手机应用包名
```
1|libra:/ $ adb shell pm list packages
package:com.android.cts.priv.ctsshim
package:com.goplaycn.googleinstall
package:com.android.providers.telephony
com.miui.gallery
...
```

#### 查找安装包位置
```
libra:/ $ adb shell pm path com.miui.gallery
/system/bin/sh: adb: not found
127|libra:/ $ pm path com.miui.gallery
package:/system/priv-app/MiuiGallery/MiuiGallery.apk
```

#### 导出
```
libra:/ $ pull /system/priv-app/MiuiGallery/MiuiGallery.apk
/system/bin/sh: pull: not found
127|libra:/ $ adb pull /system/priv-app/MiuiGallery/MiuiGallery.apk
/system/bin/sh: adb: not found
127|libra:/ $ exit

C:\Users\Administrator>adb pull /system/priv-app/MiuiGallery/MiuiGallery.apk
/system/priv-app/MiuiGallery/MiuiGalle.... 17.5 MB/s (15620260 bytes in 0.849s)

```