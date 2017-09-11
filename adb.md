
http://teachcourse.cn/1947.html
#### **adb 调试**
> $adb connnect 192.168.1.115 //连接wifi调试 同局域网下     

**问题**
"由于目标计算机积极拒绝，无法连接"    
**原因** 手机的默认adb服务是没有打开   
**解决办法**
1. 如果有线材通过usb连接电脑，可以尝试以下命令重启手机上的adb即可
> adb tcpip 5555
2. usb线连接使用adb shell或者手机终端执行
   $su    #需要root权限
   $setprop service.adb.tcp.port 5555    
   $stop adbd    
   $start adbd    
