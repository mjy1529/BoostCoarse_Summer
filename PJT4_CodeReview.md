# 부스트코스 Android 학습 내용

### ◆ 프래그먼트 (Fragment)
+ 액티비티 안에 넣는 <b>부분화면</b>

+ 부분화면을 <b>독립적으로</b> 만들어주며 액티비티를 그대로 본떠 만든 것

+ 따라서, 하나의 프래그먼트가 다른 프래그먼트에 <b>직접 접근 불가</b>

+ 액티비티 안에 있는 <b>프래그먼트 매니저가 관리</b>

+ 프래그먼트 생명주기<br>
<b>onAttach() → onCreate() → onCreateView() → onActivityCreated() → onStart() → onResume()<br>
→ onPause() → onStop() → onDestroyView() → onDestroy() → onDetach()</b>

+ 프래그먼트는 액티비티 위에 올라갔을 때 프래그먼트로서 동작할 수 있기 때문에<br><b>액티비티 위에 올라갈 때 onAttach(), 액티비티에서 내려올 때 onDetach()를 호출</b>한다.

+ 프래그먼트 안에 있는 <b>onCreateView()</b>에서 인플레이션 진행
```
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
   ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_main, container, false);
   return rootView;
}
```

#### ◇ 액티비티에서 프래그먼트를 추가하는 방법
```
MainFragment fragment1 = new MainFragment();
getSupportFragmentManager().beginTransaction().add(R.id.container, fragment1).commit();
```

#### ◇ XML 레이아웃에 추가된 프래그먼트 호출하는 방법
<b>activity_main.xml</b><br>
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <fragment
        android:id="@+id/listFragment"
        android:name="com.juyoung.myfragment.ListFragment"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

</LinearLayout>
```
<b>MainActivity.class</b>
```
ListFragment listFragment = (ListFragment) getSupportFragmentManager().findFragmentById(R.id.listFragment);
```
<br><br>
# PJT4. 영화목록과 바로가기 메뉴 Code Review
<table>
  <tr><td><img src="https://user-images.githubusercontent.com/25261296/62728177-1132b380-ba56-11e9-9895-d33faf5c5ad5.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62728184-13950d80-ba56-11e9-88e6-d925796447cd.png" width="250"></td>
     <td><img src="https://user-images.githubusercontent.com/25261296/62728336-7f777600-ba56-11e9-9a7d-86e93ae80ac6.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62728187-155ed100-ba56-11e9-8ee2-25cc43a34eb4.png" width="250"></td>
     </tr>
  <tr>
    <td colspan="2" align="center">MovieListFragment (ViewPager 사용)</td>
    <td align="center">MovieDetailFragment</td>
     <td align="center">바로가기 메뉴</td>
  </tr>
</table>

### ◆ Advice 1
> 사용하지 않는 import는 삭제하고 제출할 것
### ◆ Advice 2
> 
