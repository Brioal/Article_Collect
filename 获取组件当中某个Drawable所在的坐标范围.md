# 获取组件当中某个Drawable所在的坐标范围
## 如下图所示（以DrawableRight来做演示，其他类似)：
![](http://123.206.20.217/brioalcode/up//941598b85fc5511c3e5ec167bcb4a811867.png)
### 那么图标所在的坐标位置即为
```
x >=(getWidth() - getTotalPaddingRight());
x <= (getWidth() - getPaddingRight());
y >= getPaddingTop() ;
y <= getHeight() - getPaddingBottom()
```
