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
<br>

# PJT4. 영화목록과 바로가기 메뉴 Code Review
<table>
  <tr><td><img src="https://user-images.githubusercontent.com/25261296/62728177-1132b380-ba56-11e9-9895-d33faf5c5ad5.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62728184-13950d80-ba56-11e9-88e6-d925796447cd.png" width="250"></td>
     <td><img src="https://user-images.githubusercontent.com/25261296/62728336-7f777600-ba56-11e9-9a7d-86e93ae80ac6.png" width="250"></td>
      <td><img src="https://user-images.githubusercontent.com/25261296/62728187-155ed100-ba56-11e9-8ee2-25cc43a34eb4.png" width="250"></td>
     </tr>
  <tr>
    <td colspan="2" align="center">영화 목록<br>(MovieListFragment)</td>
    <td align="center">상세보기 (MovieDetailFragment)</td>
     <td align="center">바로가기 메뉴</td>
  </tr>
</table>

### ◆ Advice 1
※ 주의사항<br>
사용하지 않는 import는 삭제 후 제출하기

### ◆ Advice 2
<b>동일한 MovieFragment와 fragment_movie.xml 중복 사용 금지</b>
#### ◇ 수정 전
+ MovieFragment의 java 파일과 xml 파일을 각각 다섯 개씩 생성하여 사용
```
MovieFragment movieFragment = new MovieFragment();
adapter.addItem(movieFragment2);

MovieFragment2 movieFragment2 = new MovieFragment2();
adapter.addItem(movieFragment2);

...

MovieFragment5 movieFragment5 = new MovieFragment5();
adapter.addItem(movieFragment5);
```
#### ◇ 수정 후
+ 하나의 fragment와 하나의 xml 파일 사용

+ MovieFragment에 <b>newInstance() 메소드 추가</b>하여 bundle로 데이터 전달

+ fragment_movie.xml 각 뷰에 전달받은 데이터 업데이트
> MovieFragment
```
public MovieFragment newInstance(int imageId, String title, String info) {
     MovieFragment fragment = new MovieFragment();

     Bundle bundle = new Bundle();
     bundle.putInt("imageId", imageId);
     bundle.putString("title", title);
     bundle.putString("info", info);
     fragment.setArguments(bundle);

     return fragment;
}
```
> MovieListFragment
```
MovieFragment movieFragment = new MovieFragment()
      .newInstance(R.drawable.image1, "1. 군 도", "예매율 61.3% | 15세 관람가 | D-1");
adapter.addItem(movieFragment);

MovieFragment movieFragment2 = new MovieFragment()
      .newInstance(R.drawable.image2, "2. 공 조", "예매율 61.6% | 15세 관람가 | D-1");;
adapter.addItem(movieFragment2);

MovieFragment movieFragment5 = new MovieFragment()
      .newInstance(R.drawable.image3, "5. 더 킹", "예매율 11.2%% | 12세 관람가");
adapter.addItem(movieFragment5);
```

### ◆ Advice 3
> Fragment에서 MainActivity 선언 해서 사용 하지 않기(상호 참조 제거)
