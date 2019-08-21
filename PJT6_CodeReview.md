# 부스트코스 Android 학습 내용
### ◆ 인터넷 연결상태 확인하기
1) AndroidManifest.xml에 <b>ACCESS_NETWORK_STATE 권한 추가</b>
```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
2) 시스템 서비스 객체 중 <b>ConnectivityManager</b> 객체 사용
```
ConnectivityManager manager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
```
3) ConnectivityManager 객체의 <b>getActiveNetworkInfo() 메소드 호출</b>
 ```
 NetworkInfo networkInfo = manager.getActiveNetworkInfo();
 ```
<br><br>
# PJT6. 영화정보를 단말에 저장하기 Code Review
### ◆ 개요
서버에서 받아온 데이터를 <b>데이터베이스에 저장</b>
