### Khám Phá Các Loại Dependency Injection Trong Spring

Trong bước này, chúng ta sẽ khám phá ba loại **Dependency Injection (DI)** có sẵn trong **Spring Framework**:

1. **Constructor-based Injection** (Tiêm qua constructor)
2. **Setter-based Injection** (Tiêm qua setter)
3. **Field-based Injection** (Tiêm trực tiếp vào trường)

Chúng ta đã thấy ví dụ về **Constructor-based Injection** khi sử dụng constructor để tiêm phụ thuộc. Trong các ví dụ sau, chúng ta sẽ thấy cách sử dụng **setter** và **field** để thực hiện DI. Hãy cùng bắt đầu.

### Ba Loại Dependency Injection Trong Spring

#### 1. Constructor-based Injection

**Constructor-based Injection** là khi chúng ta sử dụng constructor để tiêm phụ thuộc vào lớp. Spring sẽ tiêm các phụ thuộc qua constructor khi khởi tạo bean.

Ví dụ:

```java
@Component
public class GameRunner {
    private final GamingConsole game;

    @Autowired
    public GameRunner(GamingConsole game) {
        this.game = game;
    }

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Ở đây, **Spring** sử dụng constructor để tiêm đối tượng **GamingConsole** vào **GameRunner**. Constructor-based Injection là lựa chọn tốt nhất khi các phụ thuộc cần thiết cho việc khởi tạo đối tượng.

#### 2. Setter-based Injection

**Setter-based Injection** sử dụng setter method để tiêm phụ thuộc. Đây là lựa chọn tốt khi phụ thuộc có thể được thay đổi sau khi đối tượng đã được khởi tạo.

Ví dụ:

```java
@Component
public class GameRunner {
    private GamingConsole game;

    @Autowired
    public void setGamingConsole(GamingConsole game) {
        this.game = game;
    }

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Trong ví dụ này, **Spring** sử dụng setter method để tiêm đối tượng **GamingConsole** vào **GameRunner**. Điều này cho phép chúng ta thay đổi phụ thuộc sau khi đối tượng đã được tạo.

#### 3. Field-based Injection

**Field-based Injection** sử dụng trực tiếp các biến thành viên (fields) của lớp mà không cần thông qua constructor hay setter. Đây là cách tiêm nhanh chóng, nhưng không được khuyến khích nhiều vì nó không dễ kiểm thử và vi phạm nguyên tắc của **dependency injection** tốt.

Ví dụ:

```java
@Component
public class GameRunner {
    @Autowired
    private GamingConsole game;

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Ở đây, **Spring** sử dụng **reflection** để tiêm trực tiếp đối tượng **GamingConsole** vào biến **game**. Mặc dù cách này dễ dàng nhưng hạn chế là khó kiểm thử vì không dễ mô phỏng các phụ thuộc.

### Các Bước Thực Hiện Trong Ví Dụ

#### Bước 1: Tái cấu trúc dự án

Đầu tiên, chúng ta sẽ tái cấu trúc mã nguồn để tạo một môi trường thuận tiện cho việc thử nghiệm các loại DI.

1. **Di chuyển GamingAppLauncherApplication vào package `game`**:
    - Di chuyển **GamingAppLauncherApplication** vào **com.in28minutes.learnspringframework.game**.

2. **Tạo một ứng dụng khởi chạy mới**:
    - Sao chép **GamingAppLauncherApplication** và tạo một lớp mới tên là **DependencyInjectionLauncherApplication** để thử nghiệm các loại DI.

3. **Tạo package mới để tổ chức ví dụ**:
    - Tạo package mới **com.in28minutes.learnspringframework.examples.a1** và di chuyển **DependencyInjectionLauncherApplication** vào đó.

4. **Cấu hình ComponentScan**:
    - Cập nhật **@ComponentScan** để chỉ định quét các component trong package mới.

#### Bước 2: Khởi động Spring Context

Tạo một phương thức để liệt kê tất cả các bean trong **Spring Context**:

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import java.util.Arrays;

public class DependencyInjectionLauncherApplication {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(DependencyInjectionLauncherApplication.class)) {
            Arrays.stream(context.getBeanDefinitionNames()).forEach(System.out::println);
        }
    }
}
```

Khi chạy ứng dụng, bạn sẽ thấy danh sách các bean được Spring tạo ra.

#### Bước 3: Thử Nghiệm Các Loại Dependency Injection

Bây giờ bạn đã sẵn sàng để thử nghiệm từng loại **dependency injection**:

1. **Constructor-based Injection**: Tiêm phụ thuộc thông qua constructor.
2. **Setter-based Injection**: Tiêm phụ thuộc thông qua setter method.
3. **Field-based Injection**: Tiêm trực tiếp vào biến thành viên.

Mỗi loại đều có ưu và nhược điểm riêng, và bạn có thể tùy chọn loại tiêm phù hợp nhất với yêu cầu của ứng dụng.

### Tổng Kết

Chúng ta đã tìm hiểu về ba loại **dependency injection** trong Spring: **constructor-based**, **setter-based**, và **field-based injection**. Cả ba đều có vai trò quan trọng trong việc tiêm phụ thuộc vào các lớp khác, nhưng tùy thuộc vào ngữ cảnh, bạn nên chọn loại DI phù hợp để đảm bảo tính dễ bảo trì, dễ kiểm thử, và hiệu quả cho ứng dụng của mình.

Trong bước tiếp theo, chúng ta sẽ thử nghiệm với **field injection** và tiếp tục khám phá các khía cạnh khác của **dependency injection** trong Spring Framework.
