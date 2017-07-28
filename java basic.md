#### 当且仅当满足以下所有条件时，才应该使用 volatile 变量：
```
对变量的写入操作不依赖变量的当前值，或者你能确保只有单个线程更新变量的值。
该变量没有包含在具有其他变量的不变式中。
在需要同步的时候，第一选择应该是 synchronized 关键字，这是最安全的方式
```
#### linux电脑下java
```
whereis java 
which java
```
#### jar命令
```
向jar包中添加文件
jar uf xxx.apk META-INF/xxx.file
```
#### 查看apk包名
```
keytool -printcert -file META-INF/CERT.RSA
```
#### 反编译 在自己电脑上配置完环境变量
```
使用Apktool反编译.apk文件,目的是获取未被混淆的资源文件(除混淆资源文件/加壳的apk外)
apktool d your.apk
使用解压软件解压.apk文件,获取classes.dex文件,使用dex2jar转换为可以使用jd_gui打开的jar文件
d2j-dex2jar.sh classes.dex
```
#### dos2unix 将windows文件的换行符换成unix能识别的文件
