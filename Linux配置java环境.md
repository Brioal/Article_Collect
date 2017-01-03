# Linxu配置Java环境
### 官网下载链接感觉是不稳定，有时候能下载有时候不能下载，如果不能下载请自行百度，记得下载`tar.gz`版本的，解压即可，`rpm`版本的解压不可直接用
## 第一步：移动安装包到`/usr/lib/`目录下
## 第二步：配置环境变量
### 在`etc/profile`文件最后添加
```
export JAVA_HOME="/usr/lib/jdk1.8.0_11"
export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$PATH
```
## 第三步：保存退出
## 第四步：配置生效
### 如果不生效，注销之后重新登陆
```
source ~/.bashrc
```