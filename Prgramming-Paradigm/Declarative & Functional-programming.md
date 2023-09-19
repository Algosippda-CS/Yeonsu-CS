# 📌 선언형 프로그래밍 (Declarative programming)
: '무엇을' 풀어내는가에 집중하는 패러다임
: "프로그램은 함수로 이루어진 것이다." 라는 명제가 담겨 있는 패러다임이기도 하다.


## 🔧  함수형 프로그래밍 (Functional programming)
: 선언형 패러다임의 일종   
: 작은 `순수 함수`들을 블록처럼 쌓아 로직을 구현하고, `고차 함수`를 통해 재사용성을 높인 프로그래밍 패러다임   
- ex) 자바스크립트는 함수형 프로그래밍 방식이 선호된다.

  ### 순수 함수
  : 출력이 입력에만 의존하는 것

  ### 고차 함수
  : 함수가 함수를 값처럼 매개변수로 받아 로직을 생성할 수 있는 것
  #### 일급 객체
  고차 함수를 쓰기 위해서는 해당 언어가 일급 객체라는 특징을 가져야 하며, 그 특징은 다음과 같다.
  - 변수나 메서드에 함수를 할당할 수 있다.
  - 함수 안에 함수를 매개변수로 담을 수 있다.
  - 함수가 함수를 반환할 수 있다.
 