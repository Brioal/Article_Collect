# Linxu配置Java环境
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