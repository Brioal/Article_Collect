# Win10镜像安装net3.5方法
### 1.装载系统镜像
### 2.用管理员权限打开cmd，输入以下代码：
##### 其中的L换成装载之后的镜像的盘符
```
dism.exe /online /enable-feature /featurename:netfx3 /Source:L:\sources\sxs

```
### 3.等待安装完成，结果如下则为成功安装：
![](http://123.206.20.217/brioalcode/up//41f4628656eb152843701ca49bd3bce4449.png)
