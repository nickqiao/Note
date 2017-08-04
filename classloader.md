#### DexClassLoader和PathClassLoader的区别
```
DexClassLoader可以加载jar/apk/dex,可以从SD卡中加载未安装的apk
PathClassLoader只能加载系统中已经安装过的apk
```

#### 一个运行的Andriod应用至少有几个ClassLoader
```
一个是BootClassLoader（系统启动的时候创建的）
另一个是PathClassLoader
（应用启动时创建的，用于加载“/data/app/应用报名/base.apk”里面的类）
```
