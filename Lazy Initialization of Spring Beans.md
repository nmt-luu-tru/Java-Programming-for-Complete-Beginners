### Lazy Initialization of Spring Beans

Trong bước này, chúng ta sẽ tìm hiểu về **Lazy Initialization** (khởi tạo trì hoãn) trong **Spring Framework**. Mặc định, **Spring Beans** được khởi tạo ngay khi ứng dụng khởi chạy, gọi là **Eager Initialization**. **Lazy Initialization** cho phép trì hoãn việc khởi tạo bean cho đến khi nó thực sự được sử dụng. Hãy cùng tìm hiểu thông qua một ví dụ thực tế.

### Ví Dụ về Eager Initialization (Khởi Tạo Mặc Định)

Chúng ta sẽ tạo một ứng dụng Spring đơn giản để minh họa cách hoạt động của **Eager Initialization**.

#### Bước 1: Tạo Hai Lớp ClassA và ClassB

```java
import org.springframework.stereotype.Component;

@Component
public class ClassA {
    // ClassA không có gì đặc biệt
}

@Component
public class ClassB {

    private final ClassA classA;

    // Constructor injection
    public ClassB(ClassA classA) {
        this.classA = classA;
        System.out.println("Some initialization logic goes here.");
    }

    public void doSomething() {
        System.out.println("Doing something in ClassB.");
    }
}
```

**Giải thích**:
- **ClassA** và **ClassB** đều là **Spring Beans** được đánh dấu bằng **@Component**.
- **ClassB** có phụ thuộc vào **ClassA**, và trong constructor, chúng ta thêm một số logic khởi tạo.
- Chúng ta sẽ in thông báo mỗi khi **ClassB** được khởi tạo để thấy rõ thời điểm bean được khởi tạo.

#### Bước 2: Tạo Lớp Khởi Chạy

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class LazyInitializationLauncherApplication {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(LazyInitializationLauncherApplication.class)) {
            System.out.println("Initialization of context is completed.");

            // Lấy bean ClassB và gọi phương thức doSomething()
            ClassB classB = context.getBean(ClassB.class);
            classB.doSomething();
        }
    }
}
```

**Giải thích**:
- **Spring Context** được khởi tạo và thông báo "Initialization of context is completed." sẽ được in ra khi việc khởi tạo hoàn tất.
- Chúng ta lấy bean **ClassB** và gọi phương thức `doSomething()` để thực thi.

#### Kết Quả với Eager Initialization

Khi bạn chạy ứng dụng, kết quả sẽ như sau:

```
Some initialization logic goes here.
Initialization of context is completed.
Doing something in ClassB.
```

- **Eager Initialization** được thực hiện, điều này có nghĩa là **ClassB** được khởi tạo ngay khi ứng dụng bắt đầu, mặc dù chúng ta chưa thực sự sử dụng nó.

### Lazy Initialization (Khởi Tạo Trì Hoãn)

Để trì hoãn việc khởi tạo **ClassB** cho đến khi nó thực sự được sử dụng, chúng ta có thể thêm **@Lazy** vào **ClassB**.

#### Bước 3: Thêm **@Lazy** vào ClassB

```java
@Component
@Lazy
public class ClassB {

    private final ClassA classA;

    public ClassB(ClassA classA) {
        this.classA = classA;
        System.out.println("Some initialization logic goes here.");
    }

    public void doSomething() {
        System.out.println("Doing something in ClassB.");
    }
}
```

#### Kết Quả với Lazy Initialization

Khi bạn chạy lại ứng dụng, kết quả sẽ thay đổi:

```
Initialization of context is completed.
Some initialization logic goes here.
Doing something in ClassB.
```

- **Lazy Initialization** được thực thi. Bạn sẽ thấy rằng **ClassB** chỉ được khởi tạo khi chúng ta thực sự sử dụng nó (gọi phương thức `doSomething()`).

### Khi Nào Nên Sử Dụng Lazy Initialization?

- **Eager Initialization** thường được khuyến nghị vì các lỗi trong cấu hình Spring sẽ được phát hiện ngay khi khởi chạy ứng dụng.
- **Lazy Initialization** chỉ nên được sử dụng khi có logic khởi tạo phức tạp, hoặc khi bạn muốn giảm thời gian khởi động ứng dụng. Tuy nhiên, cần lưu ý rằng lỗi trong cấu hình Spring sẽ chỉ xuất hiện khi bean thực sự được sử dụng, và điều này có thể gây ra lỗi vào thời điểm chạy ứng dụng (runtime errors).

### Tóm Lại

- **Eager Initialization** là cách khởi tạo mặc định trong Spring, giúp phát hiện lỗi sớm.
- **Lazy Initialization** có thể hữu ích trong một số trường hợp, nhưng cần sử dụng cẩn thận vì nó có thể gây ra lỗi chỉ khi bean được sử dụng.
- **@Lazy** có thể được sử dụng trên các lớp **@Component** hoặc các phương thức **@Bean** để trì hoãn việc khởi tạo bean.

Hẹn gặp lại bạn ở bước tiếp theo!
