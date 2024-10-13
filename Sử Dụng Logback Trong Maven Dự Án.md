### Hướng Dẫn Sử Dụng Logback Trong Maven Dự Án

Trong video này, chúng ta sẽ tìm hiểu cách sử dụng **Logback** trong dự án Maven, từ việc thêm **Logback** và **SLF4J** vào dự án, cho đến cách tải xuống mã nguồn và tài liệu liên quan để sử dụng **Logback** một cách hiệu quả.

#### **1. Tìm Kiếm Và Thêm Logback Dependency Trong Maven**
Để thêm dependency cho Logback vào dự án Maven, chúng ta cần tìm nó trên **Maven Central Repository**. Cụ thể, chúng ta sẽ thêm **SLF4J API** và **Logback Classic**.

Các bước thực hiện:
1. Truy cập trang web [mvnrepository.com](https://mvnrepository.com).
2. Tìm kiếm từ khóa **Logback**.
3. Chọn phiên bản **Logback Classic** mới nhất (tại thời điểm ghi hình là 1.2.3).
4. Sao chép đoạn mã dependency từ trang web và dán vào tệp `pom.xml` của dự án Maven dưới phần `<dependencies>`.

Ví dụ về cấu trúc dependency cho Logback Classic:
```xml
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
</dependency>
```

#### **2. Cập Nhật Dự Án Maven**
Sau khi thêm dependency vào tệp `pom.xml`, bạn cần cập nhật lại dự án để IntelliJ tự động tải và thêm các thư viện cần thiết:
1. Mở tab **Maven Projects** ở phía bên phải của IntelliJ.
2. Nhấn vào nút **Reload All Maven Projects** hoặc nhấn phải vào dự án và chọn **Reimport**.

Kết quả là các thư viện **logback-core** và **slf4j-api** sẽ được tải xuống và thêm vào dự án.

#### **3. Kiểm Tra Các Dependency**
Sau khi thêm và cập nhật thành công, bạn có thể kiểm tra các dependency trong dự án:
- Mở phần **External Libraries** trong IntelliJ để xem các thư viện đã được thêm vào.
- Bạn cũng có thể nhấn đúp vào **Install** trong tab **Maven Projects** để chạy build và đảm bảo tất cả các thư viện cần thiết đã được tải xuống thành công.

#### **4. Thêm Logging Vào Mã Nguồn Java**
Bây giờ chúng ta sẽ sử dụng **SLF4J** để tạo logger trong mã Java. Thêm logger vào lớp **HelloMaven** như sau:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloMaven {
    private static final Logger log = LoggerFactory.getLogger(HelloMaven.class);

    public static void main(String[] args) {
        log.info("Hello, Info Log");
        log.debug("Hello, Debug Log");
    }
}
```

##### Giải Thích:
- **LoggerFactory.getLogger()**: Tạo logger cho lớp `HelloMaven`.
- **log.info()**: Ghi log ở mức **INFO**.
- **log.debug()**: Ghi log ở mức **DEBUG**.

#### **5. Chạy Dự Án Và Kiểm Tra Kết Quả**
Chạy ứng dụng bằng cách nhấn vào nút **Run** trong IntelliJ. Kết quả sẽ hiển thị thông tin log trên console với các thông tin chi tiết như thời gian chạy và mức độ log (INFO, DEBUG).

Ví dụ đầu ra:
```
2024-10-13 15:30:01 [main] INFO HelloMaven - Hello, Info Log
2024-10-13 15:30:01 [main] DEBUG HelloMaven - Hello, Debug Log
```

#### **6. Tải Xuống Mã Nguồn Và Tài Liệu**
Trong IntelliJ, bạn có thể tải xuống mã nguồn và tài liệu của các thư viện bằng cách:
1. Nhấn vào biểu tượng **Download** ở phần **Maven Projects**.
2. Chọn **Download Sources and Documentation**.

#### **Kết Luận**
Chúng ta đã học cách tích hợp Logback vào dự án Maven và sử dụng SLF4J API để thực hiện logging. Việc sử dụng các thư viện như SLF4J và Logback giúp ghi lại log một cách linh hoạt và mạnh mẽ, đồng thời dễ dàng cấu hình và mở rộng. Trong các phần tiếp theo, chúng ta sẽ tiếp tục tìm hiểu cách cấu hình nâng cao cho Logback và sử dụng logging trong các dự án thực tế.
