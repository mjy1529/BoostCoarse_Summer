# 부스트코스 Android 학습 내용<br> 

### ◆ 액티비티 수명주기 (Life Cycle)
+ <b>onCreate() → onStart() → onResume() → onPause() → onStop() → onDestroy()</b>

+ 주로 onResume()과 onPause()에서 <b>getSharedPreferences를 사용하여 값을 저장하고 복구</b><br><br>
protected void <b>onPause()</b> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;super.onPause();<br>
&nbsp;&nbsp;&nbsp;&nbsp;<b>SharedPreferences pref = getSharedPreferences("pref", Activity.MODE_PRIVATE);</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;SharedPreferences.Editor editor = pref.edit();<br>
&nbsp;&nbsp;&nbsp;&nbsp;editor.putString("name", "레드벨벳");<br>
&nbsp;&nbsp;&nbsp;&nbsp;editor.apply();<br>
}<br><br>
protected void <b>onResume()</b> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;super.onResume();<br>
&nbsp;&nbsp;&nbsp;&nbsp;<b>SharedPreferences pref = getSharedPreferences("pref", Activity.MODE_PRIVATE);</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;if&nbsp;(pref != null) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String name = pref.getString("name", "");<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
}<br><br>

### ◆ 서비스 (Service)
+ <b>화면이 없는 상태에서 백그라운드 실행</b>

+ <b>프로세스가 종료되어도 시스템에서 자동으로 재시작</b>

+ 애플리케이션 구성요소 중 하나로 매니페스트에 등록해야 함<br><br>
<service<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:name=".MyService"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:enabled="true"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:exported="true">&lt;/service><br><br>

#### ◇ 액티비티에서 서비스를 호출할 때 (Activity → Service)
+ <b>액티비티에서 Intent로 서비스 호출</b><br><br>
Intent intent = new Intent(getApplicationContext(), <b>MyService.class</b>);&nbsp;&nbsp;// 서비스 클래스<br>
intent.putExtra("command", "show");<br>
<b>startService(intent);</b>&nbsp;&nbsp;// 액티비티 호출 시엔 startActivity(intent)<br>

+ 서비스는 시스템이 시작될 때 한번 실행되기 때문에 <b>액티비티에서 전달한 데이터는 onStartCommand()에서 받는다!!</b><br>
onCreate() → onStartCommand() → onDestroy()<br><br>
public int <b>onStartCommand</b>(Intent intent, int flags, int startId) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;if&nbsp;(intent == null) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return <b>Service.START_STICKY;</b>&nbsp;&nbsp;//&nbsp;서비스가 종료되었을 때 자동으로 실행시키기 위함<br>
&nbsp;&nbsp;&nbsp;&nbsp;} else {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String command = intent.getStringExtra("command");<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
&nbsp;&nbsp;&nbsp;&nbsp;return super.onStartCommand(intent, flags, startId);<br>
}<br><br>
#### ◇ 서비스에서 액티비티를 호출할 때 (Service → Activity)
+ <b>서비스에서 Intent로 액티비티 호출</b><br><br>
Intent showIntent = new Intent(getApplicationContext(), MainActivity.class);<br>
showIntent.<b>addFlags</b>(Intent.FLAG_ACTIVITY_NEW_TASK | <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Intent.FLAG_ACTIVITY_SINGLE_TOP | <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Intent.FLAG_ACTIVITY_CLEAR_TOP);&nbsp;&nbsp;//&nbsp;화면이 없는데서 화면이 있는 걸 띄울 수 있게 함<br>
showIntent.putExtra("command", "show");<br>
startActivity(showIntent);<br><br>
+ 서비스에서 전달된 데이터는 <b>액티비티에서 onNewIntent()로 받는다!!</b><br><br>
protected void <b>onNewIntent</b>(Intent intent) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (intent != null) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String command = intent.getStringExtra("command");<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
&nbsp;&nbsp;&nbsp;&nbsp;super.onNewIntent(intent);<br>
}<br><br>

### ◆ 브로드캐스트 수신자 (Broadcast Receiver)
+ 애플리케이션 구성요소 중 하나로 매니페스트에 등록해야 함<br><br>
<b>&lt;uses-permission android:name="android.permission.RECEIVE_SMS"/&gt;&nbsp;</b>//&nbsp;SMS 수신 권한 추가<br><br>
<receiver<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:name=".SmsReceiver"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:enabled="true"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;android:exported="true"><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;intent-filter&gt;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>&lt;action android:name="android.provicer.Telephony.SMS_RECEIVED"/&gt;</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/intent-filter&gt;<br>
&lt;/receiver&gt;
<br><br><br>

# PJT3. 한줄평 화면으로 전환하기 Code Review
<table>
  <tr><td><img src="https://user-images.githubusercontent.com/25261296/62025945-8ca19300-b214-11e9-98b3-4ac83bc8ee70.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62026008-b8bd1400-b214-11e9-9ee4-be9f548f032f.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62026035-d0949800-b214-11e9-8bd8-e0a27b69df99.png" width="250"></td>   </tr>
  <tr>
    <td colspan="2" align="center">PostReviewActivity</td>
    <td align="center">ReviewListActivity</td>
  </tr>
</table>

### ◆ Advice 1
PostReviewActivity에서 사용자가 작성한 리뷰를 모두보기 리스트에 업데이트하여 적용해 보세요.<br>
> -> startActivityForResult()를 사용하여 extra로 reviewList를 받아와 해결

### ◆ Advice 2
리뷰 작성 화면(activity_post_review.xml)을 <b>가로로 회전시킬 때</b> 화면 내에 모든 아이템들이 나오지 않습니다.<br>
> -> 해결방법 : 화면 전환에 따른 UI 교체<br>
1) 가로모드용 activity_post_review.xml(land) 레이아웃 생성
2) AndroidManifest.xml에서 PostReviewActivity에 <b>android:configChanges="orientation"</b> 추가
3) PostReviewActivity에 <b>onConfigurationChanged(Configuration newConfig)</b> 작성<br><br>
public void onConfigurationChanged(Configuration newConfig) {<br>
  &nbsp;&nbsp;&nbsp;&nbsp;super.onConfigurationChanged(newConfig);<br>
  &nbsp;&nbsp;&nbsp;&nbsp;setContentView(R.layout.activity_post_review);<br>
}
<table>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/25261296/62027212-143cd100-b218-11e9-8988-eb57c4228c3d.png" height="230"></td>
    <td><img src="https://user-images.githubusercontent.com/25261296/62029334-46046680-b21d-11e9-9cbf-dda74c148e01.png" height="230"></td>
  </tr>
  <tr>
    <td colspan="2" align="center">실행 화면</td>
  </tr>
</table>
