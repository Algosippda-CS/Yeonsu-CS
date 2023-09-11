# 📌 MVVM 패턴 (MVVM pattern)
: MVC의 C에 해당하는 컨트롤러가 뷰모델(View model)로 바뀐 패턴   
Model - View - View Model   

<br/>

![IMG_4BEC6D3B742D-1](https://github.com/Algosippda-CS/Yeonsu-CS/assets/82032452/4da3ea08-9599-4258-a47a-dc36e437ba6e)


## View Model (뷰 모델)
: 뷰를 더 추상화한 계층   
View Model과 View는 `1:n 관계`이다.

## MVVM 패턴의 특징
- MVC 패턴과는 다르게 커맨드와 데이터 바인딩을 가진다.
- 뷰와 뷰모델 사이의 양방향 데이터 바인딩을 지원한다.
- UI를 별도의 코드 수정 없이 재사용할 수 있다.
- 단위 테스팅하기 쉽다.

### 🔹 커맨드 (Command)
- 여러 가지 요소에 대한 처리를 하나의 액션으로 처리할 수 있게 하는 기법

### 🔹 데이터 바인딩 (Data Binding)
- 화면에 보이는 데이터와 웹 브라우저의 메모리 데이터를 일치시키는 기법으로, 뷰모델을 변경하면 뷰가 변경된다.
