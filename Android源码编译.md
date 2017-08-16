#### Android源码编译
#### 改变磁盘映像大小
```
hdiutil resize -size 140g /Users/nickchen/android.sparseimage
```
#### 编译源码步骤
* 我们在 Android 源码目录下执行如下清理命令:
```
make clobber
```
* 设置环境
```
source build/envsetup.sh
```
* 选择编译目标
```
lunch
```
* 开始编译
```
make -j8
```
