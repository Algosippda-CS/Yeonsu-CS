# 전략 패턴
: 정책 패턴(policy pattern)이라고도 한다.   
: 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 
<b>`캡슐화한 알고리즘`</b>을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴이다.

ex. 우리가 어떤 것을 살 때, 네이버페이, 카카오페이 등 다양한 방법으로 결제하듯이, 결제 방식의 '전략'만 바꿔서 결제하는 것

<br/>

## ✍️ 자바의 전략 패턴
아래의 코드는 쇼핑 카트에 아이템을 담아 `LUNACard` 또는 `KAKAOCard`라는 두 개의 전략으로 결제하는 코드이다.


```java
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;

// 결제 전략 (인터페이스)
interface PaymentStrategy {
  public void pay(int amount);
}

// 카카오카드로 결제하는 전략
class KAKAOCardStrategy implements PaymentStrategy {
  private String name;
  private String cardNumber;
  private String cvv;
  private String dateOfExpiry;
  
  public KAKAOCardStrategy(String nm, String ccNum, String cvv, String expiryDate) {
    this.name = nm;
    this.cardNumber = ccNum;
    this.cvv = cvv;
    this.dateOfExpiry = expiryDate;
  }

  @Override
  public void pay(int amount) {
    System.out.println(amount + " paid using KAKAOCard.");
  }
}

// 루나카드로 결제하는 전략
class LUNACardStrategy implements PaymentStrategy {
  private String emailId;
  private String password;
  
  public LUNACardStrategy(String email, String pwd) {
    this.emailId = email;
    this.password = pwd;
  }

  @Override
  public void pay(int amount) {
    System.out.println(amount + " paid using LUNACard.");
  }
}

// 제품
class Item {
  private String name;
  private int price;
  public Item(String name, int cost) {
    this.name = name;
    this.price = cost;
  }

  public String getName() {
    return name;
  }
  
  public int getPrice() {
  return price;
  }
}

// 장바구니
class ShoppingCart {
  List<Item> items;
  
  public ShoppingCart() {
    this.items = new ArrayList<Item>();
  }
  
  public void addItem(Item item) {
    this.items.add(item);
  }
  
  public void removeItem(Item item) {
    this.items.remove(item);
  }

  public int calculateTotal() {
    int sum = 0;
    for (Item item : items) {
      sum += item.getPrice();
    }
    return sum;
  }

  public void pay(PaymentStrategy paymentMethod) {
    int amount = calculateTotal();
    paymentMethod.pay(amount);
  }
}

public class HelloWorld {
  public static void main(String[] args) {
    ShoppingCart cart = new ShoppingCart();
    
    Item A = new Item("iPhone", 150);
    Item B = new Item("Galaxy", 130);
    
    cart.addItem(A);
    cart.addItem(B);
    
    // pay by LUNACard
    cart.pay(new LUNACardStrategy("apple@example.com", "lalala"));
    
    // pay by KAKAOCard
    cart.pay(new KAKAOCardStrategy("Lee yeonsu", "123456789", "123", "09/06"));
    }
}
/*
280 paid using LUNACard.
280 paid using KAKAOCard.
*/

```
</br>


### 👉 passport의 전략 패턴
전략 패턴을 활용한 라이브러리로는 `passport`가 있다.   
`passport`는 `Node.js`에서 인증 모듈을 구현할 때 쓰는 미들웨어 라이브러리로, 여러 가지 '전략'을 기반으로 인증할 수 있게 한다.   
- LocalStrategy 전략, OAuth 전략 등을 지원
  
