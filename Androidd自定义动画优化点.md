#### 使用 PropertyValuesHolder
平时可能这样写
```
ObjectAnimator animX = ObjectAnimator.ofFloat(myView, "x", 50f);
ObjectAnimator animY = ObjectAnimator.ofFloat(myView, "y", 100f);
AnimatorSet animSetXY = new AnimatorSet();
animSetXY.playTogether(animX, animY);
animSetXY.start();
```
应该改成这样:
```
PropertyValuesHolder pvhX = PropertyValuesHolder.ofFloat("x", 50f);
PropertyValuesHolder pvhY = PropertyValuesHolder.ofFloat("y", 100f);
ObjectAnimator.ofPropertyValuesHolder(myView, pvhX, pvyY).start();
```
#### 使用 Keyframe
```
AnimatorSet animSet = new AnimatorSet();
ObjectAnimator transYFirstAnim = ObjectAnimator.ofFloat(mView, "translationY", 0, 100);
ObjectAnimator transYSecondAnim = ObjectAnimator.ofFloat(mView, "translationY", 100, 0);
animSet.playSequentially(transYFirstAnim, transYSecondAnim);
```
改为
```
Keyframe k0 = Keyframe.ofFloat(0f, 0); //第一个参数为“何时”，第二个参数为“何地”
Keyframe k1 = Keyframe.ofFloat(0.5f, 100);
Keyframe k2 = Keyframe.ofFloat(1f, 0);
PropertyValuesHolder p = PropertyValuesHolder.ofKeyframe("translationY", k0, k1, k2);
ObjectAnimator objectAnimator = ObjectAnimator.ofPropertyValuesHolder(mView, p);
objectAnimator.start();
```
#### 使用 AnimatorListenerAdapter 代替 AnimatorListener
由于 AnimatorListener 是接口，所以实现它得实现它所有的方法，而我们有时只用到它的个别回调（如：onAnimationStart），使用它会导致代码看起来非常冗杂。而 AnimatorListenerAdapter 是默认实现了 AnimatorListener 的一个抽象类，你可以按需要重写其中的方法，代码会优雅一点。
#### 使用 ViewPropertyAnimator机制
```
ObjectAnimator animator = ObjectAnimator.ofFloat(textview, “alpha”, 0f); animator.start(); 
//等同 
textview.animate().alpha(0f);
```
animate() 方法就是在 Android 3.1 系统上新增的一个方法，这个方法的返回值是一个 ViewPropertyAnimator 对象。（简明方便）
```
textview.animate().x(500).y(500).setDuration(5000).setInterpolator(new BounceInterpolator());
```
#### ，每个 View 中都有 Canvas 可以用来绘制动画，只需要在这个 View 中重载 onDraw() 方法就可以。那用什么来绘制动画呢？我们可以考虑使用 SurfaceView，它能够在非 UI 线程中进行图形绘制，释放了 UI 线程的压力
```
public class MainActivity extends Activity {  
	@Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(new Circle(this)); // 添加自定义的SurfaceView  
    }  
  
    @Override  
    public boolean onCreateOptionsMenu(Menu menu) {  
        // Inflate the menu; this adds items to the action bar if it is present.  
        getMenuInflater().inflate(R.menu.main, menu);  
        return true;  
    }  
}
public class Circle extends SurfaceView implements SurfaceHolder.Callback {
    private OnCircleAnimationListener mListener;
    private int mWidth;
    private int mHeight;
    private SurfaceHolder mHolder;
    private static final String TEXT_CIRCLE = "跳过";
    private int mDegree = 0;
    private long mDelay = 3000; // 默认运行时间3秒
    private boolean mStop = false;
    private Paint mClearPaint;
    public Circle(Context context) {
        super(context);
        //
        mHolder = getHolder();
        mHolder.addCallback(this);
    }
    public Circle(Context context, AttributeSet attrs) {
        super(context, attrs);
        mHolder = getHolder();
        mHolder.addCallback(this);
        // 下面的代码会能够去除掉圆圈之外的黑色背景
        setZOrderOnTop(true);
        mHolder.setFormat(PixelFormat.TRANSLUCENT);
    }
    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
//        setMeasuredDimension(100, 100);
    }
    @Override
    public void surfaceCreated(SurfaceHolder surfaceHolder) {
        // 获取宽高
        mWidth = getMeasuredWidth();
        mHeight = getMeasuredHeight();
        if (mListener != null) {
            mListener.onAnimationPrepared(Circle.this);
        }
    }
    @Override
    public void surfaceChanged(SurfaceHolder surfaceHolder, int i, int i1, int i2) {
        Log.e("John", "Circle" + " # " + "surface changed");
    }
    @Override
    public void surfaceDestroyed(SurfaceHolder surfaceHolder) {
    }
    public void setCircleAnimationListener(OnCircleAnimationListener listener) {
        mListener = listener;
    }
    public void startCircleAnimation() {
        new DrawThread().start();
    }
    public void setAnimationDelay(long delay) {
        mDelay = delay;
    }
    public void stopAnimation() {
        mStop = true;
    }
    public class DrawThread extends Thread {
        private Paint mPaint;
        private Paint mTextPaint;
        private Paint mArcPaint;
        public DrawThread() {
            mPaint = new Paint();
            mPaint.setAntiAlias(true);
            mTextPaint = new TextPaint();
            mTextPaint.setTextSize(mHeight / 2-5);
            mTextPaint.setColor(Color.WHITE);
            mPaint.setColor(Color.RED);
            mArcPaint = new Paint();
            mArcPaint.setStrokeWidth((float) (mWidth / 2 * 0.1));
            mArcPaint.setColor(Color.BLUE);
            mArcPaint.setAntiAlias(true);
            mArcPaint.setStyle(Paint.Style.STROKE);
            //这是定义橡皮擦画笔
            mClearPaint = new Paint();
            mClearPaint.setAntiAlias(true);
            mClearPaint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.CLEAR));
        }
        @Override
        public void run() {
            mListener.onAnimationStart(Circle.this);
            while (!mStop) {
                drawCircle();
                if (mDegree >= 360) {
                    mListener.onAnimationFinished(Circle.this);
                    break;
                }
                // 把总的动画时间分成360份
                long animation_duration = mDelay / 360;
                SystemClock.sleep(animation_duration);
                mDegree++;
            }
        }
        // 绘制圆圈
        private void drawCircle() {
            mListener.onAnimationRunning(Circle.this);
            Canvas canvas = mHolder.lockCanvas();
            if (canvas == null) {
                return;
            }
            canvas.drawRect(0, 0, mWidth, mHeight, mClearPaint);
            canvas.drawColor(Color.TRANSPARENT, PorterDuff.Mode.CLEAR);
            canvas.save();
            canvas.scale(0.9f, 0.9f, mWidth * 1f / 2, mHeight * 1f / 2);
            canvas.drawCircle(mWidth * 1.0f / 2, mHeight * 1.0f / 2, mWidth * 1.0f / 2, mPaint);
            float centerY = mHeight * 1f / 2;
            // 这个是获取每个文字的宽度，那么怎么知道有几个文字呢?
            float widths[] = new float[2];
            mTextPaint.getTextWidths(TEXT_CIRCLE, widths);
            canvas.drawText(TEXT_CIRCLE, 5, centerY + (widths[0] * 1f / 2) - 10, mTextPaint);
            canvas.restore();
            // 旋转坐标画圆圈
            canvas.save();
            canvas.rotate(-90, mWidth / 2, mHeight / 2);
            RectF rectF = new RectF((float) (mWidth / 2 * 0.1) / 2, (float) (mWidth / 2 * 0.1) / 2, mWidth - (float) (mWidth / 2 * 0.1) / 2, mHeight - (float) (mWidth / 2 * 0.1) / 2);
            canvas.drawArc(rectF, 0, mDegree, false, mArcPaint);
            canvas.restore();
            mHolder.unlockCanvasAndPost(canvas);
        }
    }
    public interface OnCircleAnimationListener {
        void onAnimationPrepared(View view);
        void onAnimationFinished(View view);
        void onAnimationRunning(View view);
        void onAnimationStart(View view);
    }
}  
```
