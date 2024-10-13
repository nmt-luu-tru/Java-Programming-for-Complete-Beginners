Trong video này, chúng ta đã tìm hiểu về cách sử dụng **properties** file trong Spring để cấu hình các giá trị mà không cần hard-code trong mã nguồn Java. Thay vì đặt các giá trị như **max number** và **guess count** trực tiếp trong mã, chúng ta đã chuyển sang sử dụng một **properties file**. Điều này giúp cho việc quản lý cấu hình dễ dàng hơn, linh hoạt hơn, và có thể thay đổi mà không cần biên dịch lại mã nguồn.

### **Các bước chính**

#### **1. Tạo file `game.properties`**

Trước hết, chúng ta tạo một **properties file** để lưu trữ các cấu hình cho trò chơi. File này được đặt trong thư mục `resources/config`.

Ví dụ, nội dung file `game.properties`:
```properties
# Game properties
game.maxNumber=100
game.guessCount=10
```
- **game.maxNumber**: Giá trị tối đa mà người chơi có thể đoán.
- **game.guessCount**: Số lần đoán tối đa mà người chơi được phép.

#### **2. Sử dụng `@PropertySource` để tải properties file**

Trong lớp **GameConfig**, chúng ta sử dụng annotation `@PropertySource` để chỉ định Spring tải properties file này khi khởi tạo context.

Ví dụ trong lớp **GameConfig**:
```java
@Configuration
@PropertySource("classpath:config/game.properties")
public class GameConfig {
    //...
}
```
Annotation `@PropertySource` giúp chỉ ra rằng chúng ta muốn Spring tải file `game.properties` từ đường dẫn `config/game.properties` trong **classpath**.

#### **3. Sử dụng `@Value` để tiêm giá trị từ properties file**

Tiếp theo, chúng ta sử dụng annotation `@Value` để lấy các giá trị từ properties file và tiêm chúng vào các thuộc tính trong các lớp cấu hình.

Ví dụ:
```java
@Value("${game.maxNumber}")
private int maxNumber;

@Value("${game.guessCount}")
private int guessCount;
```
Ở đây, chúng ta sử dụng cú pháp `@Value("${game.maxNumber}")` để lấy giá trị của **game.maxNumber** từ file `game.properties`. Nếu giá trị không được tìm thấy, Spring sẽ ném ra lỗi.

#### **4. Đặt giá trị mặc định với `@Value`**

Trong trường hợp file properties không chứa giá trị nào đó hoặc file không tồn tại, chúng ta có thể chỉ định giá trị mặc định bằng cách sử dụng cú pháp `:default_value`.

Ví dụ:
```java
@Value("${game.maxNumber:20}")
private int maxNumber;

@Value("${game.guessCount:5}")
private int guessCount;
```
Ở đây, nếu giá trị `game.maxNumber` không được tìm thấy, Spring sẽ sử dụng giá trị mặc định là `20`. Tương tự, `guessCount` sẽ có giá trị mặc định là `5` nếu không được tìm thấy.

#### **5. Chạy ứng dụng và kiểm tra**

Sau khi cấu hình xong, chúng ta chạy ứng dụng để đảm bảo các giá trị từ properties file được tiêm đúng cách và kiểm tra nếu giá trị mặc định hoạt động khi không tìm thấy properties trong file.

### **Kết quả**

Khi chạy ứng dụng, nếu file `game.properties` tồn tại và chứa giá trị:
- **max number** sẽ là 100.
- **guess count** sẽ là 10.

Nếu file không có các giá trị này, ứng dụng sẽ sử dụng các giá trị mặc định:
- **max number**: 20.
- **guess count**: 5.

### **Tổng kết**

Việc sử dụng **properties file** giúp quản lý cấu hình dễ dàng hơn, linh hoạt hơn và giúp tách biệt các thông tin cấu hình ra khỏi mã nguồn. Điều này không chỉ giúp mã nguồn dễ bảo trì mà còn giảm rủi ro sai sót khi cần thay đổi cấu hình.

Trong video tiếp theo, sẽ có một bài **challenge** để bạn có thể thực hành thêm kiến thức về việc sử dụng properties file trong Spring. Hẹn gặp lại bạn trong video tiếp theo!
