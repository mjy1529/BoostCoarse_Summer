# 부스트코스 Android 학습 내용
<br><br>

# PJT5. 서버에서 영화정보 가져오기 Code Review
### ◆ 개요
<b>Volley와 Gson 라이브러리를 사용</b>하여 서버에서 영화목록, 영화상세, 한줄평 데이터를 응답받아 화면에 표시<br>
<table>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855170-758e9500-bd2c-11e9-8168-95f5454ab31d.png" width=""></td>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855177-78898580-bd2c-11e9-85a7-ec86e48b8600.png" width=""></td>
    <td><img src="https://user-images.githubusercontent.com/25261296/62855181-7a534900-bd2c-11e9-9ae9-6c5a273fedf5.png" width=""></td>
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
** 액티비티에서 인터페이스를 구현해야 함 **
```
public interface FragmentChangeListener {
    void onFragmentChange(String id);
}
```
