### Các Scope của Spring Beans

Trong bước này, chúng ta sẽ tìm hiểu về các **scope** khác nhau của **Spring Beans** và cách chúng ảnh hưởng đến việc khởi tạo và quản lý các đối tượng trong **Spring Framework**. Các scope phổ biến nhất là **Singleton** và **Prototype**, và chúng ta cũng sẽ đề cập đến một số scope khác sử dụng trong các ứng dụng web.

### 1. **Singleton Scope**
- **Singleton** là scope mặc định trong Spring. Khi bạn yêu cầu một bean với scope **Singleton**, **Spring IoC container** sẽ chỉ tạo **một** instance duy nhất cho bean đó và trả lại instance này mỗi khi bạn yêu cầu bean.
- Điều này có nghĩa là bất cứ khi nào bạn gọi `context.getBean()` với một bean có scope **Singleton**, Spring sẽ luôn trả về cùng một đối tượng.

**Ví dụ:**
```java
@Component
public class NormalClass {
    // Một class bình thường với scope mặc định (Singleton)
}
```

### 2. **Prototype Scope**
- Với **Prototype**, mỗi lần bạn yêu cầu một bean từ **Spring IoC container**, **Spring** sẽ tạo ra một instance mới của bean đó.
- Điều này rất hữu ích khi bạn cần tạo ra nhiều đối tượng giống nhau nhưng muốn chúng độc lập với nhau.

**Ví dụ:**
```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class PrototypeClass {
    // Một class với scope Prototype
}
```

### 3. **So Sánh Singleton và Prototype**
Để hiểu rõ hơn, hãy xem kết quả của việc gọi `context.getBean()` với các bean có scope khác nhau.

```java
public class BeanScopesLauncherApplication {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(BeanScopesLauncherApplication.class)) {
            
            // Lấy bean NormalClass với scope Singleton
            NormalClass normal1 = context.getBean(NormalClass.class);
            NormalClass normal2 = context.getBean(NormalClass.class);
            
            // Kết quả: Cùng một đối tượng NormalClass
            System.out.println(normal1);
            System.out.println(normal2);

            // Lấy bean PrototypeClass với scope Prototype
            PrototypeClass proto1 = context.getBean(PrototypeClass.class);
            PrototypeClass proto2 = context.getBean(PrototypeClass.class);
            
            // Kết quả: Các đối tượng PrototypeClass khác nhau
            System.out.println(proto1);
            System.out.println(proto2);
        }
    }
}
```

**Kết quả:**
- **NormalClass** (Singleton): Mã băm của đối tượng (hash code) giống nhau.
- **PrototypeClass** (Prototype): Mã băm của đối tượng khác nhau, cho thấy các instance độc lập được tạo ra.

### 4. **Các Scope trong Ứng Dụng Web**

Ngoài **Singleton** và **Prototype**, Spring còn cung cấp các scope dành riêng cho ứng dụng web:
- **Request Scope**: Một bean được tạo mới cho mỗi HTTP request.
- **Session Scope**: Một bean được tạo mới cho mỗi session người dùng.
- **Application Scope**: Một bean duy nhất được tạo cho toàn bộ ứng dụng web.
- **WebSocket Scope**: Một bean được tạo mới cho mỗi kết nối WebSocket.

### 5. **So Sánh Spring Singleton và Java Singleton**
- **Spring Singleton**: Chỉ có **một** instance bean trong **một** Spring IoC container. Nếu có nhiều IoC container trong cùng một **JVM**, mỗi container có thể có instance riêng.
- **Java Singleton**: Theo **Design Patterns (Gang of Four)**, một **Singleton** trong Java có nghĩa là chỉ có **một** instance của đối tượng đó trong toàn bộ JVM.

Trong hầu hết các ứng dụng, bạn chỉ có một Spring IoC container trong một JVM, do đó, **Spring Singleton** và **Java Singleton** thường được coi là giống nhau. Tuy nhiên, trong trường hợp bạn có nhiều Spring IoC container, chúng sẽ khác nhau.

### Tổng Kết:
- **Singleton Scope**: Được sử dụng cho hầu hết các trường hợp, đảm bảo rằng chỉ có một đối tượng duy nhất được tạo và dùng lại trong toàn bộ ứng dụng.
- **Prototype Scope**: Được sử dụng khi bạn cần tạo ra nhiều đối tượng độc lập mỗi khi yêu cầu bean từ Spring container.
- **Scope trong ứng dụng web**: Cung cấp các tùy chọn khác cho các ứng dụng dựa trên web như **request**, **session**, **application**, và **websocket**.

Hai scope quan trọng nhất cần chú ý là **Singleton** và **Prototype**. **Singleton** là mặc định và phù hợp cho hầu hết các trường hợp, trong khi **Prototype** hữu ích khi bạn cần đối tượng mới mỗi lần sử dụng.

Hẹn gặp lại bạn ở bước tiếp theo!
