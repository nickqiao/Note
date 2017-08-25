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
