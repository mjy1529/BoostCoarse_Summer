# PJT3. 한줄평 화면으로 전환하기
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
