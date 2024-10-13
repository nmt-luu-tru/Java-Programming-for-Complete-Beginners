### Khởi Tạo và Cấu Hình Logback Bằng XML

Trong video này, chúng ta sẽ học về các bước khởi tạo **Logback** và cách cấu hình Logback bằng tệp XML. Đây là cách phổ biến để quản lý log trong các dự án Java thông qua thư viện Logback.

#### 1. **Tại sao phải loại bỏ thẻ Scope trong `pom.xml`?**
Trước khi bắt đầu cấu hình Logback, chúng ta cần lưu ý về thẻ **scope** mà chúng ta đã loại bỏ khỏi tệp `pom.xml`. Thẻ **scope** được sử dụng để chỉ định rằng một dependency chỉ nên được sử dụng cho các lớp kiểm thử. Nếu bạn thêm dependency **logback** với scope là **test**, điều đó có nghĩa là Logback chỉ có thể được sử dụng trong các lớp kiểm thử, chứ không phải trong mã chính. Vì vậy, chúng ta cần loại bỏ thẻ **scope** này để Logback có thể hoạt động trong toàn bộ mã nguồn của dự án.

#### 2. **Khởi tạo Logback**
Khi ứng dụng Java của bạn chạy, Logback sẽ tìm kiếm tệp cấu hình theo thứ tự sau:
1. `logback-test.xml` trong classpath.
2. `logback.groovy` trong classpath.
3. `logback.xml` trong classpath.
4. Nếu không tìm thấy các tệp trên, Logback sẽ sử dụng cấu hình cơ bản (basic configuration) và ghi log ra **console**.

Nếu bạn không tạo tệp cấu hình, Logback sẽ tự động sử dụng cấu hình tối thiểu, và điều này lý giải vì sao ứng dụng của bạn vẫn ghi log mà không cần cấu hình gì thêm.

#### 3. **Các thành phần chính của Logback**
Logback bao gồm ba thành phần chính:
- **Logger**: Bắt và lưu thông tin log.
- **Appender**: Chuyển tiếp thông tin log đến các đích khác nhau như console, file, cơ sở dữ liệu, v.v.
- **Layout**: Định dạng thông tin log, tức là làm sao để các log hiển thị theo mẫu nhất định.

#### 4. **Cấu hình Logback với XML**
Chúng ta sẽ tạo một tệp cấu hình **logback.xml** để điều chỉnh cách Logback ghi log trong ứng dụng. Ví dụ cấu hình cơ bản của **logback.xml** như sau:

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%date [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <logger name="com.example" level="DEBUG" />

    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

##### Giải thích:
1. **Appender**: Được đặt tên là `STDOUT` và dùng để ghi log ra console. Dòng này sử dụng `ConsoleAppender` từ thư viện Logback để ghi log ra màn hình.
2. **Pattern**: Mẫu định dạng log được chỉ định bởi thẻ `<pattern>`. Mẫu này bao gồm các thành phần như `%date` (ngày giờ), `%thread` (tên luồng), `%level` (mức độ log), `%logger` (tên logger) và `%msg` (thông điệp log).
3. **Logger**: Được định nghĩa cho package `com.example` với mức độ log là `DEBUG`.
4. **Root Logger**: Đây là logger gốc của hệ thống, với mức log là `INFO` và sử dụng appender `STDOUT`.

#### 5. **Thực thi và kiểm tra log**
Sau khi đã tạo tệp cấu hình **logback.xml**, hãy chạy lại chương trình để kiểm tra kết quả. Kết quả log sẽ hiển thị trên console theo đúng mẫu đã cấu hình trong tệp XML.

Ví dụ kết quả log:
```
2024-10-13 15:30:01 [main] INFO  com.example - Hello, Info Log
2024-10-13 15:30:01 [main] DEBUG com.example - Hello, Debug Log
```

Trong ví dụ trên:
- `2024-10-13 15:30:01`: Thời gian log.
- `[main]`: Tên luồng thực thi.
- `INFO` hoặc `DEBUG`: Mức độ log.
- `com.example`: Tên logger.
- `Hello, Info Log`: Nội dung thông điệp log.

#### 6. **Tùy chỉnh cấu hình log**
Bạn có thể dễ dàng tùy chỉnh cách Logback ghi log bằng cách thay đổi mẫu định dạng (`pattern`) hoặc thêm các logger và appender khác nhau để ghi log vào nhiều đích đến khác nhau như file hoặc cơ sở dữ liệu.

Ví dụ, nếu bạn muốn ghi log vào file, bạn có thể thêm một **FileAppender**:
```xml
<appender name="FILE" class="ch.qos.logback.core.FileAppender">
    <file>app.log</file>
    <encoder>
        <pattern>%date [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
</appender>

<root level="INFO">
    <appender-ref ref="FILE" />
</root>
```

#### Kết luận:
Cấu hình Logback cho phép bạn kiểm soát chi tiết về cách ghi log và nơi ghi log. Bạn có thể dễ dàng tạo các file cấu hình để theo dõi hoạt động của ứng dụng và xử lý các sự kiện quan trọng. Trong các phần tiếp theo của khóa học, chúng ta sẽ học cách ghi log vào file và quản lý nhiều logger khác nhau trong hệ thống.
