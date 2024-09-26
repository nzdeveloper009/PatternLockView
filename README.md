![PatternLockView](screenshots/pattern-lock-view-banner.png?raw=true)

# PatternLockView
An easy-to-use, customizable, Material Design ready Pattern Lock view for Android.


This library allows you to implement pattern locking mechanism in your app **easily and quickly**. It is very easy to use and there are **plenty of customization options** available to change the functionality and look-and-feel of this view to match your needs.


![PatternLockView](screenshots/pattern_lock_view_small.gif?raw=true) ![PatternLockView](screenshots/pattern_lock_view_2_small.gif?raw=true)



## Add the JitPack repository to your build file
```
dependencyResolutionManagement {
		repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
		repositories {
			mavenCentral()
			maven { url 'https://jitpack.io' }
		}
	}
```

``` Add the dependency
dependencies {
    implementation("com.github.nzdeveloper009:PatternLockView:1.0.0")
}
```

### Step 1

Place the view in your XML layout file.

```xml
    <com.nokhaiz.PatternLockView
        android:id="@+id/pattern_lock_view"
        android:layout_width="280dp"
        android:layout_height="280dp"/>
```

This is enough to get the view rendered in your layout. But you would certainly want to add a callback listener to listen to pattern changes.

### Step 2

Reference the view in code and add a listener to it.

```java
mPatternLockView = (PatternLockView) findViewById(R.id.pattern_lock_view);
mPatternLockView.addPatternLockListener(mPatternLockViewListener);
```

Implement the listener interface as follows,

```java
private PatternLockViewListener mPatternLockViewListener = new PatternLockViewListener() {
        @Override
        public void onStarted() {
            Log.d(getClass().getName(), "Pattern drawing started");
        }

        @Override
        public void onProgress(List<PatternLockView.Dot> progressPattern) {
            Log.d(getClass().getName(), "Pattern progress: " +
                    PatternLockUtils.patternToString(mPatternLockView, progressPattern));
        }

        @Override
        public void onComplete(List<PatternLockView.Dot> pattern) {
            Log.d(getClass().getName(), "Pattern complete: " +
                    PatternLockUtils.patternToString(mPatternLockView, pattern));
        }

        @Override
        public void onCleared() {
            Log.d(getClass().getName(), "Pattern has been cleared");
        }
    };
```

And that's it! Your PatternLockView is ready to rock. You might also want to remove the listeners when not needed,         `removePatternLockListener(mPatternLockViewListener);`


### XML (Quick and Easy)

You can add various attributes to the PatternLockView from your XML layout.

```xml
  app:dotCount="3"                                        // Change the no.of dots in a row (or column)
  app:dotNormalSize="12dp"                                // Change the size of the dots in normal state
  app:dotSelectedSize="24dp"                              // Change the size of the dots in selected state
  app:pathWidth="4dp"                                     // Change the width of the path
  app:aspectRatioEnabled="true"                           // Set if the view should respect custom aspect ratio
  app:aspectRatio="square"                                // Set between "square", "width_bias", "height_bias"
  app:normalStateColor="@color/white"                     // Set the color of the pattern view in normal state
  app:correctStateColor="@color/primary"                  // Set the color of the pattern view in correct state
  app:wrongStateColor="@color/pomegranate"                // Set the color of the pattern view in error state     
  app:dotAnimationDuration="200"                          // Change the duration of the animating dots
  app:pathEndAnimationDuration="100"                      // Change the duration of the path end animaiton
```

### JAVA (Programatically)

You can also programatically change the properties of the view, thereby having more control over it.

```java
mPatternLockView.setViewMode(PatternLockView.PatternViewMode.CORRECT);       // Set the current viee more 
mPatternLockView.setInStealthMode(true);                                     // Set the pattern in stealth mode (pattern drawing is hidden)
mPatternLockView.setTactileFeedbackEnabled(true);                            // Enables vibration feedback when the pattern is drawn
mPatternLockView.setInputEnabled(false);                                     // Disables any input from the pattern lock view completely

mPatternLockView.setDotCount(3);
mPatternLockView.setDotNormalSize((int) ResourceUtils.getDimensionInPx(this, R.dimen.pattern_lock_dot_size));
mPatternLockView.setDotSelectedSize((int) ResourceUtils.getDimensionInPx(this, R.dimen.pattern_lock_dot_selected_size));
mPatternLockView.setPathWidth((int) ResourceUtils.getDimensionInPx(this, R.dimen.pattern_lock_path_width));
mPatternLockView.setAspectRatioEnabled(true);
mPatternLockView.setAspectRatio(PatternLockView.AspectRatio.ASPECT_RATIO_HEIGHT_BIAS); 
mPatternLockView.setNormalStateColor(ResourceUtils.getColor(this, R.color.white));
mPatternLockView.setCorrectStateColor(ResourceUtils.getColor(this, R.color.primary));
mPatternLockView.setWrongStateColor(ResourceUtils.getColor(this, R.color.pomegranate));
mPatternLockView.setDotAnimationDuration(150);
mPatternLockView.setPathEndAnimationDuration(100);

```
