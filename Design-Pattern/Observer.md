## 4. 옵저버 패턴 (Observer Pattern)

> 객체의 상태가 변경되었을 때, 해당 객체를 관찰하는 옵저버들에게 상태 변화를 자동으로 알려주는 패턴


### 코드 예시

```java
// 옵저버
interface Subscriber {
    void update(String video);
}

// 구독자
class User implements Subscriber {

    private String name;

    public User(String name) {
        this.name = name;
    }

    @Override
    public void update(String video) {
        System.out.println(name + "에게 알림: " + video);
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

// 주체
class YoutubeChannel {

    // 옵저버 목록
    private List<Subscriber> subscribers = new ArrayList<>();

    // 옵저버 등록
    public void subscribe(Subscriber subscriber) {
        subscribers.add(subscriber);
    }

    // 새 영상 업로드
    public void uploadVideo(String video) {

        // 등록된 모든 옵저버에게 상태 변화 알림
        for (Subscriber subscriber : subscribers) {
            subscriber.update(video);
        }
    }
}
```

```java
public class Main {

    public static void main(String[] args) {

        YoutubeChannel channel = new YoutubeChannel();

        Subscriber user1 = new User("지혜");
        Subscriber user2 = new User("영균");

        // 옵저버 등록
        channel.subscribe(user1);
        channel.subscribe(user2);

        // 상태 변화
        channel.uploadVideo("새 영상이 업로드되었습니다.");
    }
}
```

### 실행 결과

```text
지혜에게 알림: 새 영상이 업로드되었습니다.
영균에게 알림: 새 영상이 업로드되었습니다.
```

> `YoutubeChannel`에 상태 변화가 발생하면 등록된 `Subscriber`의 `update()`를 호출하여 모든 옵저버에게 변화를 알림

### 활용

* 이벤트 기반 시스템에서 상태 변화를 여러 객체에 전달할 때 사용
* MVC 패턴에서 Model의 상태 변화를 View 등에 전달하는 데 활용될 수 있음

### 장단점

| 구분 | 내용 |
|---|---|
| **장점** | 주체와 옵저버 간의 결합도를 낮출 수 있음<br>새로운 옵저버를 쉽게 추가할 수 있어 확장 및 유지보수가 용이함<br>하나의 상태 변화를 여러 객체에 전달하기 용이함 |
| **단점** | 옵저버가 많아지면 알림 처리로 인해 성능에 영향을 줄 수 있음<br>여러 옵저버가 연쇄적으로 동작할 경우 전체 동작 흐름을 파악하기 어려울 수 있음 |

