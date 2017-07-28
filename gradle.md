#### dependency 
```
1 provided compile-time only dependency(dagger2的注入是编译时生成的，apt也是编译时的，不过这里用了apt获得一些上述的功能)
2 package package-time only dependency
3 compile compile-time and package-time dependency(大多时候我们用的compile)
```
#### 打包命令
```
chmod +x gradlew
./gradlew task buildSdkJar
```
