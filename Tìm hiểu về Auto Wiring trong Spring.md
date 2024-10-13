### Tìm hiểu về **Auto Wiring** trong Spring

Trong video này, chúng ta sẽ học cách sử dụng annotation **@Autowired** để **inject** (tiêm) các **bean** tự động. Chúng ta sẽ sử dụng **dependency injection** bằng annotation.

### Cách Auto Wiring Beans
Khi sử dụng annotation **@Autowired**, bạn có thể inject dependencies theo nhiều cách:
1. **Auto wiring setter methods** (sử dụng setter method).
2. **Auto wiring via constructors** (inject qua constructor).
3. **Auto wiring instance variables** (inject trực tiếp vào biến instance).

Chúng ta đã học về **constructor-based** và **setter-based dependency injection**, nhưng lần này chúng ta sẽ sử dụng **auto wiring** với các biến instance, tức là sử dụng **dependency injection** trực tiếp vào các trường dữ liệu của lớp.

#### Bước 1: Chỉnh sửa file cấu hình beans.xml
Đầu tiên, chúng ta sẽ thêm thẻ `<context:annotation-config />` vào file `beans.xml`. Thẻ này sẽ kích hoạt cơ chế nhận dạng các annotation như **@Autowired**, **@PostConstruct**, và **@PreDestroy** trong các lớp bean.

Chúng ta sẽ cần xóa bỏ cấu hình cũ cho bean `commonAnnotationBeanPostProcessor`, vì nó đã được tự động thêm khi chúng ta sử dụng thẻ **context:annotation-config**.

**Cập nhật file `beans.xml`**:
1. Mở file `beans.xml` và thêm thẻ `<context:annotation-config />` để kích hoạt tự động cấu hình các annotation.
2. Xóa định nghĩa bean `commonAnnotationBeanPostProcessor`.

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
           http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context.xsd">
   
    <context:annotation-config />

    <!-- Định nghĩa bean cho game -->
    <bean id="game" class="com.example.GameImpl" />
    <bean id="numberGenerator" class="com.example.NumberGeneratorImpl" />

</beans>
```

#### Bước 2: Xóa setter method và sử dụng **@Autowired**
Mở lớp `GameImpl`, xóa **setter method** đã có và thay vào đó sử dụng **@Autowired** để inject `NumberGenerator` vào trực tiếp biến instance.

```java
@Component
public class GameImpl implements Game {

    @Autowired
    private NumberGenerator numberGenerator;

    // Các phương thức khác...

}
```

### Chạy ứng dụng
Sau khi thực hiện các thay đổi, chúng ta có thể chạy ứng dụng. Spring sẽ tự động **inject** bean `NumberGenerator` vào trường `numberGenerator` trong lớp `GameImpl`.

Trong file log, bạn sẽ thấy các dòng log thể hiện quá trình auto wiring của Spring, như là:
```
Autowiring by type from bean name 'game' to bean named 'numberGenerator'
```

### Kết luận
- Sử dụng annotation **@Autowired** giúp Spring tự động inject dependencies mà không cần viết mã cấu hình bằng tay.
- Annotation **@Autowired** có thể được sử dụng với cả **constructor-based**, **setter-based**, và **field-based** dependency injection.
- Trong thực tiễn, **constructor-based** dependency injection được khuyến khích hơn vì nó đảm bảo các dependency không bị null và cho phép tạo các đối tượng không thay đổi (immutable).

Với **Auto Wiring**, Spring tự động tạo và quản lý các dependency cho chúng ta, giúp mã ngắn gọn hơn và dễ bảo trì.

### Trong video tiếp theo
Chúng ta sẽ tìm hiểu thêm về **beans as components** và cách sử dụng **@Component** để tự động nhận diện và cấu hình các bean trong Spring. Hẹn gặp lại bạn ở video tiếp theo!
