# AndroidTraining
https://developer.android.com/training/index.html

# Supporting Different Screens
## Create Different Layouts
```
MyProject/
    res/
        layout/              # default (portrait)
            main.xml
        layout-land/         # landscape
            main.xml
        layout-large/        # large (portrait)
            main.xml
        layout-large-land/   # large landscape
            main.xml
```
## Create Different Bitmaps
```
MyProject/
    res/
        drawable-xhdpi/
            awesomeimage.png
        drawable-hdpi/
            awesomeimage.png
        drawable-mdpi/
            awesomeimage.png
        drawable-ldpi/
            awesomeimage.png
```

# Supporting Different Platform Versions
## Specify Minimum and Target API Levels
**AndroidManifest.xml**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" ... >
    <uses-sdk android:minSdkVersion="4" android:targetSdkVersion="15" />
    ...
</manifest>
```
## Check System Version at Runtime
```java
private void setUpActionBar() {
    // Make sure we're running on Honeycomb or higher to use ActionBar APIs
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB) {
        ActionBar actionBar = getActionBar();
        actionBar.setDisplayHomeAsUpEnabled(true);
    }
}
```
## Use Platform Styles and Themes
```xml
<activity android:theme="@android:style/Theme.Dialog">
<activity android:theme="@android:style/Theme.Translucent">
<activity android:theme="@style/CustomTheme">
<application android:theme="@style/CustomTheme">
```

# Starting an Activity

## Understand the Lifecycle Callbacks
![](https://developer.android.com/images/training/basics/basic-lifecycle.png)

## Specify Your App's Launcher Activity
```xml
<activity android:name=".MainActivity" android:label="@string/app_name">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

**If either the MAIN action or LAUNCHER category are not declared for one of your activities, then your app icon will not appear in the Home screen's list of apps**

## Create a New Instance
**Once the onCreate() finishes execution, the system calls the onStart() and onResume() methods in quick succession**

##　Destroy the Activity
**if your activity includes background threads that you created during onCreate() or other long-running resources that could potentially leak memory if not properly closed, you should kill them during onDestroy().
**

# Pausing and Resuming an Activity

## Pause Your Activity
```java
@Override
public void onPause() {
    super.onPause();  // Always call the superclass method first

    // Release the Camera because we don't need it when paused
    // and other activities might need to use it.
    if (mCamera != null) {
        mCamera.release();
        mCamera = null;
    }
}
```

## Resume Your Activity
```java
@Override
public void onResume() {
    super.onResume();  // Always call the superclass method first

    // Get the Camera instance as the activity achieves full user focus
    if (mCamera == null) {
        initializeCamera(); // Local method to handle camera init
    }
}
```

# Stopping and Restarting an Activity

## Stop Your Activity
**Even if the system destroys your activity while it's stopped, it still retains the state of the View objects**

## Start/Restart Your Activity
**When the system destroys your activity, it calls the onDestroy() method for your Activity**

# Recreating an Activity

## Save Your Activity State
**As your activity begins to stop, the system calls onSaveInstanceState() so your activity can save state information with a collection of key-value pairs**

## Restore Your Activity State
**Both the onCreate() and onRestoreInstanceState() callback methods receive the same Bundle that contains the instance state information**
