Chào mừng bạn trở lại!

Hy vọng bạn đã có thời gian thử bài tập vừa rồi. Hãy cùng xem xét giải pháp và hiểu rõ hơn về cách sử dụng **@Primary** và **@Qualifier** trong Spring Framework khi có nhiều bean cùng triển khai một interface.

### Vấn Đề: Nhiều Bean Cùng Triển Khai Interface

Khi bạn đánh dấu cả **MarioGame** và **PacManGame** với **@Component**, Spring Framework sẽ gặp vấn đề vì không thể xác định nên sử dụng bean nào để **autowire** vào lớp **GameRunner**. Lỗi xuất hiện là **NoUniqueBeanDefinitionException**, vì Spring phát hiện có nhiều hơn một bean triển khai interface **GamingConsole** mà không thể tự quyết định được.

### Cách Giải Quyết 1: Sử Dụng @Primary

Một cách để giúp Spring chọn đúng bean là sử dụng chú thích **@Primary**. Khi bạn đánh dấu một bean với **@Primary**, bạn đang nói với Spring rằng nếu có nhiều bean cùng triển khai interface, thì bean được đánh dấu **@Primary** sẽ được ưu tiên.

#### Ví dụ:

1. **Đánh dấu MarioGame với @Primary**:

```java
import org.springframework.stereotype.Component;
import org.springframework.context.annotation.Primary;

@Component
@Primary
public class MarioGame implements GamingConsole {

    @Override
    public void up() {
        System.out.println("Mario jumps!");
    }

    @Override
    public void down() {
        System.out.println("Mario goes into a hole!");
    }

    @Override
    public void left() {
        System.out.println("Mario goes left!");
    }

    @Override
    public void right() {
        System.out.println("Mario accelerates!");
    }
}
```

2. **Chạy ứng dụng**:
    - Khi bạn chạy ứng dụng, Spring sẽ tự động chọn **MarioGame** làm bean chính vì nó được đánh dấu với **@Primary**, dù có nhiều bean khác cũng triển khai **GamingConsole**.

Kết quả:

```
Running game...
Mario jumps!
Mario goes into a hole!
Mario goes left!
Mario accelerates!
```

### Cách Giải Quyết 2: Sử Dụng @Qualifier

Trong trường hợp bạn muốn kiểm soát rõ ràng hơn và không sử dụng **@Primary**, bạn có thể dùng **@Qualifier**. **@Qualifier** giúp bạn chỉ định rõ bean nào sẽ được tiêm vào khi có nhiều lựa chọn.

#### Ví dụ:

1. **Đánh dấu SuperContraGame với @Component** và thêm **@Qualifier**:

```java
import org.springframework.stereotype.Component;

@Component
@Qualifier("superContraGameQualifier")
public class SuperContraGame implements GamingConsole {

    @Override
    public void up() {
        System.out.println("Super Contra jumps!");
    }

    @Override
    public void down() {
        System.out.println("Super Contra goes into a hole!");
    }

    @Override
    public void left() {
        System.out.println("Super Contra goes left!");
    }

    @Override
    public void right() {
        System.out.println("Super Contra accelerates!");
    }
}
```

2. **Sử dụng @Qualifier trong GameRunner** để chọn bean cụ thể:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class GameRunner {

    private GamingConsole game;

    @Autowired
    public GameRunner(@Qualifier("superContraGameQualifier") GamingConsole game) {
        this.game = game;
    }

    public void run() {
        System.out.println("Running game...");
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

3. **Chạy ứng dụng**:
    - Spring sẽ tiêm **SuperContraGame** vào **GameRunner** vì bạn đã chỉ định rõ ràng bằng **@Qualifier**.

Kết quả:

```
Running game...
Super Contra jumps!
Super Contra goes into a hole!
Super Contra goes left!
Super Contra accelerates!
```

### Tổng Kết

- **@Primary**: Khi có nhiều bean cùng triển khai một interface, Spring sẽ ưu tiên bean được đánh dấu **@Primary**. Điều này rất hữu ích khi bạn chỉ muốn ưu tiên một bean trong số nhiều lựa chọn.
  
- **@Qualifier**: Cho phép bạn chỉ định chính xác bean nào sẽ được tiêm khi có nhiều bean cùng triển khai một interface. **@Qualifier** được sử dụng khi bạn cần điều khiển cụ thể hơn về bean nào sẽ được tiêm vào các đối tượng.

### Bài Tập Đề Xuất

Bạn có thể thử thêm **@Qualifier** và **@Primary** cho nhiều bean khác nhau và xem cách Spring Framework xử lý các tình huống đó. Hãy thử nghiệm với các tình huống khác nhau để hiểu rõ hơn về cách Spring quản lý việc **autowire** các bean khi có nhiều lựa chọn.

Hẹn gặp lại bạn ở bước tiếp theo, nơi chúng ta sẽ khám phá thêm các khía cạnh thú vị khác của Spring Framework!
