### Cách Spring Tự Động Quản Lý Và Tạo Đối Tượng (Beans)

Trong bước này, chúng ta sẽ trả lời câu hỏi về cách **Spring Framework** quản lý các đối tượng (beans) và tự động thực hiện **auto-wiring** mà không cần chúng ta phải tự tay tạo các đối tượng. Thay vì viết mã thủ công để tạo ra các đối tượng, Spring sẽ làm điều này cho chúng ta. Hãy cùng xem lại các bước và những thay đổi cần thực hiện để đạt được điều này.

### 1. Tái Cấu Trúc Dự Án

Trước tiên, chúng ta cần tái cấu trúc lại dự án để dễ quản lý và tổ chức mã nguồn hơn.

1. **Đổi tên dự án**:
    - Đổi tên dự án hiện tại thành **Learn Spring Framework 01** bằng cách nhấp chuột phải vào dự án và chọn **Refactor → Rename**, sau đó nhập tên mới **Learn Spring Framework 01**.

2. **Tạo bản sao của dự án**:
    - Sao chép toàn bộ dự án **Learn Spring Framework 01** (Ctrl + C), sau đó dán (Ctrl + V) thành **Learn Spring Framework 02**.

3. **Đóng dự án cũ**:
    - Nhấp chuột phải vào **Learn Spring Framework 01** và chọn **Close Project**.

### 2. Xóa Các Tệp Không Cần Thiết

Sau khi tái cấu trúc dự án, xóa các tệp không còn cần thiết để tập trung vào việc tích hợp Spring Framework với ứng dụng game.

1. **Xóa các tệp HelloWorld**:
    - Nhấp chuột phải vào các tệp **App02HelloWorldSpring** và **HelloWorldConfiguration** và chọn **Delete**.

2. **Xóa tệp App01GamingBasicJava**:
    - Nhấp chuột phải vào tệp **App01GamingBasicJava** và chọn **Delete**.

### 3. Hợp Nhất Tệp Cấu Hình Và Mã Nguồn

Thay vì giữ một tệp cấu hình Spring riêng biệt, hợp nhất mã cấu hình với mã nguồn chính của ứng dụng.

1. **Sao chép mã từ tệp GamingConfiguration vào App03GamingSpringBeans**.
2. **Xóa lớp GamingConfiguration** sau khi mã của nó đã được chuyển vào **App03GamingSpringBeans**.
3. **Xóa từ khóa `public`** của lớp **GamingConfiguration**.

Sau khi thay đổi, mã nguồn của **App03GamingSpringBeans** sẽ trông như sau:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

@Configuration
public class App03GamingSpringBeans {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(App03GamingSpringBeans.class)) {
            GameRunner gameRunner = context.getBean(GameRunner.class);
            gameRunner.run();
        }
    }

    @Bean
    public GamingConsole game() {
        return new PacManGame();  // Bạn có thể chọn PacMan, Mario, hoặc Super Contra
    }

    @Bean
    public GameRunner gameRunner(GamingConsole game) {
        return new GameRunner(game);
    }
}
```

### 4. Sử Dụng Auto Wiring

Spring Framework cho phép chúng ta tự động tạo và quản lý các đối tượng bằng cách sử dụng **@Component** và **@Autowired**.

1. **Thêm @Component vào các lớp trò chơi**:
    - Thêm chú thích **@Component** vào các lớp như **PacManGame**, **MarioGame**, **SuperContraGame** để Spring tự động tạo và quản lý các đối tượng:

```java
import org.springframework.stereotype.Component;

@Component
public class PacManGame implements GamingConsole {

    @Override
    public void up() {
        System.out.println("Pac-Man moves up!");
    }

    @Override
    public void down() {
        System.out.println("Pac-Man moves down!");
    }

    @Override
    public void left() {
        System.out.println("Pac-Man moves left!");
    }

    @Override
    public void right() {
        System.out.println("Pac-Man moves right!");
    }
}
```

2. **Sử dụng @Autowired trong GameRunner**:
    - Sử dụng **@Autowired** để Spring tự động "tiêm" đối tượng **GamingConsole** vào **GameRunner**:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class GameRunner {

    private GamingConsole game;

    @Autowired
    public GameRunner(GamingConsole game) {
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

3. **Kích hoạt Component Scanning**:
    - Thêm **@ComponentScan** trong **App03GamingSpringBeans** để Spring tự động phát hiện và tạo các bean:

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

@Configuration
@ComponentScan("com.in28minutes.learnspringframework")
public class App03GamingSpringBeans {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(App03GamingSpringBeans.class)) {
            GameRunner gameRunner = context.getBean(GameRunner.class);
            gameRunner.run();
        }
    }
}
```

### 5. Chạy Ứng Dụng

Chạy ứng dụng **App03GamingSpringBeans**. Spring sẽ tự động phát hiện và quản lý các bean như **PacManGame** và **GameRunner**:

```
Running game...
Pac-Man moves up!
Pac-Man moves down!
Pac-Man moves left!
Pac-Man moves right!
```

### Kết Luận

Chúng ta đã khám phá cách Spring Framework tự động tạo và quản lý các đối tượng thông qua **@Component** và **@Autowired**. Bằng cách sử dụng **Component Scanning**, Spring có thể tự động phát hiện các lớp và tạo các bean mà không cần viết mã thủ công.
