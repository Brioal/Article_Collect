# 带有清空按钮的EditText开源库
## 效果图：
![](http://123.206.20.217/brioalcode/up//b6ff659665651d74d2b4977337a26321594.png)
### 基本介绍如下:
![](http://123.206.20.217/brioalcode/up//b6ff659665651d74d2b4977337a26321594.png)
### 使用方式：
### 一.添加库依赖
#### 1. 项目的`build.gradle`下添加
```
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```

#### 2. app的`build.gradle`下添加依赖
```
	dependencies {
	        compile 'com.github.Brioal:DeleteEditText:1.0'
	}
```

### 二.xml布局
#### 与`EditText`的使用没有区别，只有一点就是如果要更改默认的删除图标，设置`drawableRight`即可，不设置的话会显示默认的`icon`
```
<com.brioal.deview.DEView
            android:id="@+id/main_et1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />
```
### 以上的设置即可使用带有清空按钮的EditText了，但是有两点需要注意：
### 因为删除按钮的时候主要影响了EditText的`setOnFocusChangeListener（）`方法和`addTextChangedListener（）`，如果你在项目中需要用到这两个方法的话，为了不影响删除按钮的功能，请参照以下的例子：
#### 这个例子的功能是实时的输出EditText的焦点状态和输入内容更改之后的文字，代码如下：
```
mDEView2.setOnFocusChangeListener(new DEFocuChangeListener(mDEView2){
            @Override
            public void onFocusChange(View v, boolean hasFocus) {
                super.onFocusChange(v, hasFocus);
                System.out.println("焦点状态:"+hasFocus);
            }
        });
        mDEView2.addTextChangedListener(new DETextChangeListener(mDEView2){
            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
                super.onTextChanged(s, start, before, count);
            }

            @Override
            public void afterTextChanged(Editable s) {
                super.afterTextChanged(s);
                System.out.println("当前的内容是:"+s.toString());
            }
        });

```
### 当然除了这种方式还可以直接写一个类继承`DEFocuChangeListener`或者`DETextChangeListener`。


