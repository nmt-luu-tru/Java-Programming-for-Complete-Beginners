## Giải Quyết Bài Tập: Tạo Ứng Dụng Game Sử Dụng Spring

### Bước 1: Tạo Lớp Cấu Hình Spring

Bắt đầu với việc tạo lớp cấu hình cho ứng dụng game của bạn. Hãy tạo một lớp mới có tên `GamingConfiguration`. Trong lớp này, bạn sẽ định nghĩa các **bean** cần thiết cho ứng dụng game của mình.

```java
@Configuration
public class GamingConfiguration {

    @Bean
    public GamingConsole game() {
        return new PacmanGame();
    }

    @Bean
    public GameRunner gameRunner(GamingConsole game) {
        return new GameRunner(game);
    }
}
```

Ở đây:
- `@Configuration` đánh dấu lớp là lớp cấu hình cho Spring.
- `@Bean` đánh dấu phương thức trả về một **bean** Spring.

### Bước 2: Tạo Context Spring và Lấy Bean

Trong lớp ứng dụng chính (ví dụ: `App03GamingSpringBeans`), bạn sẽ tạo một context Spring và lấy các **bean** đã định nghĩa:

```java
public class App03GamingSpringBeans {
    public static void main(String[] args) {
        try (AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(GamingConfiguration.class)) {
            GameRunner gameRunner = context.getBean(GameRunner.class);
            gameRunner.run();
        }
    }
}
```

Ở đây:
- Sử dụng `AnnotationConfigApplicationContext` để tạo context từ lớp cấu hình.
- Lấy **bean** `GameRunner` và gọi phương thức `run()` trên đó.

### Kết Quả

Khi bạn chạy ứng dụng, bạn sẽ thấy đầu ra như sau:

```
Running game...
Controls: Up, Down, Left, Right
```

### Tổng Kết

Trong bước này, bạn đã:
- Tạo một lớp cấu hình Spring để định nghĩa các **bean**.
- Sử dụng context Spring để lấy và chạy các **bean** trong ứng dụng của mình.

Bây giờ, bạn đã tạo thành công ứng dụng game sử dụng Spring Framework với cấu hình và **bean** thích hợp!
