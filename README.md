# psandroidanim
##2. Understanding View Animation
###1 Overview of View Animation
two ways:
XML file in res/anim, java code
The elements performing animations:
```
<alpha>
<scale>
<translate>
<rotate>
```
can use ```<set>``` to group


###2 Elements Performing Tween Animation
####alpha
```
android:fromAlpha  (0.0=transparent 1.0=opaque)
android:toAlpha
```
####scale
```
android:fromXScale
android:toXScale
android:pivotX
```
```
android:fromYScale
android:toYScale
android:pivotY
```

#####sample: scale up an image to 1.5 times pivoted at center
```
<scale 
android:fromXScale ="1.0"
android:toXScale ="1.5"
android:fromYScale="1.0"
android:toYScale="1.5"
android:pivotX="50%"
android:pivotY="50%"
android:duration="500"
/>
```


####translate
```
android:fromXDelta
android:toXDelta
android:fromYDelta
android:toYDelta
```

#####sample: move image 50px in positive x axis
```
<translate 
android:fromXDelta="0"
android:toXDelta="50"
android:fromYDelta="0"
android:toYDelta="0"
android:duration="500"
/>
```
####rotate
```
android:fromDegrees
android:toDegrees
android:pivotX
android:pivotY
```
#####sample move image 360 degree 1.5 seconds
```
<translate 
android:fromDegrees="0"
android:toDegrees="360"
android:pivotX="50%"
android:pivotY="50%"
android:duration="1500"
/>
```
###3 Implement Tween Animation Through Animation Resource Files
MainActivity.java
```
private ImageView mImageView;
private Animation mRotateAnim;

@Override
protected void onCreate(Bundle savedInstanceState){
  super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_main)
  mImageView = (ImageView)findViewById(R.id.volleyball);
}

....
public void scaleAnimation(View view){
  mScaleAnim = AnimationUtils.loadAnimation)this,R.anim.scale_anim);
  
}

```

res/anim/alpha_anim.xml
```
<alpha
android:duration="2000"
android:fromAlpha="1.0"
android:toAlpha="0.0"
/>
```

Note these animation is not permanent, it will return to its original state(solve this next lecture)

###4 Animation Listener
####onAnimationEnd
- notifies the end of the animation.
- this callback is not invoked for animations with repeat count set to infinite

####onAnimationRepeat


Ex
```
public class MainActivity extends ActionBarActivity implements Animation.AnimationListener{
}
```





##5. Applying Animations to Commmon Apps Scenario
###1 Activity Transition
exp, overridePendingTransition  


MainActivity.java
```
public void slideTransition(View view){
  startActivity(new Intent(MainActivity.this,SecondActivity.class);
  overridePendingTransition(R.anim.activity_open_translate,R.anim.activity_close_scale);
}
```

SecondActivity.java
```
//go back to first Activity if we press `back` button
@Override
protected void onPause(){
  super.onPause()
  overridePendingTransition(R.anim.activity_open_scale,R.anim.activity_close_translate);
  //first->ingoing activity  //second->outgoing activity
}
```

%p->means relative to parent.Ex: activity_push_up_out.xml,(typically, out animation xml needs to add p, like 100%p)
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk.res.android">    
<translate android:toYDelta="-100%p" android:fromYDelta="0%p" android:duraion..../>
<alpha android:toAlpha="0.5" android:fromAlpha="1.0" android:duraion..../>
</set>
```
activity_push_up_in.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk.res.android">    
<translate android:toYDelta="0%" android:fromYDelta="100%" android:duraion..../>
<alpha android:toAlpha="1.0" android:fromAlpha="0.0" android:duraion..../>
</set>
```
