#### Android5.0后 Service Intent  must be explitict(显式调用)
```
Intent mIntent = new Intent();
mIntent.setAction("XXX.XXX.XXX");//你定义的service的action
mIntent.setPackage(getPackageName());//这里你需要设置你应用的包名
context.startService(mIntent);
```

