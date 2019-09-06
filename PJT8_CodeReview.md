# 부스트코스 Android 학습 내용
### ◆ 스플래시 화면
> styles.xml
```
<style name="SplashTheme" parent="Theme.AppCompat.NoActionBar">
    <item name="android:windowBackground">@drawable/splash_background</item>
</style>
```

> AndroidManifest.xml
```
<application>
    <activity
        android:name=".SplashActivity"
        android:theme="@style/SplashTheme"> //SplashTheme 적용
    </activity>
 </application>
```
