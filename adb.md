#### 调起 Activity
```
adb shell am start [options] <INTENT> 例如： adb shell am start -n com.tencent.mm/.ui.LauncherUI
```
#### 调起 Service 
```
adb shell am startservice [options] <INTENT> 
例如： adb shell am startservice -n com.tencent.mm/.plugin.accountsync.model.AccountAuthenticatorService
```
#### 强制停止应用 
```
adb shell am force-stop com.qihoo360.mobilesafe
```
#### 查看当前所在的进程信息 
```
adb shell ps 或 adb shell ps|grep 包名 
```
#### 清除应用数据与缓存   
```
adb shell pm clear <packagename>
```
#### 查看前台 Activity 
```
adb shell dumpsys activity activities | grep mFocusedActivity
```
#### 查看正在运行的Services 
```
adb shell dumpsys activity services [<packagename>]
```
#### 查看设备信息
```
adb shell getprop ro.product.model
adb shell dumpsys battery
adb shell wm size
adb shell wm density
adb shell dumpsys window displays
Android_id adb shell settings get secure android_id
imei adb shell dumpsys iphonesubinfo
获取ip地址 adb shell ifconfig | grep Mask
mac地址 adb shell cat /sys/class/net/wlan0/address
cpu信息 adb shell cat /proc/cpuinfo
```
