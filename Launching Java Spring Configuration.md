# Tạo Spring Bean Đầu Tiên Và Giới Thiệu Spring Configuration Class

## 1. Giới Thiệu Về Spring Bean

Trong Spring Framework, **Spring bean** là các đối tượng được Spring tạo, quản lý và kiểm soát vòng đời. Khi một đối tượng trở thành một **Spring bean**, Spring sẽ chịu trách nhiệm quản lý nó, bao gồm việc tạo, tiêm phụ thuộc và hủy đối tượng khi không còn sử dụng. Điều này giúp chúng ta không phải tự tay quản lý các đối tượng và phụ thuộc trong ứng dụng.

Trong ví dụ này, chúng ta sẽ tạo một **Spring bean** đơn giản là một chuỗi **name**, và để Spring Framework quản lý đối tượng này thông qua **Spring context**.

## 2. Khởi Tạo Spring Context Và Tạo Spring Bean

### Bước 1: Đổi Tên Lớp Hiện Tại

Để bắt đầu, chúng ta sẽ đổi tên lớp và dọn dẹp mã không cần thiết:

1. Nhấp chuột phải vào lớp **AppGamingBasicJava**, chọn **Refactor** -> **Rename** và đổi tên thành **App01GamingBasicJava**.
2. Xóa lớp **LearnSpringFrameworkApplication.java** vì chúng ta sẽ không sử dụng nó cho ví dụ này.

### Bước 2: Tạo Lớp Mới Cho Ví Dụ Hello World Với Spring

1. Sao chép lớp **App01GamingBasicJava** và đổi tên thành **App02HelloWorldSpring**.
2. Mở lớp **App02HelloWorldSpring**, xóa toàn bộ mã hiện tại và lưu lại.

### Bước 3: Khởi Chạy Spring Context

Bây giờ, chúng ta sẽ khởi tạo một **Spring context**, nơi Spring Framework quản lý các đối tượng. **Spring context** là môi trường mà Spring tạo và quản lý các bean trong ứng dụng. Đây là bước cơ bản để Spring Framework có thể quản lý các đối tượng thay cho chúng ta.

### Bước 4: Tạo Lớp Cấu Hình Spring

**Spring Configuration Class** là một lớp Java đặc biệt được đánh dấu bởi chú thích **@Configuration**, cho phép chúng ta định nghĩa các **Spring bean** mà Spring sẽ quản lý. Các phương thức trong lớp này trả về các đối tượng mà chúng ta muốn Spring quản lý dưới dạng bean.

#### Ví Dụ Cụ Thể

1. Tạo một lớp cấu hình Spring:

    - Nhấp chuột phải vào gói `com.in28minutes.learnspringframework`, chọn **New** -> **Class**.
    - Đặt tên lớp là **HelloWorldConfiguration** và nhấn **Finish**.

2. Thêm chú thích **@Configuration** để thông báo với Spring rằng đây là một lớp cấu hình.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class HelloWorldConfiguration {

    // Định nghĩa một Spring bean tên là 'name'
    @Bean
    public String name() {
        return "Hello, Spring!";
    }
}
```

### Giải Thích Lớp Cấu Hình Spring:

- **@Configuration**: Chú thích này cho biết đây là một lớp cấu hình, nơi chúng ta có thể định nghĩa các **Spring bean**.
- **@Bean**: Đánh dấu các phương thức trả về một đối tượng để Spring Framework quản lý nó như một bean. Trong ví dụ này, phương thức `name()` trả về một chuỗi và chuỗi này trở thành một **Spring bean** với tên là **name**.

Lớp cấu hình này định nghĩa một **bean** có tên là **name**. Khi Spring context được khởi tạo, Spring sẽ tạo và quản lý đối tượng này. Lợi ích của việc sử dụng **Spring Configuration Class** là chúng ta có thể dễ dàng kiểm soát và định nghĩa tất cả các bean trong ứng dụng tại một nơi duy nhất.

### Bước 5: Sử Dụng Spring Context Để Lấy Bean

Trong lớp **App02HelloWorldSpring**, chúng ta sẽ khởi tạo **Spring context** và lấy ra **Spring bean** được định nghĩa trong lớp cấu hình **HelloWorldConfiguration**.

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class App02HelloWorldSpring {
    public static void main(String[] args) {
        // Tạo Spring context từ lớp cấu hình HelloWorldConfiguration
        var context = new AnnotationConfigApplicationContext(HelloWorldConfiguration.class);

        // Lấy bean 'name' từ Spring context
        String name = context.getBean("name", String.class);
        System.out.println(name); // Kết quả sẽ là "Hello, Spring!"
    }
}
```

- **AnnotationConfigApplicationContext**: Đây là lớp dùng để khởi tạo **Spring context** dựa trên lớp cấu hình.
- **getBean**: Sử dụng phương thức này để lấy bean từ **Spring context**. Ở đây, chúng ta lấy **bean** với tên là **name** và loại là **String**.

### Bước 6: Chạy Ứng Dụng

Bạn có thể chạy ứng dụng bằng cách nhấp chuột phải vào **App02HelloWorldSpring** và chọn **Run As** -> **Java Application**. Kết quả sẽ là:

```
Hello, Spring!
```

Điều này cho thấy rằng **Spring Framework** đã tạo và quản lý thành công chuỗi **name** mà chúng ta đã định nghĩa trong lớp **HelloWorldConfiguration**.

## 3. Kết Luận

Trong bước này, chúng ta đã:

- Tạo một **Spring Configuration Class** để định nghĩa các **Spring bean**.
- Sử dụng **@Configuration** và **@Bean** để thông báo cho Spring về các đối tượng mà nó sẽ quản lý.
- Khởi tạo **Spring context** và lấy **Spring bean** từ đó.

**Spring Configuration Class** giúp chúng ta dễ dàng kiểm soát tất cả các **bean** trong ứng dụng tại một nơi duy nhất, giúp mã nguồn trở nên dễ quản lý và bảo trì. Trong bước tiếp theo, chúng ta sẽ tiếp tục mở rộng ví dụ này để quản lý các đối tượng phức tạp hơn, và khám phá thêm các tính năng của Spring Framework.
