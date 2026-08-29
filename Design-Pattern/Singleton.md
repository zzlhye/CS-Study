# 1. 싱글톤 패턴 (Singleton Pattern)
> 하나의 클래스에서 인스턴스를 하나만 생성하고 이를 공유하여 사용하는 패턴

## 코드 예시

```java
public class Singleton {

    // 1. 클래스 내부에서 하나의 인스턴스 생성
    private static Singleton instance = new Singleton();

    // 2. 외부에서 추가적인 인스턴스 생성을 방지
    private Singleton() {
    }

    // 3. 생성된 인스턴스를 반환
    public static Singleton getInstance() {
        return instance;
    }
}
```

```java
public class Main {

    public static void main(String[] args) {

        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2); // true
    }
}
```

## 장단점

| 구분 | 내용 |
|---|---|
| **장점** | 인스턴스를 하나만 생성하여 공유하기 때문에 불필요한 객체 생성을 줄일 수 있음 |
| **단점** | 직접 참조로 인해 의존성이 높아질 수 있음<br>하나의 인스턴스를 공유하기 때문에 테스트 간 영향을 주어 독립적인 테스트가 어려울 수 있음 |

※ 의존성 주입(DI)을 통해 객체 간 결합도를 낮춰 보완할 수 있음

---

## 관련 개념 - Spring의 IoC와 DI

### 의존성 주입 (DI, Dependency Injection)

> 필요한 객체를 직접 생성하지 않고 외부에서 주입받아 사용하는 방식

#### DI의 장단점

| 구분 | 내용 |
|---|---|
| **장점** | 객체 간 결합도를 낮출 수 있음 <br> 의존 객체를 쉽게 교체할 수 있어 유지보수 및 테스트가 용이함 <br> 객체 간 의존 관계가 명확해져 애플리케이션의 구조를 파악하기 쉬움 | 
| **단점** | 객체 간 관계가 많아지면 의존성 구조를 파악하기 어려울 수 있음 <br> 작은 프로그램에서는 구조가 오히려 복잡해질 수 있음 | 

### Spring에서의 DI

* @Service, @Repository, @Component 등의 어노테이션이 붙은 클래스를 Spring이 찾아 Spring Bean으로 등록
* Spring이 객체를 생성·관리하고 필요한 곳에 주입하기 때문에 개발자가 직접 `new`로 생성하지 않고 사용할 수 있음

```text
@Service 등의 어노테이션
        ↓
Spring이 클래스 탐색
        ↓
IoC Container가 객체 생성
        ↓
Spring Bean으로 등록 및 관리
        ↓
필요한 곳에 DI로 주입
```

### Spring Bean

> 개발자가 직접 `new`로 생성하는 대신 Spring이 생성하고 관리하는 자바 객체

### IoC Container

> Spring Bean을 생성하고 보관하며 관리하는 컨테이너
>
> <sub>※ 제어의 역전(IoC)?  
기존에는 개발자가 직접 객체를 생성하고 관리했다면, Spring에서는 객체의 생성과 관리를 IoC Container가 담당해서</sub>


