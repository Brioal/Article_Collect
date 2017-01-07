# 共享动画的实现（AndroidL及以上）
# 效果图：
![](http://123.206.20.217/brioalcode/up//fa66414fe56282c1a626e29d090dca44213.gif)
## 实现步骤：
###1.主题设置
#### `Activity`的主题下添加如下元素，开启支持动画，并且`Activity`必须继承`AppCompatActivity`
```
<item name="android:windowIsTranslucent">true</item>
```
###2 .前一个`Activity`和后一个`Activity`添加相同的组件（代码以ImageView为例子）
###3. 跳转到第二个`Activity`的代码如下：
```
public static void enterLDetail(AppCompatActivity activity, View transView, int position) {
        Intent intent = new Intent(activity, DetailLActivity.class);
        intent.putExtra("position", position);
        ActivityOptionsCompat options = ActivityOptionsCompat.makeSceneTransitionAnimation(activity, transView, "img");
        ActivityCompat.startActivity(activity,intent,options.toBundle());
    }
```

###4.第二个Activity的onCreate方法内代码
```
mImageView = (ImageView) findViewById(R.id.l_detail_iv_img);
ViewCompat.setTransitionName(mImageView, "img");
```

### 完成