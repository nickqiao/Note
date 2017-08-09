#### 代理模式
#### activity启动问题
一个 Activity 的启动，如果不采用标准的 Intent 方式，没有经历过 AMS(ActivityManagerService) 的一系列注册和初始化过程，
它的生命周期方法是不会被系统调用的
* 在 ProxyActivity 生命周期里用反射调用插件 Activity 相应生命周期的方法
* 把插件 Activity 的生命周期抽象成接口，在 ProxyActivity 的生命周期里调用

#### 在插件 Activity 里使用 res 资源
平时获取res方式: context.getResoures().getXXX(resId)
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
super 类 ContextThemeWrapper 里的 “getResources()” 方法,
```
    Context mBase;
    
    public ContextWrapper(Context base) {
        mBase = base;
    }
    @Override
    public Resources getResources() {
        return mBase.getResources();
    }
```
由于context是抽象类，具体实现应该是在contextImpl中
```
    @Override
    public Resources getResources() {
        return mResources;
    }
    构造方法中 {
      resources = mResourcesManager.getTopLevelResources(packageInfo.getResDir(),
                        packageInfo.getSplitResDirs(), packageInfo.getOverlayDirs(),
                        packageInfo.getApplicationInfo().sharedLibraryFiles, displayId,
                        overrideConfiguration, compatInfo);
     mResources = resources;
    }
    
    Resources getTopLevelResources(String resDir, String[] splitResDirs,
           String[] overlayDirs, String[] libDirs, int displayId,
           Configuration overrideConfiguration, CompatibilityInfo compatInfo) {
       Resources r;
       AssetManager assets = new AssetManager();
       if (libDirs != null) {
           for (String libDir : libDirs) {
               if (libDir.endsWith(".apk")) {
                   if (assets.addAssetPath(libDir) == 0) {
                       Log.w(TAG, "Asset path '" + libDir +
                               "' does not exist or contains no resources.");
                   }
               }
           }
       }
       DisplayMetrics dm = getDisplayMetricsLocked(displayId);
       Configuration config ……;
       r = new Resources(assets, dm, config, compatInfo);
       return r;
   }
    
```
