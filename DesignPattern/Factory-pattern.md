# 팩토리 패턴(Factory pattern)
: 객체 생성 부분을 떼어내 추상화한 패턴   
: 상속 관계에 있는 두 클래스에서 상위 클래스는 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴
- 상위 클래스 -> 중요한 뼈대 결정
- 하위 클래스 -> 객체 생성에 관한 구체적인 내용 결정

## 팩토리 패턴의 특징
- 느슨한 결합: 상위 클래스와 하위 클래스가 분리되기 때문
- 더 많은 유연성: 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없다.
- 유지 보수성 증가: 객체 생성 로직이 따로 떼어져 있기 때문에 코드를 리팩토링하더라도 한 곳만 고칠 수 있다.

## 자바의 팩토리 패턴
```java
abstract class Coffee {  // 추상 클래스(상위 클래스): 중요한 뼈대 설정 
  public abstract int getPrice();

  @Override
  public String toString() {
    return "Hi this coffee is " + this.getPrice();
  }
}
class CoffeeFactory {
  public static Coffe getCoffee(String type, int price) {
    if ("Latte".equalsIgnoreCase(type)) return new Latte(price);
    else if ("Americano".equalsIgnoreCase(type)) return new Americano(price);
    else {
      return new DefaultCoffee();
    }
  }
}
class DefaultCoffee extends Coffee {  // DefaultCoffe에 대한 구체적인 내용 결정
  private int price;

  public DefaultCoffee() {
    this.price = -1;
  }

  @Override
  publid int getPrice() {
    return this.price;
  }
}
class Latte extends Coffee {  // Latte에 대한 구체적인 내용 결정
  private int price;
  
  public Latte(int price) {
  this.price = price;
  }
  @Override
  public int getPrice() {
    return this.price;
  }
}
class Americano extends Coffee {  // Americano에 대한 구체적인 내용 결정
  private int price;
  
  public Latte(int price) {
  this.price = price;
  }
  @Override
  public int getPrice() {
    return this.price;
  }
}
public class HelloWorld {
  public static void main(String[] args) {
    Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
    Coffee ame = CoffeFactory.getCoffee("Americano", 3000);
    System.out.println("Factory latte ::" + latte);
    System.out.println("Factory ame ::" + ame);
  }
}
/*
Factory latte :: Hi this coffee is 4000
Factory ame :: Hi this coffee is 3000
*/
```
