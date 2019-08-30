# 부스트코스 Android 학습 내용
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
+ 동영상 재생
```
videoView.seekTo(0); //처음부터 실행
videoView.start();
```
#### ★ 추가 학습 내용
+ <b>onBackPressed() vs finish()</b><br>
<b>→ Intent를 통해 Data를 넘겨줄 때는 finish(), 아무 데이터를 넘겨주지 않을 때는 onBackPressed() 사용</b><br>
** finish() 호출 시 액티비티 종료(= onDestroy() 호출) **<br>
> [참고] https://m.blog.naver.com/PostView.nhn?blogId=itsme0124&logNo=192940956&proxyReferer=https%3A%2F%2Fwww.google.com%2F

+ <b>싱글톤 패턴 vs static 클래스의 차이</b><br>
→ 싱글톤 : 

+ arraylist와 vector의 차이
<br><br>
# PJT7. 사진보기와 동영상 재생 Code Review
