# 组件设置`setCompoundDrawables`不生效解决办法
## 在代码中设置组件的drawable的时候如果单纯的使用`setCompoundDrawables`是不会有效果的，因为没有指定drawable的大小，即`Bound`，具体代码如下：
```

Drawable drawable = getResources().getDrawable(R.drawable.ic_et_bg);
drawable.setBounds(0, 0, drawable.getIntrinsicWidth(), drawable.getIntrinsicHeight());
mEt.setCompoundDrawables(mEt.getCompoundDrawables()[0],drawable,mEt.getCompoundDrawables()[2],mEt.getCompoundDrawables()[0]);

```
### 这种方式是可以指定drawable的大小的，还有另外一种方式，使用drawable的默认大小，如下：
```
Drawable drawable = getResources().getDrawable(R.drawable.ic_et_bg);
mEt.setCompoundDrawablesWithIntrinsicBounds(mEt.getCompoundDrawables()[0],drawable,mEt.getCompoundDrawables()[2],mEt.getCompoundDrawables()[0]);

```