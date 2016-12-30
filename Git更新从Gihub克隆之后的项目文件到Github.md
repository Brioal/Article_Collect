# Git更新从Gihub克隆之后的项目文件到服务器
1 . 更新从Gihub克隆之后的项目文件到服务器
#### 由于是从Github clone下来的，基本的git设置已经有了，所以就省去了remote到远程仓库的配置方式，那么更新文件到Github就一共只有以下几步：
### 1.添加新增文件到git
```
//添加所有文件到git
git add .
//添加部分文件
git add xxx.xxx xxx.xxx
```
### 2.提交修改
```
git commit -m "提交信息"
```
### 3.push
```
//一般来说只需要这一步操作,执行之后会要求输入用户名和密码
git push
```
## 完毕
