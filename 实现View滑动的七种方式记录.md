# 实现View滑动的七种方式记录
## 效果图：由于每种实现方式的效果基本上是一模一样的，所以只演示一个效果图
![](http://123.206.20.217/brioalcode/up//b23c0e9807252c4fdb310394c0acd2bc238.gif)
### 实现方式都是采用自定义View的方法，监听onTouchEvent方法，计算位移，然后采用不同的方式来将View进行位移
## 一 . `layout`方法
### 实现原理：
### View在其父组件的位置是由父组件的onLayout方法确定的，其实View本身也可以通过相同的方法确定本身的位置，这个方法就是`layout`,参数与`onLayout`一样。而View当前的坐标可由`getLeft`,`getTop`,`getRight`,`getBottom`来确定，再加上偏移值即可确定滑动之后的位置。
### `onTouchEvent`方法实现代码
```
private int mLastX = 0;
    private int mLastY = 0;
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        int x = (int) event.getX();
        int y = (int) event.getY();
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                //记住开始时候的坐标
                mLastX = x;
                mLastY = y;
                break;
            case MotionEvent.ACTION_MOVE:
                //获取坐标偏移值
                int offsetX = x - mLastX;
                int offsetY = y - mLastY;
                layout(getLeft() + offsetX, getTop() + offsetY, getRight() + offsetX, getBottom() + offsetY);
                break;
        }
        return true;
    }
```

## 二.`offsetLeftAndRight()``和`offsetTopAndBottom()``方法
## 此方法相当于对`layout`方法的方向上的封装，实现原理与第一种方式一样，直接贴代码：
```
private int mLastX = 0;
    private int mLastY = 0;

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        int x = (int) event.getX();
        int y = (int) event.getY();
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                mLastX = x;
                mLastY = y;
                break;
            case MotionEvent.ACTION_MOVE:
                int offsetX = x - mLastX;
                int offsetY = y - mLastY;
                offsetLeftAndRight(offsetX);
                offsetTopAndBottom(offsetY);
                break;
        }
        return true;
    }
```


## 三 .`LayoutParams`方法
### `LayoutParams`保存的是`View`的布局参数，因此可以通过改变`LayoutParams`的参数来改变View的位置。原理与第一种方法一样，不同的只是对偏移量的处理,处理偏移量的代码如下：
```
ViewGroup.MarginLayoutParams params = (ViewGroup.MarginLayoutParams) getLayoutParams();
params.leftMargin = getLeft() + offsetX;
params.topMargin = getTop() + offsetY;
setLayoutParams(params);
```

## 四.`scrollTo` , `scrollBy`方法
### `scrollTo()``所需要的参数是要滚动到位置的绝对坐标，`scrollBy()``所需参数是与当前坐标的偏移坐标。但是这种方式作用的对象不是`View`本身，而是其父组件，并且父组件移动的方式与View的方式不一样，因为当父组件移动的时候，其内部的其他View也是在一起移动的，所以想使View向右移动的话需要将父组件向左移动，上下移动也是一样的。
### 处理坐标偏移量的代码：
```
 ((View) getParent()).scrollBy(-offsetX, -offsetY);
```

## 五.`Scroller`方法
### `Scroller`能实现平滑移动的效果，所以这个例子实现的是手指拖动来移动，然后松开手指的时候平滑移动到原本的位置，与`scrollTo`方法一样，`Scroller`作用的也是其父组件。
### `Scroller`的使用步骤：
### 1.初始化`Scroller`
```
mScroller = new Scroller(context);
```
### 2.重写`computeScroll()``方法,实现方式还是父组件的`scrollTo`方法，但是可以通过`Scrolle`r获取当前应该移动到的坐标点，移动之后需要调用重绘，因为`computeScroll`方法只会在`onDraw()`内被调用，当`Scroller`判断移动完毕的时候就会停止移动。
```
@Override
    public void computeScroll() {
        super.computeScroll();
        if (mScroller.computeScrollOffset()) {
            View parent = (View) getParent();
            parent.scrollTo(mScroller.getCurrX(), mScroller.getCurrY());
            //通过重绘来不断调用computeScroll
            invalidate();
        }
    }
```
### 3.开启滚动：
### 开启滚动的方法如下:
```
public void startScroll(int startX , int startY , int dx , int dy , int duration);
public void startScroll(int startX , int startY , int dx , int dy );
```
### 参数分别为：当前`X`上的滚动值，当前`Y`上的滚动值，要滚动的`X`上的偏移值，要滚动的`Y`上的偏移值，滑动持续的时间。
### View滚动到原本的位置的代码：
```
case MotionEvent.ACTION_UP:
                View parent = (View) getParent();
                mScroller.startScroll(parent.getScrollX(), parent.getScrollY() ,- parent.getScrollX(), -parent.getScrollY(),2500);
                //激活滑动操作
                invalidate();
                break;
```

## 六.属性动画
### 效果图:
![](http://123.206.20.217/brioalcode/up//5742a0ae746cb03dd2cba497f8cca1ed904.gif)

### 这个不用多说，不能像之前一样随手指一动（就算可以实现我想应该没人会这样做），演示效果是点击`View`之后`View`自动平滑的向下移动。
### 动画`xml`
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:fromXDelta="0%"
        android:fromYDelta="0%"
        android:toXDelta="60%p"
        android:toYDelta="60%p"/>
</set>
```
### 动画的使用代码：
```
mView.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               Animation animation = AnimationUtils.loadAnimation(mContext, R.anim.trans_back);
               animation.setDuration(2500);
               mView.startAnimation(animation);
           }
       });
```

## 七.`ViewDragHelper`方法
### `ViewDragHelper`在自定义`ViewGroup`中应用很多，功能非常强大，官方的`DrawerLayout`和`SlidePaneLayout`就主要是`ViewDragHelper`实现的。
### 本次实现的效果还是跟随手指移动，是自定义`ViewGroup`。步骤如下：
### `Activity`的布局中会在这个`ViewGroup`中添加一个`View`用于演示滑动，在开始以下步骤之前进行其他处理，如`View`的位置和初始化等的。
### 1.初始化`ViewDrahHelper`
```
mHelper = ViewDragHelper.create(this, new ViewDragHelper.Callback() {
            //决定那个View参与滑动
            @Override
            public boolean tryCaptureView(View child, int pointerId) {
                return child == mView;
            }
            //指定当滑动的坐标变化的时候要滑动的View在X坐标上应该怎么样变化
            @Override
            public int clampViewPositionVertical(View child, int top, int dy) {
                return top;
            }
            //指定当滑动的坐标变化的时候要滑动的View在Y坐标上应该怎么样变化
            @Override
            public int clampViewPositionHorizontal(View child, int left, int dx) {
                return left;
            }
        });
```
### 2.拦截事件
```
@Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        return mHelper.shouldInterceptTouchEvent(ev);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        mHelper.processTouchEvent(event);
        return true;
    }
```

### 3.处理`computeScroll`
```
@Override
    public void computeScroll() {
        if (mHelper.continueSettling(true)) {
            ViewCompat.postInvalidateOnAnimation(this);
        }
    }
```

### 完毕。

### `ViewGroup`的完整代码
```
public class MethodView7 extends ViewGroup {
    private View mView;
    private ViewDragHelper mHelper;

    public MethodView7(Context context) {
        this(context, null);
    }

    public MethodView7(Context context, AttributeSet attrs) {
        super(context, attrs);
        mHelper = ViewDragHelper.create(this, new ViewDragHelper.Callback() {
            @Override
            public boolean tryCaptureView(View child, int pointerId) {
                return child == mView;
            }

            @Override
            public int clampViewPositionVertical(View child, int top, int dy) {
                return top;
            }

            @Override
            public int clampViewPositionHorizontal(View child, int left, int dx) {
                return left;
            }
        });
    }

    @Override
    protected void onFinishInflate() {
        super.onFinishInflate();
        mView = getChildAt(0);
    }

    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        return mHelper.shouldInterceptTouchEvent(ev);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        mHelper.processTouchEvent(event);
        return true;
    }

    @Override
    public void computeScroll() {
        if (mHelper.continueSettling(true)) {
            ViewCompat.postInvalidateOnAnimation(this);
        }
    }

    @Override
    protected void onLayout(boolean changed, int l, int t, int r, int b) {
        mView.layout(16, 16,  216, 216);
    }
}
```


## 七种方法完毕.
