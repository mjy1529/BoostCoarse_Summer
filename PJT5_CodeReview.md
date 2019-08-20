# 부스트코스 Android 학습 내용
### ◆ Volley 사용법
+ build.gradle (Module:app)에 라이브러리 추가
```
implementation 'com.android.volley:volley:1.1.0'
```
+ AndroidManifest.xml에 인터넷 권한 추가
```
<uses-permission android:name="android.permission.INTERNET"/>
```
+ Java 코드 작성
```
StringRequest request = new StringRequest(
        Request.Method.GET, //GET 방식으로 요청
        AppHelper.URL + "/movie/readMovieList?type=" + type, // 웹서버 URL
        new Response.Listener<String>() { //응답 받았을 때 호출
            @Override
            public void onResponse(String response) {
                processCommentResponse(response);
            }
        },
        new Response.ErrorListener() { //에러 발생 시 호출
            @Override
            public void onErrorResponse(VolleyError error) {
                Log.d(TAG, "get movie list fail : " + error.getMessage());
            }
        }
);
request.setShouldCache(false);
AppHelper.requestQueue.add(request); //요청 객체(request) 요청 큐에 넣기
```

### ◆ Gson 사용법
+ JSON 문자열을 자바 객체로 변환해주는 라이브러리

+ build.gradle (Module:app)에 라이브러리 추가
```
implementation 'com.google.code.gson:gson:2.8.2'
```
+ JSON에 맞는 자바 클래스 정의<br>
이때, 변수 이름과 자료형은 JSON 속성의 이름, 자료형과 같아야 함

+ Gson 사용하여 변환
```
Gson gson = new Gson();

// MovieListResult 클래스 객체로 변환  
MovieListResult listResult = gson.fromJson(response, MovieListResult.class);    
```
<br>

# PJT5. 서버에서 영화정보 가져오기 Code Review
### ◆ 개요
<b>Volley와 Gson 라이브러리를 사용</b>하여 서버에서 영화목록, 영화상세, 한줄평 데이터를 응답받아 화면에 표시<br>
<table>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855170-758e9500-bd2c-11e9-8168-95f5454ab31d.png"></td>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855177-78898580-bd2c-11e9-85a7-ec86e48b8600.png"></td>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855181-7a534900-bd2c-11e9-9ae9-6c5a273fedf5.png"></td>
  </tr>
 </table>
 
### ◆ Advice 1
※ 주의사항
+ 멤버변수에 접근제어자 붙이기

+ 0, 1과 같은 값은 상수로 정의하기<br>
ex) public static final int POST_COMMENT_ACTIVITY = 0;

+ <b>패키지명은 소문자로</b> 작성하기

### ◆ Advice 2
<b>프래그먼트 인터페이스를 별도의 클래스로 작성할 것</b><br>

<b>(액티비티에서 인터페이스를 구현)</b>
```
public interface FragmentChangeCallback {
    void onFragmentChange(String id);
}
```
