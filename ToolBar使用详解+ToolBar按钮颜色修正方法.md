# ToolBar使用详解+ToolBar按钮颜色修正方法
## 效果图：
![](http://123.206.20.217/brioalcode/up//72173d2d215ce34821134f795f8de4ae364.png)
[ToolBar按钮颜色修正方法](#jump)
### 从左到右分别为`navigationIcon`,`Logo`,标题，副标题，内嵌的`View`,`ContextMenu`,下文将依次介绍各自的使用方式:
### 前提：
 1. 推荐使用`android.support.v7.widget.Toolbar`包下的ToolBar，兼容性更好
 2. 下文所用的`xml`属性前缀应该是`app`而不是`android`,否则没有效果

## 一 .  `navigationIcon`
#### xml属性设置
 ```
app:navigationIcon="@drawable/ic_navi"
 ```
#### 设置点击事件
 ```
 mToolbar.setNavigationOnClickListener(new View.OnClickListener() {
             @Override
             public void onClick(View v) {
                 //TODO
             }
         });
 ```

 ## 二.`Logo`
 ### xml属性设置
 ```
app:logo="@drawable/ic_navi"
 ```

 ## 三. 标题，副标题
 ### xml设置
 ```
 app:title="标题"
 app:subtitle="副标题"
 ```
 ### 字体颜色设置
 ```
app:titleTextColor="@android:color/white"
app:subtitleTextColor="@android:color/white"
 ```

 ## 四 . `View`
 ### ToolBar其实是一个ViewGroup，所以直接在`xml`中添加即可
 ```
 <android.support.v7.widget.Toolbar
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
        >

         <TextView
             android:layout_width="40dp"
             android:layout_height="40dp"
             android:layout_margin="5dp"
             android:gravity="center"
             android:text="View"
             android:textColor="@android:color/white"
             android:textSize="18sp"/>
     </android.support.v7.widget.Toolbar>
 ```

 ## 五.`ContextMenu`
 ### `menu`文件
 ```
 <?xml version="1.0" encoding="utf-8"?>
 <menu xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto">
     <item
         android:id="@+id/nav_1"
         android:icon="@drawable/ic_navi"
         android:title="按钮一"
         app:showAsAction="always"
         />
     <item
         android:id="@+id/nav_2"
         android:icon="@drawable/ic_navi"
         android:title="按钮二"
         app:showAsAction="always"
         />
     <item
         android:id="@+id/nav_3"
         android:icon="@drawable/ic_navi"
         android:title="按钮三"
         />
     <item
         android:id="@+id/nav_4"
         android:icon="@drawable/ic_navi"
         android:title="按钮四"
         />
 </menu>
 ```
 ### 设置菜单显示与点击事件
 ```
 //添加溢出菜单
        toolbar.inflateMenu(R.menu.setting_menu);
        // 添加菜单点击事件
        toolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
            @Override
            public boolean onMenuItemClick(MenuItem item) {
                switch (item.getItemId()){
                    case R.id.item_setting:
                        //点击设置菜单
                        break;
                }
                return false;
            }
        });
 ```
 <span id = "jump"></span>
### 设置显示按钮的颜色和展开的文字颜色(同样适用于显示返回按钮自定义按钮颜色)
#### `style`文件
```
<style name="ToolbarTheme" parent="Theme.AppCompat.Light">
        <!-- 设置 toolbar 溢出菜单的文字的颜色 -->
        <item name="android:textColor">@android:color/holo_red_dark</item>
        <item name="actionMenuTextColor">@android:color/white</item>
        <item name="colorButtonNormal">@android:color/white</item>
        <item name="colorControlNormal">@android:color/white</item>
    </style>
```
#### 设置主题:注意是`app：theme`而不是`style`
```
app:theme="@style/ToolbarTheme"
```
