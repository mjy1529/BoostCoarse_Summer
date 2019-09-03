# PJT7. 사진보기와 동영상 재생 Code Review
### ◆ 개요
+ 영화상세 화면에 <b>갤러리 목록을 추가</b>하여 사진과 동영상을 볼 수 있게 함
<table>
    <tr>
        <td><img src="https://user-images.githubusercontent.com/25261296/64137487-79956a80-ce33-11e9-9808-2ae6fdb014af.png"></td>
        <td><img src="https://user-images.githubusercontent.com/25261296/64137488-79956a80-ce33-11e9-9aee-319fb00db804.png"></td>
        <td><img src="https://user-images.githubusercontent.com/25261296/64137489-7a2e0100-ce33-11e9-83be-baea8a9687f8.png"></td>
        <td><img src="https://user-images.githubusercontent.com/25261296/64137659-95e5d700-ce34-11e9-9442-f1f8137ec936.png"></td>
    </tr>
    <tr>
        <td colspan="2" align="center">갤러리 Recyclerview 추가</td>
        <td align="center">사진보기 Activity 추가</td>
        <td align="center">url 링크로 동영상 재생</td>
    </tr>
</table>

### ◆ Advice 1
<b>변수명을 i로 사용하지 말 것</b><br>
일반적으로 <b>i, n은 지역변수로 너무 많이 사용하는 변수명</b>이므로 공동작업이 이루어질 때 다른 개발자가 모르고 for문 등에서 i를 지역변수로 선언할 경우가 발생함. <b>특히나 전역변수로는 절대 사용하면 안됨!!</b>
+ 매개변수 i를 position으로 수정

### ◆ Advice 2
<b>split()로 나누기 전의 값을 객체에 담아서 사용할 것</b>
#### ◇ 수정 전
+ data.getPhotos(=서버에서 받은 photos Url), data.getVideos(=서버에서 받은 videos Url)을 바로 사용
```
if (data.getPhotos() != null) {
    String[] photos = data.getPhotos().split(",");
    ...
}

if (data.getVideos() != null) {
    String[] videos = data.getVideos().split(",");
    ...
}
```
#### ◇ 수정 후
+ photoStr, videoStr 객체에 저장하여 사용
```
String photoStr = data.getPhotos();
String videoStr = data.getVideos();

if (photoStr != null) {
    String[] photos = photoStr.split(",");
    ...
}

if (videoStr != null) {
    String[] videos = videoStr.split(",");
    ...
}
```
### ◆ Advice 3
<b>ViewPager의 PageLimit을 상수가 아닌 서버에서 받은 영화 리스트 사이즈로 생성할 것</b><br>
#### ◇ 수정 전
```
viewPager.setOffscreenPageLimit(5);
```
#### ◇ 수정 후
```
viewPager.setOffscreenPageLimit(movieList.size());
```

### ◆ Advice 4
** Adevice 4부터는 이번 프로젝트 관련 내용이 아닌 [PJT6 CodeReview의 Advice5](https://github.com/mjy1529/BoostCourse_Android/blob/master/PJT6_CodeReview.md#-advice-5)를 적용한 후 받은 리뷰입니다. **<br><br>
<b>CommentAdapter에서 '추천하기' 서버연동 역시 클래스로 분리하여 구현할 것!!</b><br>
일반적으로 서버는 개발 및 테스트를 위해 보통 2~3대를 사용하며 그만큼 필요한 정보들(요청 URL, 파라미터, 요청 방식 등)이 많아지기 때문에 서버연동 객체를 각각 두며 <b>서버 연동규격서를 기준</b>으로 구현되어야 한다.<br>
#### cf. 서버 연동과 데이터베이스를 모듈로 분리하여 수정한 클래스 구조
<table>
    <tr>
        <td><img src="https://user-images.githubusercontent.com/25261296/64155978-d82c0a00-ce6e-11e9-9432-066395581a67.PNG" width="150"></td>
        <td><img src="https://user-images.githubusercontent.com/25261296/64155974-d7937380-ce6e-11e9-9087-4bb939eb43db.PNG" width="150"></td>
        <td><img src="https://user-images.githubusercontent.com/25261296/64155976-d7937380-ce6e-11e9-89f2-40bf57370775.PNG" width="150"></td>
    </tr>
    <tr>
        <td align="center">전체 클래스 구조</td>
        <td align="center">adapter와 data</td>
        <td align="center">netwrok와 database</td>
    </tr>
</table>

### ◆ Advice 5

### ◆ Advice 6

### ◆ Question

<br><br>

# 부스트코스 Android 학습 내용
### ◆ 음악 재생하기
+ play audio
```
MediaPlayer player = new MediaPlayer();
player.setDataSource(url);
player.prepare();
player.start();
```

+ pause audio
```
if (player != null) {
    position = player.getCurrentPosition(); //position 변수에 재생 위치 저장
    player.pause();
}
```

+ resume audio
```
if (player != null && !player.isPlaying()) {
    player.seekTo(position);
    player.start();
}
```

+ stop audio
```
if (player != null && player.isPlaying()) {
    player.stop();
}
```
### ◆ 동영상 재생하기
<img src="https://user-images.githubusercontent.com/25261296/64033597-bccbb100-cb87-11e9-9351-dbf7d350f423.png" width="180"><br>
+ videoView 세팅
```
MediaController controller = new MediaController(this); //재생이나 중지 버튼을 위한 controller
videoView.setMediaController(controller);

videoView.setVideoURI(Uri.parse(url));
videoView.requestFocus(); //동영상 정보 가져옴

videoView.setOnPreparedListener(new MediaPlayer.OnPreparedListener() { 
    @Override
    public void onPrepared(MediaPlayer mp) { //videoView가 재생준비 되었을 때 호출
        Toast.makeText(MainActivity.this, "동영상 준비됨.", Toast.LENGTH_SHORT).show();
    }
});
```
+ play video
```
videoView.seekTo(0); //처음부터 실행
videoView.start();
```
#### ☆ 추가 학습 내용
+ <b>onBackPressed() vs finish()</b><br>
<b>→ Intent를 통해 Data를 넘겨줄 때는 finish(), 아무 데이터를 넘겨주지 않을 때는 onBackPressed() 사용</b><br>
** finish() 호출 시 액티비티 종료(= onDestroy() 호출) **<br>
> [참고] https://m.blog.naver.com/PostView.nhn?blogId=itsme0124&logNo=192940956&proxyReferer=https%3A%2F%2Fwww.google.com%2F

+ <b>싱글톤 패턴 vs static 클래스의 차이</b><br>
→ 싱글톤 : 

+ arraylist와 vector의 차이
<br><br>
