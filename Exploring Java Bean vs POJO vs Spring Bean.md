### Sự khác biệt giữa **Java Bean**, **POJO**, và **Spring Bean**

#### 1. **POJO** (Plain Old Java Object)
- **POJO** là một đối tượng Java thông thường, không có bất kỳ ràng buộc nào về cấu trúc hay phương thức.
- Một **POJO** không cần tuân thủ bất kỳ quy tắc nào như việc phải có constructor không tham số hoặc implement các interface đặc biệt.
- Ví dụ, một lớp Java với vài thuộc tính và phương thức thông thường là **POJO**.
- **Bất kỳ lớp Java nào** mà bạn tạo đều có thể coi là **POJO** nếu không có ràng buộc gì thêm.
  
**Ví dụ về POJO:**
```java
public class Person {
    private String name;
    private int age;

    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}
```

#### 2. **Java Bean**
- **Java Bean** là một POJO nhưng phải tuân thủ ba ràng buộc chính:
  1. **Phải có constructor không tham số** (no-arg constructor): Lớp phải có constructor công khai mà không nhận tham số.
  2. **Phải có getter và setter**: Các thuộc tính của lớp phải được truy cập và thay đổi thông qua các phương thức `getters` và `setters`.
  3. **Phải implement interface Serializable**: Để đối tượng có thể được tuần tự hóa và truyền qua mạng hoặc lưu trữ.

**Ví dụ về Java Bean:**
```java
import java.io.Serializable;

public class Person implements Serializable {
    private String name;
    private int age;

    // No-arg constructor
    public Person() {}

    // Getters and setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}
```

#### 3. **Spring Bean**
- **Spring Bean** là bất kỳ đối tượng Java nào được quản lý bởi **Spring Framework**.
- Khi một đối tượng được quản lý bởi **Spring IOC Container** (như **BeanFactory** hoặc **ApplicationContext**), nó trở thành một **Spring Bean**.
- Một **Spring Bean** có thể là một **POJO**, nhưng điều quan trọng là nó phải được quản lý bởi **Spring**.

**Ví dụ về Spring Bean:**
```java
@Configuration
public class AppConfig {
    @Bean
    public Person person() {
        return new Person();
    }
}

// Ở đây, đối tượng `Person` được Spring quản lý và trở thành một Spring Bean.
```

### Tóm tắt sự khác biệt:
- **POJO**: Bất kỳ lớp Java nào, không có yêu cầu đặc biệt.
- **Java Bean**: Một **POJO** nhưng phải có **constructor không tham số**, **getter/setter** và **implement Serializable**.
- **Spring Bean**: Bất kỳ đối tượng nào do **Spring Container** quản lý, có thể là **POJO** hoặc **Java Bean**, nhưng quan trọng là phải được **Spring** quản lý.

Trong bước này, chúng ta đã phân tích sự khác biệt giữa **Java Bean**, **POJO** và **Spring Bean**, và hiểu rõ hơn về cách chúng được sử dụng trong các ứng dụng Java và Spring.
