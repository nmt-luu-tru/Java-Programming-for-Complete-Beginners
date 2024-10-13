### Sử dụng Dependency Injection dựa trên Constructor

Trong video này, chúng ta sẽ học cách sử dụng **constructor-based dependency injection** trong Spring. Chúng ta đã đi đến bước 3 trong sơ đồ lớp của dự án. Hiện tại, biến **numberGenerator** trong lớp **GameImpl** chưa được khởi tạo, và chúng ta cần tạo một định nghĩa bean cho lớp này để có thể sử dụng **numberGenerator**. Chúng ta sẽ xem cách cấu hình nó trong **Spring IoC container**.

#### Bước 1: Cập nhật `beans.xml` với Bean của `GameImpl`

Đầu tiên, chúng ta phải định nghĩa bean cho **GameImpl** trong tệp **beans.xml**.

```xml
<bean id="game" class="Academy.learnprogramming.GameImpl">
</bean>
```

- Trong đoạn mã trên, chúng ta đã định nghĩa một bean với **id** là "game" và trỏ tới lớp **GameImpl**. 

#### Bước 2: Lấy Bean trong Lớp Chính (Main Class)

Tiếp theo, chúng ta sẽ yêu cầu Spring container trả về đối tượng bean **Game** trong lớp **Main** và gọi phương thức **reset**.

```java
// Lấy đối tượng game từ container
Game game = context.getBean(Game.class);

// Gọi phương thức reset
game.reset();
```

- **getBean(Game.class)** sẽ trả về đối tượng **Game** từ Spring container.

#### Bước 3: Xử lý lỗi NullPointerException

Khi chạy mã, chúng ta có thể gặp lỗi **NullPointerException** vì biến **numberGenerator** chưa được khởi tạo trong **GameImpl**.

#### Bước 4: Sử dụng Constructor-Based Dependency Injection

Chúng ta sẽ sửa lỗi trên bằng cách sử dụng **constructor-based dependency injection**. Để làm điều này, chúng ta cần thêm một constructor vào lớp **GameImpl** và thay đổi định nghĩa bean trong **beans.xml**.

##### Thêm Constructor trong `GameImpl`

```java
public class GameImpl implements Game {
    private final NumberGenerator numberGenerator;

    // Constructor với dependency injection
    public GameImpl(NumberGenerator numberGenerator) {
        this.numberGenerator = numberGenerator;
    }

    @Override
    public void reset() {
        smallest = 0;
        guess = 0;
        remainingGuesses = guessCount;
        biggest = numberGenerator.getMaxNumber();
        number = numberGenerator.next();
        log.debug("The number is {}", number);
    }

    // Các phương thức khác...
}
```

- Constructor này sẽ nhận đối tượng **NumberGenerator** làm tham số và khởi tạo trường **numberGenerator**.

##### Cập nhật `beans.xml`

Tiếp theo, chúng ta cần thay đổi tệp **beans.xml** để Spring container biết cách inject **NumberGenerator** vào **GameImpl**.

```xml
<bean id="game" class="Academy.learnprogramming.GameImpl">
    <constructor-arg ref="numberGenerator"/>
</bean>

<bean id="numberGenerator" class="Academy.learnprogramming.NumberGeneratorImpl"/>
```

- Trong đoạn mã trên, chúng ta đã chỉ rõ rằng **GameImpl** phụ thuộc vào **NumberGenerator** và sử dụng **constructor-arg** để inject dependency này. 

#### Bước 5: Kiểm Tra

Sau khi cấu hình xong, chúng ta có thể chạy chương trình và kiểm tra kết quả. Khi chạy chương trình, bạn sẽ thấy không có lỗi và số được sinh ra bởi **NumberGenerator** được in ra như mong đợi.

### Kết Luận

Chúng ta đã thành công trong việc sử dụng **constructor-based dependency injection** để inject **NumberGenerator** vào **GameImpl**. Điều này giúp cải thiện tính linh hoạt và khả năng quản lý của mã nguồn, đồng thời tách biệt rõ ràng các dependency, giúp mã dễ dàng bảo trì và mở rộng trong tương lai. Trong video tiếp theo, chúng ta sẽ tìm hiểu về **setter-based dependency injection**.
