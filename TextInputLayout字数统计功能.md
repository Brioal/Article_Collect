# TextInputLayout字数统计功能实现
### 效果演示
![](http://123.206.20.217/brioalcode/up//8b817590bdc6b55d942e4ef4e1349d2f295.gif)
#### 图示可以看出，字数统计和浮动标签显示分为两种状态，一是字数未满的状态，图中显示的是红色，二是字数满了之后的状态，图中显示的是蓝色。这两种状态都可以人为的定制。

#### `xml`文件:
#### 建议用`TextInputEditText`,MD风格能更好的支持
#### 其中的`app:counterOverflowTextAppearance`设置的是字数满了之后的样式，本文只设置了字体的颜色，实际中可以添加字体大小等属性
#### 其中的`app:counterTextAppearance`设置的是字数未满时候的样式，本文只设置了字体的颜色，实际中可以添加字体大小等属性
```
<android.support.design.widget.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:counterEnabled="true"
        app:counterMaxLength="20"
        app:counterOverflowTextAppearance="@style/count_over_text"
        app:counterTextAppearance="@style/count_text">

        <EditText
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:hint="用户名"
            android:inputType="text"/>

    </android.support.design.widget.TextInputLayout>
```

#### 属性文件
#### 注意`style`还有个`parent`
```
<style name="count_over_text" parent="Base.TextAppearance.AppCompat.Light.Widget.PopupMenu.Small">>
        <item name="android:textColor">#1310d6</item>
    </style>
 <style name="count_text" parent="Base.TextAppearance.AppCompat.Light.Widget.PopupMenu.Small">>
        <item name="android:textColor">#d6105f</item>
    </style>

```
