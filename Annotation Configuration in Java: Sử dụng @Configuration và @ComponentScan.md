### **Annotation Configuration in Java: Sử dụng @Configuration và @ComponentScan**

Trong video này, chúng ta sẽ tìm hiểu cách cấu hình Spring sử dụng **annotation** thay vì file cấu hình XML. Cụ thể, chúng ta sẽ sử dụng các annotation **@Configuration**, **@ComponentScan**, và **@Bean** để thay thế cho cấu hình trong `beans.xml`.

### **Bước 1: Xóa bỏ `beans.xml`**

Trước tiên, vì chúng ta sẽ sử dụng Java Configuration thay cho cấu hình XML, hãy xóa file `beans.xml` khỏi dự án của bạn. Điều này giúp chúng ta tập trung vào cách cấu hình hoàn toàn bằng annotation trong Spring.

### **Bước 2: Tạo lớp cấu hình sử dụng @Configuration**

Trong Spring, để khai báo một lớp cấu hình, bạn cần tạo một lớp mới và sử dụng annotation **@Configuration**. Lớp này sẽ chứa tất cả các cấu hình bean cần thiết cho Spring container.

#### Ví dụ tạo lớp `AppConfig`:

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
    // Đây là lớp cấu hình cho Spring
}
```

Ở đây, **@ComponentScan** với thuộc tính **basePackages** chỉ định gói mà Spring sẽ quét để tìm các thành phần **@Component**, **@Service**, **@Repository**, hoặc **@Controller**.

### **Bước 3: Cập nhật Main Class**

Trong phương thức **main**, chúng ta cần thay đổi cách tạo Spring Application Context để sử dụng cấu hình từ lớp `AppConfig`.

#### Cập nhật `Main.java`:

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Lấy các bean từ context và sử dụng
        Game game = context.getBean(Game.class);
        game.reset();
    }
}
```

Ở đây, thay vì sử dụng `ClassPathXmlApplicationContext` (khi chúng ta sử dụng `beans.xml`), chúng ta chuyển sang sử dụng **AnnotationConfigApplicationContext** để nạp cấu hình từ lớp `AppConfig`.

### **Bước 4: Tạo @Bean Methods**

Trong cấu hình bằng Java, thay vì quét các thành phần với **@Component**, bạn cũng có thể định nghĩa bean một cách tường minh bằng cách sử dụng annotation **@Bean**.

#### Ví dụ trong `AppConfig`:

```java
import org.springframework.context.annotation.Bean;

@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {

    @Bean
    public NumberGenerator numberGenerator() {
        return new NumberGeneratorImpl(); // Trả về một bean của NumberGenerator
    }

    @Bean
    public Game game() {
        return new GameImpl(); // Trả về một bean của Game
    }
}
```

Annotation **@Bean** cho biết phương thức này trả về một đối tượng bean được quản lý bởi Spring. Bạn có thể sử dụng nó để định nghĩa các bean mà Spring sẽ khởi tạo và quản lý.

### **Bước 5: Chạy và Kiểm Tra Ứng Dụng**

Sau khi thực hiện các bước trên, bạn có thể chạy ứng dụng để kiểm tra xem Spring có khởi tạo đúng các bean không. Nếu thành công, bạn sẽ thấy rằng các bean `NumberGenerator` và `Game` đã được tạo và hoạt động bình thường.

### **So sánh @Component và @Bean**

1. **@Component**: Dùng để đánh dấu một lớp như là một bean của Spring, và Spring sẽ tự động quét và quản lý các lớp này nếu bạn sử dụng **@ComponentScan**.
   
2. **@Bean**: Dùng trong các lớp cấu hình (annotated với **@Configuration**) để tạo các bean theo cách tường minh. Điều này giúp bạn dễ dàng kiểm soát việc khởi tạo bean và có thể tùy chỉnh thêm khi cần thiết.

### **Kết luận**

- **@Configuration** và **@ComponentScan** cho phép chúng ta cấu hình Spring mà không cần dùng đến XML.
- **@Bean** giúp tạo ra các bean một cách tường minh và linh hoạt hơn khi cần kiểm soát việc khởi tạo bean.
- Sử dụng cấu hình Java giúp code rõ ràng, dễ quản lý và tránh được việc phải sử dụng XML phức tạp.

Trong video tiếp theo, chúng ta sẽ thảo luận về các thử thách mà bạn có thể đối mặt khi làm việc với cấu hình Spring và cách giải quyết chúng.
