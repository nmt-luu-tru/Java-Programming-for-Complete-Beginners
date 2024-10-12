### Tạo **Bean** Mới và Tái Sử Dụng Các **Bean** Tồn Tại Trong **Spring**

Trong bước này, chúng ta sẽ khám phá cách tạo một **bean** mới (`personTwo`) bằng cách sử dụng các giá trị từ các **bean** đã tồn tại (`name` và `age`). Chúng ta sẽ xem xét hai cách để thực hiện điều này: thông qua **method calls** và thông qua **method parameters**.

#### 1. Tạo **Bean** Mới Bằng Cách Gọi Phương Thức

Đầu tiên, chúng ta sẽ sử dụng cách gọi phương thức. Chúng ta muốn tạo một **bean** mới có tên `personTwoMethodCall` và sử dụng các **bean** đã tồn tại:

```java
@Bean
public Person personTwoMethodCall() {
    String name = context.getBean("name", String.class); // Lấy giá trị name
    int age = context.getBean("age", Integer.class);    // Lấy giá trị age
    return new Person(name, age); // Tạo đối tượng Person mới
}
```

Để lấy **bean** này, chúng ta sẽ sử dụng:

```java
System.out.println(context.getBean("personTwoMethodCall"));
```

Khi chạy ứng dụng, bạn sẽ thấy rằng **bean** `personTwoMethodCall` được in ra với thông tin từ **bean** `name` và `age`. Kết quả hiển thị sẽ tương tự như sau:

```
Person{name='Ranga', age=15}
```

#### 2. Tạo **Bean** Mới Bằng Cách Sử Dụng Tham Số Phương Thức

Bây giờ, chúng ta sẽ thử cách thứ hai, sử dụng tham số. Cách này cho phép chúng ta chỉ định các tham số cho phương thức mà **Spring** sẽ tự động điền vào từ các **bean** đã được quản lý:

```java
@Bean
public Person personThreeParameters(String name, int age, Address address) {
    return new Person(name, age, address);
}
```

Chúng ta cần chỉ định đúng tên cho các tham số:

- `name`: Tương ứng với **bean** `name`.
- `age`: Tương ứng với **bean** `age`.
- `address`: Tương ứng với **bean** `addressTwo`.

Khi lấy **bean** này, bạn có thể làm như sau:

```java
System.out.println(context.getBean("personThreeParameters"));
```

Nếu bạn chạy ứng dụng, bạn sẽ nhận được cùng một kết quả cho **bean** này. Kết quả hiển thị sẽ tương tự như sau:

```
Person{name='Ranga', age=15, address=Address{firstLine='Baker Street', city='London'}}
```

#### 3. Thêm Địa Chỉ Mới cho **Person**

Chúng ta cũng có thể thêm một địa chỉ mới cho **personThree**:

```java
@Bean
public Address addressThree() {
    return new Address("Moti Nagar", "Hyderabad"); // Tạo địa chỉ mới
}
```

Và sửa đổi phương thức tạo `personThreeParameters` để sử dụng địa chỉ mới:

```java
@Bean
public Person personThreeParameters(String name, int age, Address addressThree) {
    return new Person(name, age, addressThree);
}
```

Để lấy **bean** này, bạn có thể sử dụng:

```java
System.out.println(context.getBean("personThreeParameters"));
```

Khi chạy ứng dụng, kết quả sẽ giống như sau:

```
Person{name='Ranga', age=15, address=Address{firstLine='Moti Nagar', city='Hyderabad'}}
```

#### 4. Giải Quyết Lỗi Nhiều **Bean** Tồn Tại

Nếu bạn gặp lỗi khi cố gắng lấy một **bean** với tên mà có nhiều **bean** cùng tên, như thông báo lỗi bạn đã thấy trước đó:

```
Expecting a matching bean but found two: addressTwo and addressThree
```

Để khắc phục điều này, bạn có thể sử dụng tên cụ thể của **bean** khi gọi:

```java
context.getBean("addressTwo", Address.class); // Lấy địa chỉ theo tên cụ thể
```

### Tổng Kết

Trong bước này, chúng ta đã:

1. **Tạo một **bean** mới** (`personTwo`) bằng cách gọi phương thức từ các **bean** đã tồn tại.
2. **Sử dụng tham số** để tạo một **bean** mới (`personThree`) từ các **bean** đã được quản lý.
3. **Thêm địa chỉ mới** cho đối tượng `Person`.
4. **Giải quyết lỗi** khi có nhiều **bean** cùng tên.

Những kiến thức này là rất quan trọng để giúp bạn hiểu cách **Spring** quản lý **beans** và tái sử dụng chúng một cách hiệu quả. Trong các bước tiếp theo, chúng ta sẽ khám phá thêm các tính năng nâng cao hơn trong **Spring Framework**!
