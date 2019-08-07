# 부스트코스 Android 학습 내용

### ◆ 프래그먼트 (Fragment)
+ 액티비티 안에 넣는 <b>부분화면</b>

+ 부분화면을 <b>독립적</b>으로 만들어주며 액티비티를 그대로 본떠 만든 것

+ 따라서, 하나의 프래그먼트가 다른 프래그먼트에 <b>직접 접근 불가</b>

+ 액티비티 안에 있는 <b>프래그먼트 매니저가 관리</b>

+ 프래그먼트 안에 있는 <b>onCreateView()에서 인플레이션 진행</b><br><br>
public View <b>onCreateView</b>(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;<b>ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragment_main, container, false);</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;return rootView;<br>
}<br>

+ 액티비티에서 프래그먼트를 추가하는 방법<br><br>
MainFragment fragment1 = new MainFragment();<br>
<b>getSupportFragmentManager().beginTransaction().add(R.id.container, fragment1).commit();</b>

+ 프래그먼트 생명주기<br>
<b>onAttach() → onCreate() → onCreateView() → onActivityCreated() → onStart() → onResume()<br>
→ onPause() → onStop() → onDestroyView() → onDestroy() → onDetach()</b><br><br>
** 프래그먼트는 액티비티 위에 올라갔을 때 프래그먼트로서 동작할 수 있기 때문에 <br>액티비티 위에 올라갈 때 onAttach(), 액티비티에서 내려올 때 onDetach()를 호출</b>한다. **
<br><br><br>

# PJT4. 영화목록과 바로가기 메뉴 Code Review
### ◆ Advice 1
