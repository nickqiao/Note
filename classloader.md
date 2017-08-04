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
#### ClassLoader双亲代理模型加载类的特点和作用
```
JVM中ClassLoader通过defineClass方法加载jar里面的Class，而Android中这个方法被弃用了。
 @Deprecated
    protected final Class<?> defineClass(byte[] classRep, int offset, int length)
            throws ClassFormatError {
        throw new UnsupportedOperationException("can't load this type of class file");
    }
Android中用loadClass方法
public Class<?> loadClass(String className) throws ClassNotFoundException {
        return loadClass(className, false);
    }

    protected Class<?> loadClass(String className, boolean resolve) throws ClassNotFoundException {
        Class<?> clazz = findLoadedClass(className);

        if (clazz == null) {
            ClassNotFoundException suppressed = null;
            try {
                clazz = parent.loadClass(className, false);
            } catch (ClassNotFoundException e) {
                suppressed = e;
            }

            if (clazz == null) {
                try {
                    clazz = findClass(className);
                } catch (ClassNotFoundException e) {
                    e.addSuppressed(suppressed);
                    throw e;
                }
            }
        }

        return clazz;
    }
 
```
