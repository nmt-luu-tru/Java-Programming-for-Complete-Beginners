### Sự Khác Biệt Giữa @Component và @Bean trong Spring Framework

Trong bước này, chúng ta sẽ tìm hiểu sự khác biệt giữa **@Component** và **@Bean** và khi nào nên sử dụng từng cái. Cả hai đều được sử dụng để khai báo **Spring Beans**, nhưng cách thức và ngữ cảnh sử dụng chúng khác nhau.

### 1. **@Component**
- **@Component** được sử dụng trên bất kỳ lớp Java nào để đánh dấu lớp đó là một **Spring Bean**.
- Khi bạn thêm **@Component** vào một lớp (như **MarioGame** hay **GameRunner**), Spring sẽ quản lý instance của lớp đó.
- Khi sử dụng **@Component**, Spring sẽ tự động quét các lớp trong phạm vi **component scan** và tạo các bean từ những lớp được đánh dấu **@Component**.

**Ví dụ**:
```java
@Component
public class MarioGame implements GamingConsole {
    // Implementation
}
```
Trong ví dụ trên, Spring sẽ tự động tạo một bean cho **MarioGame** khi phát hiện **@Component** trên lớp đó thông qua quá trình **component scan**.

### 2. **@Bean**
- **@Bean** được sử dụng trên một phương thức trong một lớp **Spring Configuration** để khai báo một **Spring Bean** thông qua việc gọi phương thức đó.
- **@Bean** thường được sử dụng khi bạn cần tự viết mã để tạo bean hoặc khi cần cấu hình phức tạp hơn.

**Ví dụ**:
```java
@Configuration
public class AppConfig {

    @Bean
    public MarioGame marioGame() {
        return new MarioGame();
    }
}
```
Trong ví dụ này, bạn đang tạo một **bean** cho **MarioGame** bằng cách khai báo một phương thức có **@Bean** trong lớp cấu hình.

### 3. Sự Khác Biệt Chính Giữa @Component và @Bean

#### 3.1. **Cách Sử Dụng**

- **@Component**: Được sử dụng trực tiếp trên lớp, giúp Spring tự động quét và quản lý instance của lớp đó.
- **@Bean**: Được sử dụng trên phương thức trong lớp **@Configuration**, yêu cầu lập trình viên tự viết mã để tạo và cấu hình bean.

#### 3.2. **Tạo Bean Tự Động vs. Tạo Bean Thủ Công**

- **@Component**: Spring tự động tạo và quản lý bean thông qua **component scan**. Bạn chỉ cần đánh dấu lớp bằng **@Component** và Spring sẽ lo phần còn lại.
- **@Bean**: Bạn tự chịu trách nhiệm viết mã để tạo bean và Spring sẽ quản lý bean đó sau khi nó được tạo.

#### 3.3. **Quản Lý Phụ Thuộc (Auto-wiring)**

- **@Component**: Bạn có thể dễ dàng quản lý các phụ thuộc thông qua **constructor injection**, **setter injection**, hoặc **field injection**.
- **@Bean**: Bạn có thể truyền các phụ thuộc vào phương thức **@Bean** thông qua tham số hoặc sử dụng các phương thức để gọi các phụ thuộc khác trong quá trình tạo bean.

**Ví dụ** (Auto-wiring với @Component):
```java
@Component
public class GameRunner {

    @Autowired
    private GamingConsole game;

    // Constructor, setter, or field injection
}
```

**Ví dụ** (Auto-wiring với @Bean):
```java
@Configuration
public class AppConfig {

    @Bean
    public GameRunner gameRunner(GamingConsole game) {
        return new GameRunner(game);
    }
}
```

### 4. Khi Nào Nên Sử Dụng @Component và @Bean?

#### 4.1. **Khi Sử Dụng @Component**
- **@Component** thường được khuyến nghị sử dụng khi bạn tạo các **bean** cho các lớp trong ứng dụng của mình.
- Nó dễ sử dụng vì bạn chỉ cần đánh dấu lớp với **@Component** và Spring sẽ tự động quản lý bean.
- Phù hợp khi bạn không cần kiểm soát nhiều về cách tạo bean hoặc không có yêu cầu logic đặc biệt trong quá trình tạo bean.

#### 4.2. **Khi Sử Dụng @Bean**
- **@Bean** nên được sử dụng khi bạn cần logic tùy chỉnh trước khi tạo bean.
- **@Bean** hữu ích khi bạn cần tạo bean cho các thư viện bên thứ ba mà bạn không thể thay đổi mã nguồn của chúng để thêm **@Component**.
- Ví dụ: Khi bạn cần tạo bean cho **Spring Security** hoặc các thư viện bên ngoài, bạn không thể thêm **@Component** vào mã nguồn của thư viện đó, nên bạn sẽ sử dụng **@Bean** để tạo bean cho chúng.

**Ví dụ**:
```java
@Configuration
public class SecurityConfig {

    @Bean
    public SecurityManager securityManager() {
        return new SecurityManager();
    }
}
```

### 5. Tóm Lại

- **@Component**: Dễ sử dụng và được khuyến nghị cho các lớp bạn tự viết trong ứng dụng của mình. Chỉ cần thêm **@Component** vào lớp và Spring sẽ tự động tạo bean và quản lý phụ thuộc.
- **@Bean**: Được sử dụng khi bạn cần logic phức tạp trước khi tạo bean hoặc khi bạn cần tạo bean cho các thư viện bên ngoài mà bạn không thể chỉnh sửa mã nguồn của chúng.

Nhớ rằng **@Component** thường được sử dụng trong các ứng dụng tiêu chuẩn, trong khi **@Bean** là lựa chọn lý tưởng khi bạn cần tạo bean với logic tùy chỉnh hoặc khi làm việc với các thư viện bên thứ ba.

Hẹn gặp bạn ở bước tiếp theo!
