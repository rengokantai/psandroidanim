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

```
