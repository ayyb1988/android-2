# android
2015年8月2日03:15:33
####Android ObjectAnimator 动画，透明度，平移，旋转，拉伸，背景颜色，动画集合
___
* alpha
```
		//透明度变化动画
        //第一个参数为 view对象，第二个参数为 动画改变的类型，第三，第四个参数依次是开始透明度和结束透明度。
        ObjectAnimator alphaAnimator = ObjectAnimator.ofFloat(iv, "alpha", 1f, 0f);
        alphaAnimator.setDuration(2000);//设置动画时间
        alphaAnimator.setInterpolator(new DecelerateInterpolator());//设置动画插入器，减速
        alphaAnimator.setRepeatCount(-1);//设置动画重复次数，这里-1代表无限
        alphaAnimator.setRepeatMode(Animation.REVERSE);//设置动画循环模式。
        alphaAnimator.start();//启动动画。
        alphaAnimator.addListener(new Animator.AnimatorListener() {
            @Override
            public void onAnimationStart(Animator animator) {

            }

            @Override
            public void onAnimationEnd(Animator animator) {
                //08-01 17:31:20.979  13300-13300/com.example.hp.animations I/debug﹕ 0
                Log.i("debug", iv.getVisibility() + "");
                //只是透明度变化，状态依然是visible
            }

            @Override
            public void onAnimationCancel(Animator animator) {

            }

            @Override
            public void onAnimationRepeat(Animator animator) {

            }
        });
```
* scanX
```
        //左右拉伸动画
        ObjectAnimator scaleX = ObjectAnimator.ofFloat(iv, "scaleX", 1f, 0f);
        scaleX.setDuration(3000);
        scaleX.setRepeatCount(-1);
        scaleX.setInterpolator(new DecelerateInterpolator());
        scaleX.setRepeatMode(Animation.REVERSE);
        scaleX.start();
```
* scanY
```
        //上下拉伸动画
        ObjectAnimator scaleY = ObjectAnimator.ofFloat(iv, "scaleY", 1f, 0f);
        scaleY.setDuration(3000);
        scaleY.setRepeatCount(-1);
        scaleY.setInterpolator(new DecelerateInterpolator());
        scaleY.setRepeatMode(Animation.REVERSE);
        scaleY.start();
```
* translate
```
        //平移动画,三四个参数是从什么坐标移动到什么坐标
        //ObjectAnimator translate = ObjectAnimator.ofFloat(iv, "x", iv.getX(), 0f);
        ObjectAnimator translate = ObjectAnimator.ofFloat(iv, "y", iv.getY(), -20f);
        translate.setDuration(3000);
        translate.setRepeatCount(-1);
        translate.setInterpolator(new DecelerateInterpolator());
        translate.setRepeatMode(Animation.REVERSE);
        translate.start();
```
* rotate
```
        //rotate 旋转动画,纵向旋转180度（上下翻转）
        ObjectAnimator rotate = ObjectAnimator.ofFloat(iv, "rotationX", 0f, 180f);
        rotate.setDuration(3000);
        rotate.setRepeatCount(-1);
        rotate.setInterpolator(new DecelerateInterpolator());
        rotate.setRepeatMode(Animation.REVERSE);
        rotate.start();
```
```
        //rotate 旋转动画,横向旋转180度（左右翻转）
        ObjectAnimator rotate = ObjectAnimator.ofFloat(iv, "rotationY", 0f, 180f);
        rotate.setDuration(3000);
        rotate.setRepeatCount(-1);
        rotate.setInterpolator(new DecelerateInterpolator());
        rotate.setRepeatMode(Animation.REVERSE);
        rotate.start();
```
* backgroudColor
```
        //改变背景颜色的动画
        ObjectAnimator backgroundColor = ObjectAnimator.ofInt(iv,
                "backgroundColor", Color.RED, Color.BLUE, Color.GRAY,
                Color.GREEN);
        backgroundColor.setDuration(3000);
        backgroundColor.setRepeatCount(-1);
        backgroundColor.setInterpolator(new DecelerateInterpolator());
        backgroundColor.setRepeatMode(Animation.REVERSE);
                /*
         * ArgbEvaluator：这种评估者可以用来执行类型之间的插值整数值代表ARGB颜色。
         * FloatEvaluator：这种评估者可以用来执行浮点值之间的插值。
         * IntEvaluator：这种评估者可以用来执行类型int值之间的插值。
         * RectEvaluator：这种评估者可以用来执行类型之间的插值矩形值。
         *
         * 由于本例是改变View的backgroundColor属性的背景颜色所以此处使用ArgbEvaluator
         */

        backgroundColor.setEvaluator(new ArgbEvaluator());
        backgroundColor.start();
```
* AnimatorSet（动画集合）
```
        //动画集合播放
        AnimatorSet animatorSet = new AnimatorSet();

        ObjectAnimator scaleX = ObjectAnimator.ofFloat(iv, "scaleX", 1f, 0.5f);
        scaleX.setDuration(3000);
        ObjectAnimator scaleY = ObjectAnimator.ofFloat(iv, "scaleY", 1f, 0.5f);
        scaleY.setDuration(3000);
        ObjectAnimator rotate = ObjectAnimator.ofFloat(iv, "rotationX", 0f, 180f);
        rotate.setDuration(3000);
        ObjectAnimator translate = ObjectAnimator.ofFloat(iv, "y", iv.getY(), -20f);
        translate.setDuration(3000);
        //先执行scaleX动画之后在执行scaleY
        animatorSet.play(scaleX).before(scaleY);
        //先执行translate之后执行rotate
        animatorSet.play(rotate).after(translate);//scaleX和translate一起开始

        //同时执行
//        animatorSet.play(scaleX).with(scaleY);
        animatorSet.start();
```
