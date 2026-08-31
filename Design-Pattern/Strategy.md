## 3. 전략 패턴 (Strategy Pattern) (=정책 패턴 Policy Pattern) 

> 객체의 동작을 직접 수정하지 않고, 필요한 동작(전략)을 선택하여 교체할 수 있도록 하는 패턴


### 코드 예시

```java
// 결제 전략
interface PaymentStrategy {
    void pay();
}

// 카드 결제 전략
class CardPayment implements PaymentStrategy {

    @Override
    public void pay() {
        System.out.println("카드로 결제합니다.");
    }
}

// 카카오페이 결제 전략
class KakaoPayment implements PaymentStrategy {

    @Override
    public void pay() {
        System.out.println("카카오페이로 결제합니다.");
    }
}

// 네이버페이 결제 전략
class NaverPayment implements PaymentStrategy {

    @Override
    public void pay() {
        System.out.println("네이버페이로 결제합니다.");
    }
}

// 결제 전략을 사용하는 클래스
class Order {

    private PaymentStrategy paymentStrategy;

    public Order(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void payment() {
        paymentStrategy.pay();
    }
}
```

```java
public class Main {

    public static void main(String[] args) {

        // 카드 결제 전략 선택
        Order order1 = new Order(new CardPayment());
        order1.payment(); // 카드로 결제합니다.

        // 카카오페이 결제 전략 선택
        Order order2 = new Order(new KakaoPayment());
        order2.payment(); // 카카오페이로 결제합니다.

        // 네이버페이 결제 전략 선택
        Order order3 = new Order(new NaverPayment());
        order3.payment(); // 네이버페이로 결제합니다.
    }
}
```
> `Order` 클래스 자체를 수정하지 않고, 전달하는 `PaymentStrategy` 객체만 변경하여 원하는 결제 방식을 선택할 수 있음


### 장단점

| 구분 | 내용 |
|---|---|
| **장점** | 객체의 동작을 쉽게 변경하거나 확장할 수 있어 유지보수성이 높아짐<br> 여러 동작을 각각의 전략으로 분리하여 복잡한 조건문을 줄일 수 있음  |
| **단점** | 전략이 늘어날수록 클래스 수가 많아질 수 있음 <br> 간단한 기능에서는 오히려 코드 구조가 복잡해질 수 있음 |
