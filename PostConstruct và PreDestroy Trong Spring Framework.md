### PostConstruct và PreDestroy Trong Spring Framework

Trong bước này, chúng ta sẽ tìm hiểu về hai annotation rất quan trọng trong **Spring Framework**: **@PostConstruct** và **@PreDestroy**. Những annotation này được sử dụng để thực hiện các thao tác khởi tạo hoặc dọn dẹp tài nguyên trong vòng đời của **Spring Bean**. Chúng ta sẽ cùng nhau xây dựng ví dụ minh họa cách hoạt động của hai annotation này.

### 1. **@PostConstruct**: Khởi Tạo Sau Khi Các Phụ Thuộc Được Auto-Wire

- **@PostConstruct** được sử dụng để đánh dấu một phương thức trong bean sẽ được gọi ngay sau khi tất cả các phụ thuộc (dependencies) của bean đó đã được Spring tự động **auto-wire**. Thông thường, phương thức này sẽ được sử dụng để thực hiện các thao tác khởi tạo mà yêu cầu các phụ thuộc đã sẵn sàng.

**Ví dụ**:
```java
import jakarta.annotation.PostConstruct;
import org.springframework.stereotype.Component;

@Component
public class SomeClass {

    private final SomeDependency someDependency;

    // Constructor injection
    public SomeClass(SomeDependency someDependency) {
        this.someDependency = someDependency;
        System.out.println("All dependencies are ready");
    }

    @PostConstruct
    public void initialize() {
        System.out.println("Running initialization logic");
        someDependency.getReady();
    }
}
```

**SomeDependency**:
```java
import org.springframework.stereotype.Component;

@Component
public class SomeDependency {

    public void getReady() {
        System.out.println("SomeDependency is ready for use");
    }
}
```

**Giải thích**:
- **SomeClass** có một phụ thuộc **SomeDependency**, được auto-wire thông qua constructor.
- Phương thức `initialize()` được đánh dấu bằng **@PostConstruct**, và sẽ được gọi sau khi Spring đã hoàn thành việc tiêm phụ thuộc.
- Trong phương thức `initialize()`, chúng ta có thể thực hiện các thao tác khởi tạo (như gọi phương thức của **SomeDependency**).

### 2. **@PreDestroy**: Dọn Dẹp Trước Khi Bean Bị Hủy

- **@PreDestroy** được sử dụng để đánh dấu một phương thức sẽ được gọi **ngay trước khi bean bị hủy**. Thường thì phương thức này sẽ thực hiện các thao tác dọn dẹp, như đóng kết nối cơ sở dữ liệu hoặc giải phóng các tài nguyên mà bean đã giữ.

**Ví dụ**:
```java
import jakarta.annotation.PreDestroy;
import org.springframework.stereotype.Component;

@Component
public class SomeClass {

    private final SomeDependency someDependency;

    public SomeClass(SomeDependency someDependency) {
        this.someDependency = someDependency;
        System.out.println("All dependencies are ready");
    }

    @PostConstruct
    public void initialize() {
        System.out.println("Running initialization logic");
        someDependency.getReady();
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Cleaning up resources");
    }
}
```

**Giải thích**:
- **@PreDestroy** được sử dụng để đánh dấu phương thức `cleanup()`, phương thức này sẽ được gọi khi bean **SomeClass** chuẩn bị bị hủy khỏi **Spring IoC container**.
- Phương thức này rất hữu ích khi bạn cần đóng kết nối cơ sở dữ liệu, giải phóng bộ nhớ hoặc dừng các tiến trình nền (background tasks).

### 3. **Cách Hoạt Động**

- Khi bạn khởi động ứng dụng và Spring IoC container khởi tạo **SomeClass**:
  1. **Constructor** được gọi để tiêm phụ thuộc (**SomeDependency**).
  2. Sau khi tất cả các phụ thuộc đã được tiêm, **@PostConstruct** sẽ gọi phương thức `initialize()` để thực hiện các thao tác khởi tạo.
  
- Khi ứng dụng bị tắt, hoặc khi bean **SomeClass** bị hủy:
  1. **@PreDestroy** sẽ gọi phương thức `cleanup()` để thực hiện các thao tác dọn dẹp trước khi bean bị loại bỏ khỏi container.

### 4. **Kết Quả Chạy Ứng Dụng**

Khi chạy ứng dụng, bạn sẽ thấy kết quả tương tự như sau:

```
All dependencies are ready
Running initialization logic
SomeDependency is ready for use
Cleaning up resources
```

### 5. **Tóm Lại**

- **@PostConstruct**: Được sử dụng để thực hiện các thao tác khởi tạo **sau khi các phụ thuộc đã được tiêm**. Ví dụ: Kết nối đến cơ sở dữ liệu, tải dữ liệu ban đầu.
- **@PreDestroy**: Được sử dụng để thực hiện các thao tác dọn dẹp **trước khi bean bị hủy**, chẳng hạn như đóng kết nối cơ sở dữ liệu hoặc giải phóng các tài nguyên khác.

Hai annotation này giúp quản lý tốt hơn vòng đời của bean trong **Spring**, đặc biệt khi bạn cần thực hiện các thao tác phức tạp như khởi tạo kết nối hoặc dọn dẹp tài nguyên.

Hẹn gặp lại bạn ở bước tiếp theo!
