# 📌 옵저버 패턴 (Observer pattern)
: 주체가 어떤 객체(subject)의 상태 변화를 관찰하다가 상태 변화가 있을 때마다   
메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴

- 주체: 객체의 상태 변화를 보고 있는 관찰자
- 옵저버(들): 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 `추가 변화 사항`이 생기는 객체들



즉, 주체는 객체의 상태가 변하나 안 변하나 관찰하고, 변하면 옵저버들에게 알려준다.
객체가 변하면 옵저버들도 같이 변한다.



- 객체와 주체가 분리되어 있는 경우도 있지만
- 객체와 주체가 합쳐진 경우도 있다: 상태가 변경되는 객체를 기반으로 구축.
- ex) 트위터의 옵저버 패턴: 내가 어떤 사람인 주체를 `팔로우`하면 주체가 포스팅을 올렸을 때 `팔로워`에게 알림이 온다.

<br/>

## 옵저버 패턴의 사용
- 주로 `이벤트 기반 시스템`에 사용한다.
- `MVC(Model-View-Controller)` 패턴에도 사용된다.

<br/>

## ✍️ 자바에서의 옵저버 패턴

`topic`을 기반으로 옵저버 패턴을 구현했다.
여기서 `topic`은 주체이자 객체가 된다.


```java
import java.util.ArrayList;
import java.util.List;

interface Subject {
  public void register(Observer obj);
  public void unregister(Observer obj);
  public void notifyObservers();
  public Object getUpdate(Observer obj);
}

interface Observer) {
  public void update();
}

// Subject interface 구현
class Topic implements Subject {
private List<Observer> observers;
private String message;

  public Topic() {
    this.observers = new ArrayList<>();
    this.message = "";
  }

  @Override
  public void unregister(Observer obj) {
    observers.remove(obj);
  }
  
  @Override
  public void notifyObservers() {
    this.observers.forEach(Observer::update);
  }
  
  @Override
  public Object getUpdate(Observer obj) {
    return this.message;
  }
  
  public void postMessage(String msg) {
    System.out.println("Message sended to Topic: " + msg);
    this.message = msg;
    notifyObservers();
  }
}

class TopicSubscriber implements Observer {
  private String name;
  private Subject topic;
  
  public TopicSubscriber(String name, Subject topic) {
    this.name = name;
    this.topic = topic;
  }

  @Override
  public void update() {
    String msg = (String) topic.getUpdate(this);
    System.out.println(name + ":: got message >> " + msg);
  }
}

public class HelloWorld {
  public static void main(String[] args) {
    Topic topic = new Topic();
    // 옵저버 선언할 때 해당 이름과 어떤 토픽의 옵저버가 될 것인지 결정
    Observer a = new TopicSubscriber("a", topic);
    Observer b = new TopicSubscriber("b", topic);
    Observer c = new TopicSubscriber("c", topic);
    topic.register(a);
    topic.register(b);
    topic.register(c);
  
    topic.postMessage("amumu is op champion!!");
  }
}
/*
Message sended to Topic: amumu is op champion!!
a:: got message >> amumu is op champion!!
b:: got message >> amumu is op champion!!
c:: got message >> amumu is op champion!!
*/
```


## ✍️ 자바스크립트에서의 옵저버 패턴
자바스크립트에서의 옵저버 패턴은 `프록시 객체`를 통해 구현할 수도 있다.

### 👉 프록시(proxy) 객체
: 어떠한 대상의 기본적인 동작(속성 접근, 할당, 순회, 열거, 함수 호출 등)의 작업을 가로챌 수 있는 객체   
특정 속성에 접근할 때 그 부분을 가로채서 어떠한 로직을 강제할 수 있다.   
자바스크립트에서 프록시 객체는 두 개의 매개변수를 갖는다.
- target: 프록시할 대상
- handler: target 동작을 가로채고 어떠한 동작을 할 것인지가 설정되어 있는 함수

#### 프록시 객체를 이용한 옵저버 패턴을 이용하여 구현한 예시
프론트엔드에서 많이 쓰는 프레임워크 Vue.js 3.0에서 `ref`나 `reactive`로 정의하면 
해당 값이 변경되었을 때 자동으로 `DOM`에 있는 값이 변경되는데, 이는 프록시 객체를 이용한 옵저버 패턴을 이용하여 구현한 것이다.
