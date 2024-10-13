### **Message Generator Challenge: Giải thích và triển khai**

#### **Mục tiêu của thử thách:**
1. Tạo interface **MessageGenerator** với hai phương thức: `getMainMessage()` và `getResultMessage()`.
2. Tạo lớp **MessageGeneratorImpl** để triển khai interface.
3. Sử dụng **Logger**, autowire đối tượng **Game** và khởi tạo giá trị `guessCount` với giá trị 10.
4. Tạo phương thức **PostConstruct** để xác nhận autowire thành công.
5. Cấu hình lớp **AppConfig** để tạo một bean của **MessageGenerator**.
6. Trong lớp **Main**, gọi các phương thức từ bean **MessageGenerator** và xác nhận đầu ra từ console.

---

### **Bước 1: Tạo interface `MessageGenerator`**

Đầu tiên, ta tạo một interface có tên **MessageGenerator** với hai phương thức trả về chuỗi `String`.

```java
public interface MessageGenerator {
    String getMainMessage();
    String getResultMessage();
}
```

---

### **Bước 2: Tạo lớp `MessageGeneratorImpl`**

Tiếp theo, ta tạo lớp **MessageGeneratorImpl** triển khai từ interface **MessageGenerator**.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import javax.annotation.PostConstruct;
import org.springframework.beans.factory.annotation.Autowired;

public class MessageGeneratorImpl implements MessageGenerator {

    private static final Logger log = LoggerFactory.getLogger(MessageGeneratorImpl.class);

    @Autowired
    private Game game;  // Autowire Game object

    private int guessCount = 10;  // Initialize guessCount

    @PostConstruct
    public void init() {
        log.info("Game = {}", game);  // Confirm autowire success
    }

    @Override
    public String getMainMessage() {
        return "getMainMessage() called";
    }

    @Override
    public String getResultMessage() {
        return "getResultMessage() called";
    }
}
```

Ở đây, ta autowire đối tượng **Game**, khởi tạo giá trị cho **guessCount** và sử dụng **PostConstruct** để log thông tin.

---

### **Bước 3: Cấu hình lớp `AppConfig`**

Ta cần cấu hình lớp **AppConfig** để tạo bean cho **MessageGenerator**.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {

    @Bean
    public MessageGenerator messageGenerator() {
        return new MessageGeneratorImpl();  // Tạo bean của MessageGeneratorImpl
    }
}
```

---

### **Bước 4: Cập nhật lớp `Main`**

Trong lớp **Main**, ta sẽ lấy bean **MessageGenerator** và gọi hai phương thức `getMainMessage()` và `getResultMessage()`.

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        MessageGenerator messageGenerator = context.getBean(MessageGenerator.class);

        System.out.println(messageGenerator.getMainMessage());
        System.out.println(messageGenerator.getResultMessage());
    }
}
```

Ở đây, ta sử dụng **AnnotationConfigApplicationContext** để nạp cấu hình từ lớp **AppConfig**, sau đó lấy bean **MessageGenerator** và gọi hai phương thức.

---

### **Bước 5: Kiểm tra và xác nhận kết quả**

Khi chạy ứng dụng, bạn sẽ thấy các kết quả sau trên console:

```plaintext
getMainMessage() called
getResultMessage() called
```

Điều này cho thấy rằng cả hai phương thức `getMainMessage()` và `getResultMessage()` đã được gọi thành công.

---

### **Tóm tắt**

Trong thử thách này, bạn đã học cách:
- Tạo interface và triển khai class trong Spring.
- Sử dụng **@Autowired** để inject dependency.
- Tạo **bean** trong lớp cấu hình và quản lý nó bằng Spring container.
- Sử dụng **PostConstruct** để đảm bảo autowire được thực hiện đúng cách.

Ở video tiếp theo, chúng ta sẽ cải thiện logic của các phương thức **getMainMessage** và **getResultMessage** để thêm logic game vào đó.
