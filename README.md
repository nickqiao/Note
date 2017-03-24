# Note
some notes 
## IPC知识
### adb shell ps 或 adb shell ps|grep 包名 查看当前所在的进程信息
## 反编译 在自己电脑上配置完环境变量
### 使用Apktool反编译.apk文件,目的是获取未被混淆的资源文件(除混淆资源文件/加壳的apk外)
#### apktool d your.apk
### 使用解压软件解压.apk文件,获取classes.dex文件,使用dex2jar转换为可以使用jd_gui打开的jar文件
#### d2j-dex2jar.sh classes.dex

## svn添加忽略文件
#### export SVN_EDITOR=nano 如果遇到查看不了的忽略文件
#### svn propedit svn:ignore .
#### 进入之后把需要忽略的文件架上
#### 按ctrl x推出 按之后选Y确定
#### svn propget svn:ignore .查看忽略文件

## 打包命令 chmod +x gradlew
#### ./gradlew task buildSdkJar

## dos2unix 将windows文件的换行符换成unix能识别的文件

## gradle中dependecy设置
###  provided - compile-time only dependency(dagger2的注入是编译时生成的，apt也是编译时的，不过这里用了apt获得一些上述的功能)
###  package - package-time only dependency
###  compile - compile-time and package-time dependency(大多时候我们用的compile)
