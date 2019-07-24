# PJT1. 영화상세 화면 만들기 Code Review

<img src="https://user-images.githubusercontent.com/25261296/61787012-dae81800-ae49-11e9-8eb1-ee33e07bfd19.png" width="250"> <img src="https://user-images.githubusercontent.com/25261296/61787193-403c0900-ae4a-11e9-829d-0e4fa98b3f89.png" width="250">

### ◆ Advice 1
> 프로젝트를 통째로 전달 시에는 반드시 <b>clean build</b>를 하고 전송해야 함.

### ◆ Advice 2
> xml 파일에서 id에 대한 naming은 일반적으로 <b>헝가리언 표기법</b>과 <b>snake case</b>를 혼용하여 사용함. 

<br>

#### cf) 변수 네이밍
* Lower Camel Case
  * 각 단어의 첫 문자를 대문자로 표시하되, 이름의 첫 문자는 소문자로 적는다.
  * ex) camelCase
  
* Upper Camel Case
  * 각 단어의 첫 문자를 대문자로 표시한다.
  * ex) CamelCase
  
* Snake Case
  * 각 단어의 사이를 언더바(_)로 구분한다.
  * ex) snake_case
  
* Hungarian Notation (헝가리안 표기법)
  * 이름 앞에 변수 타입을 접두어로 넣어준다.
  * 접두어 : ch - char, db-double, str-string, b-boolean 등
  * ex) chHungarian
  
###### [참고] http://guswnsxodlf.github.io/camelcase-pascalcase-snakecase
