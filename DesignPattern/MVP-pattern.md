# 📌 MVP 패턴
: MVC 패턴으로부터 파생되었으며 MVC에서 C에 해당하는 컨트롤러가 프레젠터(presenter)로 교체된 패턴이다.

<br/>

![IMG_898373081604-1](https://github.com/Algosippda-CS/Yeonsu-CS/assets/82032452/b78e0154-72e1-4fa2-8e3b-155a43e8f90c)

- 뷰와 프레젠터는 일대일 관계이기 때문에 MVC 패턴보다 더 강한 결합을 지닌 디자인 패턴이라고 볼 수 있다.
- 뷰와 프레젠터는 모델의 인스턴스를 가지고 있어 둘을 연결하는 접착제 역할을 한다.

## 장점
View와 Model의 의존성이 없다. (Presenter를 통해서만 데이터를 전달 받기 때문에)   
MVP 패턴은 MVC 패턴의 단점이었던 View와 Model의 의존성을 해결하였다.

## 단점
애플리케이션이 복잡해질수록 View와 Presenter 사이의 의존성이 강해진다.
