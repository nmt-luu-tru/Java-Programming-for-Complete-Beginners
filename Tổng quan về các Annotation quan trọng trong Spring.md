### Tổng quan về các Annotation quan trọng trong Spring

Trong bước này, chúng ta sẽ điểm lại một số annotation quan trọng trong Spring mà chúng ta đã học từ đầu đến giờ. Những annotation này đóng vai trò quan trọng trong việc cấu hình và quản lý các bean trong Spring Framework.

#### 1. **@Configuration**
- **@Configuration** chỉ ra rằng một lớp khai báo một hoặc nhiều phương thức **@Bean**.
- Spring sẽ xử lý lớp này để tạo ra các định nghĩa bean.
- Các phương thức được đánh dấu **@Bean** sẽ trả về các bean mà Spring quản lý.

Ví dụ:
```java
@Configuration
public class GamingConfiguration {
    @Bean
    public GameRunner gameRunner() {
        return new GameRunner();
    }
}
```

#### 2. **@ComponentScan**
- **@ComponentScan** định nghĩa các package mà Spring sẽ quét để tìm các component (bean).
- Nếu không chỉ định package, nó sẽ quét từ package hiện tại và các sub-package của nó.

Ví dụ:
```java
@ComponentScan("com.in28minutes")
public class AppConfig {}
```

#### 3. **@Component**
- **@Component** chỉ ra rằng lớp này là một component do Spring quản lý (bean).
- Đây là annotation cơ bản cho các annotation khác chuyên biệt hơn như **@Service**, **@Controller**, và **@Repository**.

Ví dụ:
```java
@Component
public class MarioGame {}
```

#### 4. **@Service**
- **@Service** là một dạng chuyên biệt của **@Component**, thường được sử dụng cho các lớp chứa logic nghiệp vụ.

Ví dụ:
```java
@Service
public class BusinessCalculationService {}
```

#### 5. **@Controller**
- **@Controller** là một dạng chuyên biệt của **@Component**, được sử dụng để định nghĩa các lớp controller, ví dụ như xử lý các yêu cầu web hoặc API REST.

Ví dụ:
```java
@Controller
public class WebController {}
```

#### 6. **@Repository**
- **@Repository** là một dạng chuyên biệt của **@Component**, thường được sử dụng cho các lớp tương tác với cơ sở dữ liệu.

Ví dụ:
```java
@Repository
public class MySQLDataService {}
```

#### 7. **@Primary**
- **@Primary** được sử dụng để ưu tiên một bean khi có nhiều bean cùng loại để autowire.

Ví dụ:
```java
@Primary
@Service
public class MarioGame implements GamingConsole {}
```

#### 8. **@Qualifier**
- **@Qualifier** được sử dụng để chỉ định chính xác bean nào sẽ được autowire khi có nhiều bean cùng loại.

Ví dụ:
```java
@Service
public class GameRunner {
    @Autowired
    @Qualifier("pacmanGame")
    private GamingConsole game;
}
```

#### 9. **@Lazy**
- **@Lazy** chỉ định rằng một bean sẽ được khởi tạo chậm (lazy initialization), tức là chỉ khởi tạo khi cần thiết.

Ví dụ:
```java
@Lazy
@Component
public class GameRunner {}
```

#### 10. **@Scope**
- **@Scope** dùng để định nghĩa phạm vi (scope) của một bean trong Spring.
- Hai phạm vi phổ biến nhất là **singleton** (một instance duy nhất cho mỗi Spring container) và **prototype** (một instance mới mỗi lần yêu cầu bean).

Ví dụ:
```java
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
@Component
public class PrototypeGame {}
```

#### 11. **@PostConstruct**
- **@PostConstruct** dùng để đánh dấu một phương thức sẽ được thực thi sau khi tất cả các dependency đã được inject để thực hiện các công việc khởi tạo.

Ví dụ:
```java
@PostConstruct
public void initialize() {
    System.out.println("Khởi tạo xong");
}
```

#### 12. **@PreDestroy**
- **@PreDestroy** dùng để đánh dấu một phương thức sẽ được thực thi ngay trước khi bean bị hủy.

Ví dụ:
```java
@PreDestroy
public void cleanup() {
    System.out.println("Đang dọn dẹp");
}
```

#### 13. **@Named**
- **@Named** là annotation trong CDI (Context and Dependency Injection), tương đương với **@Component** trong Spring.

Ví dụ:
```java
@Named
public class PacmanGame {}
```

#### 14. **@Inject**
- **@Inject** là một annotation khác trong CDI, tương tự như **@Autowired** trong Spring.

Ví dụ:
```java
@Inject
public void setDataService(DataService dataService) {
    this.dataService = dataService;
}
```

### Tóm tắt
- **@Component**, **@Service**, **@Controller**, và **@Repository** là các annotation chính để định nghĩa các bean trong Spring.
- **@Primary** và **@Qualifier** dùng để điều khiển việc autowire khi có nhiều bean cùng loại.
- **@Lazy**, **@Scope**, **@PostConstruct**, và **@PreDestroy** giúp kiểm soát vòng đời và hành vi khởi tạo của bean.
- **@Named** và **@Inject** là các annotation CDI tương tự như **@Component** và **@Autowired** trong Spring.

Những annotation này là các công cụ cần thiết để quản lý bean, dependency, và cấu hình ứng dụng trong Spring Framework.
