# 📌 노출모듈 패턴 (Revealing module pattern)
: 즉시 실행 함수를 통해 private, public 같은 <b>접근 제어자를 만드는 패턴</b>   

자바스크림트는 private나 public 같은 접근 제어자가 존재하지 않고 전역 범위에서 스크립트가 실행된다.   
그렇기 때문에 노출모듈 패턴을 통해 private과 public 접근 제어자를 구현하기도 한다.



## 장점
- 개발자에게 깔끔한 접근 방법 제공
- private 데이터 제공
- 전역 변수를 덜 더럽힘
- 클로저를 통해 함수와 변수를 지역화
- 스크립트 문법이 더 일관성 있음
- 명시적으로 public 메소드와 변수를 제공해 명시성을 높임



## 단점
- private 메소드에 접근할 방법이 없음 (그래서 테스트 불가란 얘기를 하는데 private은 테스트할지 안 할지 고민해 봐야 함)
- private 메소드에 대해 함수를 확장하는 데 어려움이 있음
- private 메소드를 참조하는 public 메소드를 수정하기 어려움



## 예제

```javascript
var myModule = (function(window, undefined) {
  function myMethod() {
    console.log('myMethod');
  }

  function myOtherMethod() {
    console.log('myOtherMethod');
  }

  return {
    someMethod: myMethod,
    someOtherMethod: myOtherMethod
  };
})(window);

myModule.myMethod(); // Uncaught TypeError: myModule.myMethod is not a function
myModule.myOtherMethod(); // Uncaught TypeError: myModule.myOtherMethod is not a function
myModule.someMethod(); // console.log('myMethod');
myModule.someOtherMethod(); // console.log('myOtherMethod');
```
