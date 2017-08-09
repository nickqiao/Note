#### 代理模式
#### activity启动问题
一个 Activity 的启动，如果不采用标准的 Intent 方式，没有经历过 AMS(ActivityManagerService) 的一系列注册和初始化过程，
它的生命周期方法是不会被系统调用的
* 在 ProxyActivity 生命周期里用反射调用插件 Activity 相应生命周期的方法
* 把插件 Activity 的生命周期抽象成接口，在 ProxyActivity 的生命周期里调用

#### 在插件 Activity 里使用 res 资源
平时获取res方式: context.getResoures().get(resId)
```
@Override
    public Resources getResources() {
        if (mResources != null) {
            return mResources;
        }
        if (mOverrideConfiguration == null) {
            mResources = super.getResources();
            return mResources;
        } else {
            Context resc = createConfigurationContext(mOverrideConfiguration);
            mResources = resc.getResources();
            return mResources;
        }
    }
```
