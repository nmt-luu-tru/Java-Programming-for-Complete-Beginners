## Liệt Kê Bean và Xử Lý Nhiều Bean Trùng Khớp

### Câu hỏi 3: Làm thế nào để liệt kê tất cả các **bean** được quản lý bởi **Spring Framework**?

Để liệt kê tất cả các **bean** được quản lý bởi **Spring**, chúng ta có thể yêu cầu **Spring context** sử dụng phương thức `getBeanDefinitionNames()`. Phương thức này sẽ trả về một mảng tên của tất cả các **bean** đã được định nghĩa và đang được quản lý trong **Spring context**.

#### Ví dụ:

```java
String[] beanNames = context.getBeanDefinitionNames();
Arrays.stream(beanNames).forEach(System.out::println);
```

Ở đây:
- `getBeanDefinitionNames()` trả về mảng các tên **bean**.
- `Arrays.stream(beanNames)` biến mảng này thành một **stream**.
- `forEach(System.out::println)` in ra từng tên **bean**.

Khi bạn chạy chương trình, tất cả các **bean** (bao gồm cả các **bean** nội bộ của Spring) sẽ được liệt kê ra. Các **bean** mà bạn quan tâm là những **bean** mà bạn đã định nghĩa trong cấu hình của mình, chẳng hạn như `name`, `age`, `person`, `address`.

#### Kết quả ví dụ:

```
org.springframework.context.annotation.internalConfigurationAnnotationProcessor
org.springframework.context.annotation.internalAutowiredAnnotationProcessor
org.springframework.context.annotation.internalCommonAnnotationProcessor
org.springframework.context.event.internalEventListenerProcessor
org.springframework.context.event.internalEventListenerFactory
helloWorldConfiguration
name
age
personTwoMethodCall
personThreeParameters
addressTwo
addressThree
```

### Câu hỏi 4: Điều gì xảy ra nếu có nhiều **bean** trùng khớp?

Khi bạn yêu cầu **Spring** cung cấp một **bean** dựa trên kiểu dữ liệu (như `Person.class` hoặc `Address.class`), nếu có nhiều **bean** cùng kiểu được định nghĩa, bạn sẽ gặp lỗi vì **Spring** không biết nên trả về **bean** nào.

Ví dụ, nếu bạn có nhiều **bean** kiểu `Person` hoặc `Address`:

```java
System.out.println(context.getBean(Address.class));
```

Khi chạy, bạn sẽ nhận được ngoại lệ:

```
Exception: No qualifying bean of type 'Address' available: expected single matching bean but found 2: addressTwo,addressThree
```

### Cách xử lý khi có nhiều **bean** trùng khớp

1. **Sử dụng tên **bean**: Nếu có nhiều **bean** cùng kiểu, bạn có thể chỉ định tên cụ thể của **bean** khi gọi `getBean()`.

```java
System.out.println(context.getBean("addressTwo", Address.class));
```

2. **Sử dụng ghi chú `@Primary`**: Bạn có thể chỉ định một **bean** ưu tiên bằng cách sử dụng ghi chú `@Primary`. Khi đó, **Spring** sẽ chọn **bean** được đánh dấu `@Primary` khi có nhiều **bean** trùng khớp về kiểu.

```java
@Bean
@Primary
public Address addressTwo() {
    return new Address("Baker Street", "London");
}
```

3. **Sử dụng `@Qualifier`**: Khi có nhiều **bean**, bạn có thể chỉ định cụ thể **bean** nào sẽ được sử dụng bằng cách sử dụng `@Qualifier`.

```java
@Autowired
@Qualifier("addressThree")
private Address address;
```

### Tổng Kết

- Để liệt kê tất cả các **bean** được **Spring** quản lý, sử dụng `context.getBeanDefinitionNames()`.
- Nếu có nhiều **bean** cùng kiểu, bạn có thể chỉ định rõ tên của **bean** trong `getBean()`, sử dụng `@Primary`, hoặc `@Qualifier` để giúp **Spring** xác định **bean** nào cần sử dụng.
