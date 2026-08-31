## 2. 팩토리 패턴 (Factory Pattern)

> 객체 생성의 틀은 상위 클래스에서 정의하고, 구체적으로 어떤 객체를 생성할지는 하위 클래스에서 결정하는 패턴

### 코드 예시

```java
// 공통 객체
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("멍멍");
    }
}

class Cat implements Animal {
    public void sound() {
        System.out.println("야옹");
    }
}

// 상위 클래스 - 객체 생성의 틀 정의
abstract class AnimalFactory {
    abstract Animal createAnimal();
}

// 하위 클래스 - 생성할 객체를 구체적으로 결정
class DogFactory extends AnimalFactory {

    @Override
    Animal createAnimal() {
        return new Dog();
    }
}

class CatFactory extends AnimalFactory {

    @Override
    Animal createAnimal() {
        return new Cat();
    }
}

```

```java
public class Main {

    public static void main(String[] args) {

        AnimalFactory factory = new DogFactory();
        Animal animal = factory.createAnimal();

        animal.sound(); // 멍멍
    }
}

```

### 장단점

| 구분 | 내용 |
|---|---|
| **장점** | 객체 생성 방식의 변경이나 확장 시 기존 코드의 수정을 줄일 수 있어 유지보수성이 높아짐 <br> 객체 생성과 사용을 분리하여 객체 간 결합도를 낮출 수 있음 |
| **단점** | 객체마다 Factory 클래스가 추가될 수 있어 클래스 수가 많아지고 구조가 복잡해질 수 있음 |
