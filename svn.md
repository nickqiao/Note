#### 添加忽略文件
```
export SVN_EDITOR=nano 如果遇到查看不了的忽略文件
svn propedit svn:ignore .
按ctrl x推出 按之后选Y确定
svn propget svn:ignore .查看忽略文件
```
#### 未提交回退单个文件
```
svn revert + 文件名
```
#### 未提交递归回退
```
svn revert . -R
```
#### 回滚到版本号25
```
1 svn up， svn log找到最新版本
2 找到自己想要回滚到的版本号
3 svn merge -r 28:25 something
```
#### 创建分支
```
svn copy {主干http地址} {想要创建的分支地址}
```
#### 合并代码
```
1 cd到目标目录
2 svn merge {地址 * 地址需和目标目录同级}
```
#### 解决冲突
```
svn resolve
```
#### 删除
```
svn delete -m"描述" "地址"
```
