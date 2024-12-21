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

---

Trong Spring, nếu bạn không tự tạo file `properties`, thì **Spring Boot** sẽ sử dụng các file cấu hình mặc định mà bạn không cần phải tạo file `properties` riêng. Các file này có thể là:

- **`application.properties`** hoặc **`application.yml`** trong thư mục `src/main/resources`.
  
Cấu trúc của các file này tương tự như sau:

```properties
# application.properties
game.maxNumber=100
game.guessCount=10
```

Hoặc trong định dạng YAML:

```yaml
# application.yml
game:
  maxNumber: 100
  guessCount: 10
```

### **Trường hợp không cần `@PropertySource`**
Trong Spring Boot, nếu bạn sử dụng **`application.properties`** hoặc **`application.yml`**, bạn không cần phải dùng annotation `@PropertySource` vì Spring Boot tự động tải các file này từ thư mục `resources`. Spring Boot sẽ tự động tìm và nạp các cấu hình từ các file này khi khởi tạo ứng dụng.

### **Khi nào cần `@PropertySource`?**
Annotation `@PropertySource` chỉ cần thiết trong những trường hợp bạn sử dụng file properties khác ngoài **`application.properties`** hoặc **`application.yml`** mà bạn muốn Spring nạp vào ứng dụng. Ví dụ, nếu bạn có một file `game.properties` nằm trong thư mục `resources/config`, bạn cần phải khai báo `@PropertySource` để Spring biết đường dẫn đến file đó.

Ví dụ:
```java
@Configuration
@PropertySource("classpath:config/game.properties")
public class GameConfig {
    // Cấu hình và thuộc tính khác
}
```
---

Khi bạn sử dụng annotation `@PropertySource` để chỉ định một file properties cụ thể, **file `application.properties` hoặc `application.yml` mặc định** của Spring Boot **vẫn sẽ được sử dụng**, và bạn không cần phải lo lắng về việc chúng bị ghi đè hay bị bỏ qua.

### Cách hoạt động:

1. **`@PropertySource`** chỉ định **các file properties ngoài `application.properties` hoặc `application.yml` mặc định** mà bạn muốn Spring nạp vào.
   
2. **File `application.properties` hoặc `application.yml` mặc định** sẽ vẫn được Spring Boot tự động nạp vào. Do đó, khi bạn sử dụng annotation `@Value` để tiêm giá trị, Spring sẽ tìm kiếm trong **cả file `application.properties` (hoặc `application.yml`) và các file properties được chỉ định qua `@PropertySource`**.

### Ví dụ:

Giả sử bạn có cấu trúc như sau:

- **`application.properties`**:

```properties
# application.properties
game.maxNumber=50
game.guessCount=15
```

- **`game.properties`** (được chỉ định qua `@PropertySource`):

```properties
# game.properties
game.maxNumber=100
game.guessCount=10
```

Và trong lớp cấu hình **GameConfig** của bạn, bạn sử dụng `@PropertySource`:

```java
@Configuration
@PropertySource("classpath:config/game.properties")
public class GameConfig {
    
    @Value("${game.maxNumber}")
    private int maxNumber;

    @Value("${game.guessCount}")
    private int guessCount;

    @PostConstruct
    public void printConfig() {
        System.out.println("Max Number: " + maxNumber);
        System.out.println("Guess Count: " + guessCount);
    }
}
```

Kết quả:

- **`game.maxNumber`** sẽ có giá trị **100** từ `game.properties` (vì `game.properties` được nạp trước).
- **`game.guessCount`** sẽ có giá trị **10** từ `game.properties`.

Tuy nhiên, **nếu giá trị không có trong `game.properties`**, Spring sẽ tiếp tục tìm trong **`application.properties`** (hoặc `application.yml`), và nếu tìm thấy, nó sẽ tiêm giá trị đó.

### Cách tìm kiếm giá trị:

1. **Ưu tiên đầu tiên**: File properties được chỉ định qua `@PropertySource` (ví dụ: `game.properties` trong trường hợp trên).
2. **Ưu tiên thứ hai**: File `application.properties` hoặc `application.yml` mặc định của Spring Boot.

### Kết luận:

- **File `application.properties` hoặc `application.yml`** vẫn được Spring Boot sử dụng mặc định và **không bị ảnh hưởng** khi bạn sử dụng `@PropertySource` để nạp thêm các file cấu hình khác.
- **`@Value`** sẽ tiêm giá trị từ **cả file mặc định và các file được chỉ định qua `@PropertySource`**, và ưu tiên nạp từ file được chỉ định trước (nếu có giá trị trong đó).

---

Có, trong Spring, bạn **hoàn toàn có thể nạp cùng lúc nhiều file properties**. Bạn có thể sử dụng nhiều annotation `@PropertySource` để chỉ định các file cấu hình khác nhau mà bạn muốn Spring nạp vào ứng dụng.

### Cách làm:

Spring cho phép bạn chỉ định **nhiều file properties** bằng cách sử dụng **nhiều `@PropertySource`** hoặc kết hợp chúng trong một danh sách. Điều này rất hữu ích nếu bạn muốn tách biệt cấu hình cho các môi trường khác nhau hoặc cho các phần riêng biệt của ứng dụng.

### Cách sử dụng `@PropertySource` với nhiều file

#### 1. **Sử dụng nhiều annotation `@PropertySource`**

Bạn có thể thêm nhiều `@PropertySource` trong cùng một lớp cấu hình. Mỗi annotation sẽ chỉ định một file cấu hình cần nạp.

Ví dụ:

```java
@Configuration
@PropertySource("classpath:config/game.properties")
@PropertySource("classpath:config/database.properties")
public class GameConfig {
    // Các cấu hình khác
}
```

Trong ví dụ trên, cả **`game.properties`** và **`database.properties`** đều được nạp vào Spring.

#### 2. **Sử dụng `@PropertySource` với một danh sách các file**

Nếu bạn muốn chỉ định nhiều file trong cùng một annotation, bạn có thể sử dụng cú pháp sau:

```java
@Configuration
@PropertySource({"classpath:config/game.properties", "classpath:config/database.properties"})
public class GameConfig {
    // Các cấu hình khác
}
```

Cả hai file `game.properties` và `database.properties` sẽ được nạp cùng lúc.

### Lưu ý khi sử dụng nhiều file properties:

1. **Ưu tiên nạp các file**: Nếu có sự trùng lặp về key (ví dụ, cả hai file đều chứa cấu hình `game.maxNumber`), Spring sẽ sử dụng giá trị từ file nạp sau. Nói cách khác, **file được nạp sau cùng sẽ ghi đè giá trị của các file trước đó** nếu chúng có cùng key.
   
2. **Lỗi trùng lặp**: Nếu có trùng lặp các key mà bạn không muốn bị ghi đè, hãy chắc chắn rằng các file properties của bạn không có sự chồng chéo nhau về tên key. Điều này giúp tránh các lỗi không mong muốn khi cấu hình bị ghi đè ngoài ý muốn.

3. **Đường dẫn chính xác**: Đảm bảo rằng các đường dẫn đến các file properties phải chính xác. Nếu sử dụng `classpath:`, Spring sẽ tìm các file đó trong thư mục `resources` của dự án.

### Ví dụ thực tế:

Giả sử bạn có 3 file cấu hình:

- **`game.properties`**: 

```properties
game.maxNumber=100
game.guessCount=10
```

- **`database.properties`**:

```properties
db.url=jdbc:mysql://localhost:3306/mydb
db.username=root
```

- **`application.properties`** (mặc định của Spring Boot):

```properties
server.port=8080
```

Trong **`GameConfig.java`**:

```java
@Configuration
@PropertySource({"classpath:config/game.properties", "classpath:config/database.properties"})
public class GameConfig {

    @Value("${game.maxNumber}")
    private int maxNumber;

    @Value("${db.url}")
    private String dbUrl;

    @PostConstruct
    public void printConfig() {
        System.out.println("Max Number: " + maxNumber);
        System.out.println("DB URL: " + dbUrl);
    }
}
```

### Kết quả:

- Giá trị `game.maxNumber` sẽ được nạp từ `game.properties`.
- Giá trị `db.url` sẽ được nạp từ `database.properties`.
- Các cấu hình mặc định như `server.port` sẽ được nạp từ `application.properties` mà không cần chỉ định rõ.

### Tóm tắt:

- Bạn có thể nạp **nhiều file properties** cùng lúc bằng cách sử dụng **nhiều `@PropertySource`** hoặc chỉ định chúng trong một danh sách.
- Nếu các file properties chứa các key trùng lặp, giá trị từ file sau cùng sẽ ghi đè giá trị từ các file trước.
- Việc tách biệt cấu hình giúp quản lý ứng dụng trở nên dễ dàng và linh hoạt hơn, đặc biệt trong các môi trường phát triển, kiểm thử và sản xuất.

