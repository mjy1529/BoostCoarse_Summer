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
+ <b>인터넷 연결된 상태</b>면 서버에서 받아온 데이터 <b>데이터베이스에 저장</b><br>
+ <b>인터넷 연결되지 않은 상태</b>면 데이터베이스에 <b>저장된 데이터 사용</b><br>
<table>
  <tr>
   <td><img src="https://user-images.githubusercontent.com/25261296/63632462-528bab80-c671-11e9-921e-08c6fbbdd188.png" width="250"></td>
   <td><img src="https://user-images.githubusercontent.com/25261296/63632463-528bab80-c671-11e9-8cf6-27bf9f37081f.png" width="250"></td>
   <td><img src="https://user-images.githubusercontent.com/25261296/63632464-528bab80-c671-11e9-94ab-7361136382a3.png" width="250"></td>
  </tr>
  <tr>
   <td align="center">인터넷이 연결된 상태</td>
   <td colspan="2" align="center">인터넷이 연결되지 않은 상태</td>
  </tr>
</table>

### ◆ Advice 1
<b>서버에서 응답 받을 때 반드시 응답코드를 확인하고 처리할 것</b><br>
#### ◇ 수정 전
```
Gson gson = new Gson();
MovieListResult result = gson.fromJson(response, MovieListResult.class);
movieList = result.result;
dbHelper.insertMovieList(movieList);
```
#### ◇ 수정 후
```
Gson gson = new Gson();
MovieListResult result = gson.fromJson(response, MovieListResult.class);

if (result.code == 200) { //응답코드 확인 후 처리
    movieList = result.result;
    dbHelper.insertMovieList(movieList);
}
```
### ◆ Advice 2
### ◆ Advice 3
### ◆ Advice 4
W/OkHttpClient: A connection to http://boostcourse-appapi.connect.or.kr:10000/ was leaked. Did you forget to close a response body?
