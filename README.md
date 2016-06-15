### 背景三张图片循环交替显示的登录界面

用帧动画可以实现多张图片交替显示，但是貌似不能设置交替效果，比如淡入淡出
使用属性动画实现。


##### 实现效果
![image](https://github.com/lololiu/demo4popupwindow/raw/master/screenshots/screenshot.gif)

##### 关键代码：
```java
    private void startAnimation() {
        ObjectAnimator anim1 = new ObjectAnimator().ofFloat(mImageView1, "alpha", 1f, 0f).setDuration(5000);
        ObjectAnimator anim2 = new ObjectAnimator().ofFloat(mImageView2, "alpha", 0f, 1f).setDuration(5000);
        AnimatorSet set = new AnimatorSet();
        set.playTogether(anim1, anim2);

        ObjectAnimator anim3 = new ObjectAnimator().ofFloat(mImageView2, "alpha", 1f, 0f).setDuration(5000);
        ObjectAnimator anim4 = new ObjectAnimator().ofFloat(mImageView3, "alpha", 0f, 1f).setDuration(5000);
        AnimatorSet set1 = new AnimatorSet();
        set1.playTogether(anim3, anim4);

        ObjectAnimator anim5 = new ObjectAnimator().ofFloat(mImageView3, "alpha", 1f, 0f).setDuration(5000);
        ObjectAnimator anim6 = new ObjectAnimator().ofFloat(mImageView1, "alpha", 0f, 1f).setDuration(5000);
        AnimatorSet set2 = new AnimatorSet();
        set2.playTogether(anim5, anim6);

        AnimatorSet set3 = new AnimatorSet();
        set3.playSequentially(set, set1, set2);
        set3.addListener(new AnimatorListenerAdapter() {

            private boolean mCanceled;

            @Override
            public void onAnimationStart(Animator animation) {
                mCanceled = false;
            }

            @Override
            public void onAnimationCancel(Animator animation) {
                mCanceled = true;
            }

            @Override
            public void onAnimationEnd(Animator animation) {
                if (!mCanceled) {
                    animation.start();
                }
            }

        });
        set3.start();
    }

```