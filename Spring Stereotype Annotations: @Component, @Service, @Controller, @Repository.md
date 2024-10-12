### Spring Stereotype Annotations: @Component, @Service, @Controller, @Repository

Trong bước này, chúng ta sẽ tìm hiểu về các **annotations** trong Spring được gọi là **stereotype annotations**. Mặc dù chúng ta đã sử dụng **@Component** trong các bước trước, có một số annotations khác nhau mà chúng ta có thể sử dụng tùy thuộc vào mục đích của class.

#### 1. **@Component**
**@Component** là một annotation cơ bản trong Spring, và nó có thể được áp dụng cho bất kỳ class nào mà bạn muốn Spring quản lý. Khi bạn thêm **@Component** vào một class, Spring sẽ coi đó là một **Spring Bean** và quản lý vòng đời của nó. **@Component** là nền tảng cho tất cả các **stereotype annotations** khác.

#### 2. **@Service**
**@Service** là một chuyên biệt hóa của **@Component** và thường được sử dụng khi class chứa logic nghiệp vụ. Nếu bạn viết các phương thức hoặc logic liên quan đến nghiệp vụ, thì **@Service** là lựa chọn phù hợp. Nó giúp mã của bạn trở nên dễ đọc hơn, cho thấy rằng class này có trách nhiệm về nghiệp vụ.

#### 3. **@Controller**
**@Controller** được sử dụng khi bạn đang xây dựng các ứng dụng web, đặc biệt là các **REST APIs** hoặc các controller trong các ứng dụng web MVC. Nếu một class xử lý các yêu cầu HTTP, thì **@Controller** là annotation cần thiết. Nó cũng là nền tảng cho **@RestController**.

#### 4. **@Repository**
**@Repository** được sử dụng khi class có nhiệm vụ tương tác với cơ sở dữ liệu. Nếu class đó lưu trữ, truy xuất, hoặc thao tác dữ liệu từ cơ sở dữ liệu, thì **@Repository** là annotation phù hợp. **@Repository** không chỉ giúp biểu thị mục đích của class mà còn tự động kích hoạt các tính năng như **JDBC exception translation** trong Spring.

### Ví Dụ Thực Tế
Trong ví dụ thực tế về Spring Context launcher application, chúng ta có class **BusinessCalculationService** và các class **MongoDBDataService** và **MySQLDataService**. Trước đây, chúng ta sử dụng **@Component** để khai báo các class này là Spring Bean. Tuy nhiên, giờ đây ta sẽ thay thế chúng bằng các **stereotype annotations** phù hợp hơn:

- **@Service** cho **BusinessCalculationService**, vì đây là class chứa logic nghiệp vụ.
- **@Repository** cho **MongoDBDataService** và **MySQLDataService**, vì chúng tương tác với cơ sở dữ liệu MongoDB và MySQL.

```java
// BusinessCalculationService.java
@Service
public class BusinessCalculationService {
    // Business logic
}

// MongoDBDataService.java
@Repository
public class MongoDBDataService {
    // Data interaction with MongoDB
}

// MySQLDataService.java
@Repository
public class MySQLDataService {
    // Data interaction with MySQL
}
```

### Tại Sao Sử Dụng Annotations Cụ Thể?
Có hai lý do chính để sử dụng các annotations cụ thể:
1. **Cung cấp thông tin rõ ràng hơn cho framework**: Khi bạn sử dụng **@Service**, **@Repository**, hoặc **@Controller**, bạn đang cung cấp cho Spring thông tin chính xác về vai trò của class trong hệ thống.
2. **Hỗ trợ AOP (Aspect-Oriented Programming)**: Bạn có thể tận dụng **aspect-oriented programming** để thêm các hành vi bổ sung cho các class dựa trên annotations. Ví dụ: Spring tự động kích hoạt tính năng **JDBC exception translation** cho các class có annotation **@Repository**.

### Kết Luận
- **@Component** là annotation chung có thể áp dụng cho bất kỳ class nào.
- **@Service** được sử dụng khi class có logic nghiệp vụ.
- **@Controller** được sử dụng cho các controller trong ứng dụng web.
- **@Repository** được sử dụng cho các class tương tác với cơ sở dữ liệu.

Sử dụng các **stereotype annotations** cụ thể sẽ giúp mã của bạn dễ hiểu hơn và có khả năng mở rộng tốt hơn trong tương lai. Hãy áp dụng các annotations này khi bạn phát triển các ứng dụng Spring Framework.
