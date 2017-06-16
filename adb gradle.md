# Note
平时随手用到的一些命令

## 常用的adb命令
```
调起 Activity adb shell am start [options] <INTENT> 例如： adb shell am start -n com.tencent.mm/.ui.LauncherUI
调起 Service adb shell am startservice [options] <INTENT> 
 例如： adb shell am startservice -n com.tencent.mm/.plugin.accountsync.model.AccountAuthenticatorService
强制停止应用 adb shell am force-stop com.qihoo360.mobilesafe
查看当前所在的进程信息 adb shell ps 或 adb shell ps|grep 包名 
清除应用数据与缓存   adb shell pm clear <packagename>
查看前台 Activity adb shell dumpsys activity activities | grep mFocusedActivity
查看正在运行的Services adb shell dumpsys activity services [<packagename>]

查看设备信息
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
## 反编译 在自己电脑上配置完环境变量
```
使用Apktool反编译.apk文件,目的是获取未被混淆的资源文件(除混淆资源文件/加壳的apk外)
apktool d your.apk
使用解压软件解压.apk文件,获取classes.dex文件,使用dex2jar转换为可以使用jd_gui打开的jar文件
d2j-dex2jar.sh classes.dex
```
## svn添加忽略文件
```
export SVN_EDITOR=nano 如果遇到查看不了的忽略文件
svn propedit svn:ignore .
按ctrl x推出 按之后选Y确定
svn propget svn:ignore .查看忽略文件
```
## 打包命令
```
chmod +x gradlew
./gradlew task buildSdkJar
```
## dos2unix 将windows文件的换行符换成unix能识别的文件

## gradle中dependecy设置
1.  provided  compile-time only dependency(dagger2的注入是编译时生成的，apt也是编译时的，不过这里用了apt获得一些上述的功能)
2.  package  package-time only dependency
3.  compile  compile-time and package-time dependency(大多时候我们用的compile)
## 查看 linux电脑下java
```
whereis java 
which java 
```
## 常用的jar命令
```
向jar包中添加文件
jar uf xxx.apk META-INF/xxx.file
```
