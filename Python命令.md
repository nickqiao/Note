#### 更新pip 一定要加sudo，否则出现权限问题
```
sudo pip install --upgrade pip 
```
#### virtualenv
* 安装virtualenv
```
安装 pip install --upgrade virtualenv 
```
* 创建virtualenv环境  
```
virtualenv --system-site-packages  targetDirectory
virtualenv --system-site-packages -p python3 targetDirectory
--no-site-packages 已经安装到系统Python环境中的所有第三方包都不会复制过来
--system-site-packages 会复制系统的第三方包
```
* 进入virtualenv环境
```
source ~/工程文件夹/bin/activate
```
* 退出virtualenv环境
```
deactivate
```


