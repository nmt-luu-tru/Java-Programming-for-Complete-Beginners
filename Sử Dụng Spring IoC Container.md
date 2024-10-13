### Sử Dụng Spring IoC Container

Trong video này, chúng ta sẽ tìm hiểu về **Spring IoC Container**, cách cấu hình nó, khái niệm **bean** là gì, và tạo ví dụ làm việc với Spring Container.

### IoC là gì?

**IoC** có nghĩa là **Inversion of Control** (Đảo ngược quyền điều khiển). **Spring IoC Container** hay đơn giản là container là một thành phần của **Spring Framework** dùng để chứa các bean và quản lý vòng đời của chúng.

Một **bean** là một đối tượng Java đơn giản, được khởi tạo, lắp ráp và quản lý bởi IoC container. Chúng ta sẽ thấy cách hoạt động của IoC qua một ví dụ thực tế.

### Tài Liệu Về IoC Container

Bạn có thể tìm hiểu thêm về **Spring IoC container** từ tài liệu chính thức của Spring. Để hiểu cơ bản, chúng ta cần cung cấp cho container hai thành phần chính: **POJOs** (Plain Old Java Objects) và **metadata** (dữ liệu cấu hình). Container sẽ kết hợp hai thành phần này để tạo ra một ứng dụng có thể chạy được.

### Ví Dụ Cấu Hình XML Cho IoC Container

Hãy tạo một tệp **beans.xml** để cấu hình container. Đây là ví dụ cấu hình đơn giản của một Spring IoC container sử dụng XML:

1. **Tạo tệp `beans.xml`:**
   - Vào thư mục **resources** của dự án và tạo tệp mới có tên **beans.xml**.
   - Dán cấu hình XML sau:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Chúng ta sẽ thêm cấu hình bean tại đây sau -->
</beans>
```

### Tạo Interface và Implementation Cho `NumberGenerator`

Dựa trên sơ đồ lớp (UML class diagram) mà chúng ta đã thảo luận, chúng ta sẽ tạo một **interface** `NumberGenerator` và lớp `NumberGeneratorImpl` để triển khai nó.

1. **Tạo Interface `NumberGenerator`:**
   - Tạo một **interface** với hai phương thức `next()` và `getMaxNumber()` trả về kiểu `int`.

```java
public interface NumberGenerator {
    int next();
    int getMaxNumber();
}
```

2. **Tạo Lớp `NumberGeneratorImpl`:**
   - Lớp này triển khai interface `NumberGenerator` và có hai trường là `Random` và `maxNumber`.

```java
import java.util.Random;

public class NumberGeneratorImpl implements NumberGenerator {
    private final Random random = new Random();
    private final int maxNumber = 100;

    @Override
    public int next() {
        return random.nextInt(maxNumber);
    }

    @Override
    public int getMaxNumber() {
        return maxNumber;
    }
}
```

### Cấu Hình Bean Cho `NumberGeneratorImpl`

Bây giờ chúng ta sẽ cấu hình một **bean** cho lớp `NumberGeneratorImpl` trong tệp **beans.xml** mà chúng ta đã tạo trước đó.

```xml
<bean id="numberGenerator" class="academy.learnprogramming.NumberGeneratorImpl"/>
```

### Sử Dụng Spring IoC Container

Sau khi đã cấu hình IoC container, chúng ta sẽ sử dụng nó để khởi tạo bean và gọi các phương thức trong lớp `NumberGeneratorImpl`.

1. **Tạo Lớp Main để Test:**
   - Sử dụng **ClassPathXmlApplicationContext** để khởi tạo container và lấy bean từ container.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    private static final Logger log = LoggerFactory.getLogger(Main.class);
    private static final String CONFIG_LOCATION = "beans.xml";

    public static void main(String[] args) {
        // Tạo IoC Container
        ConfigurableApplicationContext context =
                new ClassPathXmlApplicationContext(CONFIG_LOCATION);

        // Lấy bean từ container
        NumberGenerator numberGenerator = context.getBean("numberGenerator", NumberGenerator.class);

        // Gọi phương thức next() để tạo số ngẫu nhiên
        int number = numberGenerator.next();
        log.info("Generated number: {}", number);

        // Đóng container để tránh rò rỉ bộ nhớ
        context.close();
    }
}
```

### Kết Quả
Khi chạy chương trình, bạn sẽ thấy log hiển thị số ngẫu nhiên được sinh ra bởi **NumberGeneratorImpl**. Container IoC đã tự động khởi tạo và quản lý bean cho chúng ta.

### Bật Chế Độ Debug Cho Spring

Để thấy chi tiết hơn về quá trình khởi động container Spring, bạn có thể thêm cấu hình debug trong **logback.xml**:

```xml
<logger name="org.springframework" level="DEBUG"/>
```

Khi chạy lại chương trình, bạn sẽ thấy nhiều thông tin hơn về quá trình khởi tạo các bean, ví dụ như:

- **Creating shared instance of singleton bean 'numberGenerator'**
- **Returning cached instance of singleton bean 'numberGenerator'**

Điều này cho thấy **Spring** sử dụng mô hình **singleton** mặc định cho các bean, tức là chỉ có một thể hiện duy nhất của mỗi bean trong toàn bộ ứng dụng.

### Kết Luận

Chúng ta đã học cách sử dụng **Spring IoC container** để quản lý các bean và tạo ra một ứng dụng Spring đơn giản với cấu hình XML. Chúng ta cũng đã tìm hiểu về cách bật chế độ debug để hiểu rõ hơn về cách Spring khởi tạo các bean. Trong video tiếp theo, chúng ta sẽ bắt đầu triển khai logic cho trò chơi "Guess the Number".
