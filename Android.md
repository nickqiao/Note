#### Android5.0后 Service Intent  must be explitict(显式调用)
```
Intent mIntent = new Intent();
mIntent.setAction("XXX.XXX.XXX");//你定义的service的action
mIntent.setPackage(getPackageName());//这里你需要设置你应用的包名
context.startService(mIntent);
```
####  webView给js传值注意
```
1 String 类型的参数需要使用单引号 “’” 包裹，数组类型的参数则不用，
  如：javascript:javaCallJs([01, 02, 03])，
  其他复杂类型的参数可以转换为 Json 字符串的形式传递。

2 可以把复杂字符串encode一次试试
```
