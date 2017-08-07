#### 当且仅当满足以下所有条件时，才应该使用 volatile 变量：
```
对变量的写入操作不依赖变量的当前值，或者你能确保只有单个线程更新变量的值。
该变量没有包含在具有其他变量的不变式中。
在需要同步的时候，第一选择应该是 synchronized 关键字，这是最安全的方式
```
#### java 移位运算符 >>>  无符号右移，忽略符号位，空位都以0补齐
```
int high = 2100000000;
int low = 2000000000;
System.out.println("mid using >>> 1 = " + ((low + high) >>> 1));
System.out.println("mid using / 2   = " + ((low + high) / 2));

print
mid using >>> 1 = 2050000000
mid using / 2   = -97483648
```
#### RandomAccess 接口 RandomAccess接口是List 实现所使用的标记接口，
用来表明其支持快速（通常是固定时间）随机访问。
此接口的主要目的是允许一般的算法更改其行为，从而在将其应用到随机或连续访问列表时能提供良好的性能

```
在对list的遍历算法中,要尽量来判断是属于RandomAccess(如ArrayList)还是SequenceAccess(如LinkedList）
如果属于RandomAccess ，使用普通遍历  for 循环效率更高

否则使用遍历器 Iterator进行遍历

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
