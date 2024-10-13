### **Beans as Components: Sử dụng Annotation và Component Scanning**

Trong video này, chúng ta sẽ học cách sử dụng **component scanning** để tự động tìm kiếm và quản lý các **bean** trong Spring bằng cách sử dụng annotation **@Component**. Đồng thời, chúng ta cũng tìm hiểu về các annotation đặc biệt như **@Service**, **@Controller**, và **@Repository**.

### **Component Scanning và Stereotyped Annotations**

Spring cung cấp một số **stereotyped annotations** như **@Component**, **@Service**, **@Controller**, và **@Repository**. Các annotation này đóng vai trò như các "nhãn" để chỉ ra vai trò của các lớp trong ứng dụng. Ví dụ:

- **@Component**: Dùng chung cho bất kỳ thành phần nào của Spring.
- **@Service**: Dùng cho các lớp xử lý logic nghiệp vụ.
- **@Controller**: Dùng cho các lớp xử lý yêu cầu từ người dùng trong ứng dụng web.
- **@Repository**: Dùng cho các lớp quản lý dữ liệu, kết nối cơ sở dữ liệu.

Những annotation này giúp giảm nhu cầu sử dụng cấu hình XML cho các bean trong Spring.

### **Bước 1: Kích hoạt Component Scanning**

Để kích hoạt **component scanning** trong XML, chúng ta cần thay thế thẻ **<context:annotation-config />** mà chúng ta đã sử dụng trước đó bằng thẻ **<context:component-scan />**. Thẻ này sẽ quét các gói trong ứng dụng để tìm các lớp đã được đánh dấu bằng **@Component** hoặc các annotation tương tự.

#### Cập nhật file `beans.xml`:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
           http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.example" />

</beans>
```

Trong đó, `base-package` là gói mà Spring sẽ quét để tìm các **component**.

### **Bước 2: Thêm Annotation @Component cho Các Lớp**

Bây giờ chúng ta sẽ thêm annotation **@Component** vào các lớp **GameImpl** và **NumberGeneratorImpl** để Spring tự động quản lý chúng.

#### Ví dụ lớp `GameImpl`:

```java
@Component
public class GameImpl implements Game {
    @Autowired
    private NumberGenerator numberGenerator;

    // Các phương thức khác...
}
```

#### Ví dụ lớp `NumberGeneratorImpl`:

```java
@Component
public class NumberGeneratorImpl implements NumberGenerator {
    // Implement các phương thức...
}
```

### **Bước 3: Kiểm tra và sửa lỗi khi chạy ứng dụng**

Nếu bạn gặp lỗi như:

```
No bean named 'numberGenerator' is available
```

Lý do có thể là do Spring tự động tạo tên cho các bean dựa trên tên lớp, với chữ cái đầu tiên viết thường. Trong trường hợp này, bạn có thể chỉ định tên cụ thể cho bean bằng cách thêm tham số vào **@Component** như sau:

```java
@Component("numberGenerator")
public class NumberGeneratorImpl implements NumberGenerator {
    // Implement các phương thức...
}
```

### **Bước 4: Loại bỏ tên bean và sử dụng kiểu dữ liệu**

Một cách khác để tránh lỗi này là sử dụng **loại dữ liệu** thay vì tên bean khi gọi bean từ container Spring. Điều này giúp giảm thiểu lỗi do việc nhập sai tên.

#### Cập nhật trong `Main.java`:

```java
@Autowired
private NumberGenerator numberGenerator;
```

Thay vì sử dụng tên, Spring sẽ tự động tìm kiếm bean dựa trên **loại dữ liệu** (`NumberGenerator`) để inject.

### **Kết luận**

- **Component scanning** giúp Spring tự động tìm kiếm và quản lý các bean, giảm nhu cầu phải cấu hình chúng trong XML.
- Sử dụng **@Component** và các annotation tương tự như **@Service**, **@Controller**, giúp mã ngắn gọn và dễ bảo trì hơn.
- Bạn có thể sử dụng **Auto Wiring** để tự động inject các bean mà không cần cấu hình phức tạp.

### **Trong video tiếp theo**
Chúng ta sẽ học về **Java Configuration** và cách sử dụng cấu hình dựa trên Java để thay thế cho cấu hình XML trong Spring.
