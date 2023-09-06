# 싱글톤 패턴(Singleton Pattern)
: 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴

하나의 클래스를 기반으로 단 하나의 인스턴스를 만들어 이를 기반으로 로직을 만드는 데 쓰인다.
보통 데이터베이스 연결 모듈에 많이 사용한다.

클래스 1개 -> 인스턴스 1개 -> 모듈 A, B, C,... 등이 이 인스턴스를 공유하며 사용


### 장점
인스턴스 생성 비용 절감: 인스턴스를 생성할 때 드는 비용이 줄어든다.

### 단점
의존성이 높아진다.


## 자바에서의 싱글톤 패턴
자바로는 <b>중첩 클래스</b>를 이용해서 만드는 방법이 가장 대중적이다.
```java
class Singleton {
  private static class singleInstanceHolder {
    private statid final Singleton INSTANCE = new Singleton();
  }
  public static Singleton getInstance() {
    return singleInstanceHolder.INSTANCE;
  }
}

public class HelloWorld {
  public static void main(String[] args) {
    Singletone a = Singleton.getInstance();
    Singletone b = Singleton.getInstance();
    System.out.println(a.hashCode());
    System.out.println(b.hashCode());
    if (a == b) {
      System.out.println(true);
    }
  }
}
/*
705927765
705927765
true
*/
```

## 싱글톤 패턴의 단점
1. TDD(Test Driven Development)를 할 때 걸림돌이 된다.   

   TDD를 할 때 단위 테스트 수행: 테스트가 서로 독립적 & 어떤 순서로든 실행 가능해야 함.   
   싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이므로(<b>의존적</b>) 각 테스트마다 '독립적인' 인스턴스를 만들기 어렵다.

2. 모듈 간의 결합을 강하게 만들 수 있다.   
   sol) 의존성 주입(DI, Dependency Injection)을 통해 모듈 간의 결합을 조금 더 느슨하게 만들어 해결 가능   
   (A가 B에 의존성이 있다 = B가 변하면 A도 변해야 한다.)


 ### 👉 의존성 주입
 - 의존성 주입 전: 메인 모듈이 다른 하위 모듈에 <b>'직접'</b> 의존성을 준다.
 - 의존성 주입 후: 메인 모듈이 다른 하위 모듈에 <b>'간접'</b>적으로 의존성을 주입한다.
   - 중간에 의존성 주입자(dependency injector)가 대신 다른 하위 모듈들에 의존성을 주입하게 한다.
   - 이를 통해 메인 모듈(상위 모듈)은 하위 모듈에 대한 의존성이 떨어지게 된다.(=디커플링이 된다.)


#### 🔹 의존성 주입의 장점
의존성 주입을 하면 모듈들을 쉽게 교체할 수 있는 구조가 된다. 따라서
1. 테스팅하기 쉽다.
2. 마이그레이션하기 수월하다.
3. 애플리케이션 의존성 방향이 일관된다: 구현할 때 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어주기 때문
4. 애플리케이션을 쉽게 추론할 수 있다.
5. 모듈 간의 관계들이 조금 더 명확해진다.
#### 🔹 의존성 주입의 단점
모듈들이 더 분리됨 -> 클래스 수 증가 -> 복잡성 증가, 약간의 런타임 페널티가 생기기도 한다.

#### ⭐️ 의존성 주입 원칙
>상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야 한다.   
>또한, 둘 다 추상화에 의존해야 하며, 이때 추상화는 세부 사항에 의존하지 말아야 한다.
