### Hướng Dẫn Sửa Lỗi Khi Mở Dự Án Maven Trong IntelliJ IDEA

Trong video này, chúng ta sẽ học cách **tạo**, **build**, và **chạy** một dự án Maven trong **IntelliJ IDEA**, cùng với cách xử lý một số lỗi phổ biến khi mở dự án Maven từ các nguồn khác nhau hoặc khi tải xuống từ internet.

#### **Thách Thức: Mở Dự Án Maven Từ Một Vị Trí Khác hoặc Tải Xuống Từ Internet**

Khi bạn cố gắng mở một dự án Maven từ một vị trí khác trên máy tính hoặc từ một dự án đã được tải xuống từ internet, có thể bạn sẽ gặp phải một số lỗi. Điều này thường xảy ra do IntelliJ không tự động nhận diện và cấu hình đúng các phụ thuộc cũng như cấu trúc dự án Maven.

#### **Giải Pháp: Kích Hoạt Tự Động Nhập (Auto Import) hoặc Re-import Dự Án**

Dưới đây là các bước chi tiết để khắc phục lỗi khi mở dự án Maven trong IntelliJ:

### 1. **Tạo Một Dự Án Maven Mới Trong IntelliJ**

Trước tiên, chúng ta sẽ tạo một dự án Maven mới để làm quen với cấu trúc và cách hoạt động của Maven trong IntelliJ.

#### a. **Bắt Đầu Tạo Dự Án Mới:**
- Mở **IntelliJ IDEA**.
- Chọn **Create New Project** (Tạo Dự Án Mới).

#### b. **Chọn Maven:**
- Trong cửa sổ **New Project**, chọn **Maven** ở phía bên trái.
- Nhấn **Next** để tiếp tục.

#### c. **Chọn Archetype (Tùy chọn):**
- **Archetype** là một mẫu (template) giúp bạn tạo dự án Maven theo một định dạng nhất định, tiết kiệm thời gian so với việc tạo dự án thủ công.
- Ở thời điểm này, chúng ta không cần chọn archetype nào cả, vì vậy hãy bỏ qua và nhấn **Next**.

#### d. **Cài Đặt Project SDK:**
- Chọn **Project SDK**. Trong ví dụ này, **JDK 10** được chọn vì đó là phiên bản JDK mới nhất tại thời điểm ghi video.
- Đảm bảo bạn đã cài đặt JDK 10 hoặc phiên bản tương thích trên máy tính của mình.
- Nhấn **Next** để tiếp tục.

#### e. **Cấu Hình Thông Tin Dự Án:**
- **Group ID**: Đặt là `academy.learn.programming`.
  - Group ID là một cách duy nhất để xác định dự án của bạn trên toàn thế giới, tương tự như cách bạn đặt tên gói trong Java.
- **Artifact ID**: Đặt là `hello-maven`.
  - Artifact ID là tên duy nhất cho dự án của bạn trong Group ID đó.
- **Version**: Phiên bản mặc định được IntelliJ đặt là `1.0-SNAPSHOT`. Bạn có thể giữ nguyên hoặc thay đổi theo ý muốn.
  - **Lưu ý**: Nên tránh sử dụng ngày tháng ở cuối phiên bản vì thường chúng liên quan đến các build snapshot hoặc nightly, mà chúng ta sẽ thảo luận thêm trong các phần sau của khóa học.
- **Project Name**: Đặt là `hello-maven`.
- **Project Location**: Chọn nơi bạn muốn lưu trữ dự án trên máy tính của mình. IntelliJ sẽ tự động tạo một thư mục con cho dự án này.
- Nhấn **Finish** để hoàn tất quá trình tạo dự án.

### 2. **Cấu Trúc Dự Án Maven Điển Hình**

Khi mở dự án trong IntelliJ, bạn sẽ thấy cấu trúc thư mục như sau:

```
hello-maven
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── academy.learn.programming
    │   └── resources
    │       └── logback.xml
    └── test
        ├── java
        │   └── academy.learn.programming
        └── resources
```

- **pom.xml**: Tệp cấu hình chính của Maven, chứa thông tin về dự án và các phụ thuộc (dependencies).
- **src/main/java**: Chứa mã nguồn chính của dự án.
- **src/main/resources**: Chứa các tài nguyên như tệp cấu hình, hình ảnh.
- **src/main/webapp**: Chứa các tệp JSP và các mô tả triển khai cho ứng dụng web.
- **src/test**: Chứa mã kiểm thử (unit tests).
- **src/test/resources**: Chứa các tài nguyên cho kiểm thử.

### 3. **Thiết Lập Maven Compiler Plugin**

Maven Compiler Plugin cho phép bạn chỉ định phiên bản Java mà dự án sẽ biên dịch.

#### a. **Mở tệp `pom.xml`:**
- Trong cửa sổ **Project** bên trái, mở tệp `pom.xml`.

#### b. **Thêm Maven Compiler Plugin:**
- Thêm đoạn cấu hình sau vào phần `<build>` của `pom.xml` để sử dụng **Java 10**:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>10</source>
                <target>10</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

- **Giải thích**:
  - **source**: Phiên bản Java nguồn (Java 10).
  - **target**: Phiên bản Java mục tiêu (Java 10).

### 4. **Tạo Package và Lớp Chính (Main Class)**

#### a. **Tạo Package Mới:**
- Trong thư mục `src/main/java`, nhấp chuột phải và chọn **New > Package**.
- Đặt tên package là `academy.learn.programming`.

#### b. **Tạo Lớp Chính:**
- Nhấp chuột phải vào package `academy.learn.programming`, chọn **New > Java Class**.
- Đặt tên lớp là `HelloMaven`.
- Thêm phương thức `main` để in ra một thông điệp đơn giản:

```java
package academy.learn.programming;

public class HelloMaven {
    public static void main(String[] args) {
        System.out.println("Hello Maven");
    }
}
```

### 5. **Chạy Ứng Dụng Maven**

#### a. **Chạy Lớp Chính:**
- Trong cửa sổ **Project**, mở lớp `HelloMaven`.
- Nhấn vào **Green Arrow** bên cạnh phương thức `main` và chọn **Run 'HelloMaven.main()'**.
- Kết quả sẽ hiển thị ở phần **Run** phía dưới của IntelliJ:

```
Hello Maven
```

#### b. **Xử Lý Cảnh Báo:**
- Bạn có thể thấy một số cảnh báo liên quan đến phiên bản nguồn Java (source level) đang được sử dụng bởi Maven.
- Điều này xuất phát từ việc Maven cố gắng biên dịch mã với phiên bản Java mặc định là **1.5**, trong khi chúng ta đã thiết lập Maven Compiler Plugin để sử dụng **Java 10**.
- Để khắc phục, hãy đảm bảo rằng cấu hình Maven Compiler Plugin đã được thêm chính xác như đã hướng dẫn ở bước 3.

### 6. **Kiểm Tra Cấu Hình JDK Trong IntelliJ**

#### a. **Mở Cài Đặt Module:**
- Nhấp chuột phải vào dự án, chọn **Open Module Settings**.

#### b. **Đặt Phiên Bản JDK:**
- Trong tab **Project**, đảm bảo rằng **Project SDK** được đặt là **Java 10**.
- Trong **Project language level**, chọn **10** để phù hợp với cấu hình trong `pom.xml`.
- Nhấn **OK** để lưu các thay đổi.

#### c. **Chạy Lại Ứng Dụng:**
- Sau khi thay đổi phiên bản JDK, chạy lại lớp `HelloMaven` để đảm bảo rằng các cảnh báo đã được giải quyết và ứng dụng chạy thành công mà không gặp lỗi.

### 7. **Sao Chép Dự Án Maven Từ Một Vị Trí Khác hoặc Tải Xuống Từ Internet**

Khi bạn mở một dự án Maven từ một thư mục khác hoặc tải xuống từ internet, có thể bạn sẽ gặp lỗi do IntelliJ không tự động cấu hình các phụ thuộc và cấu trúc dự án đúng cách. Dưới đây là cách khắc phục:

#### a. **Kích Hoạt Tự Động Nhập (Auto Import):**
- Khi IntelliJ thông báo rằng dự án Maven cần được nhập lại, hãy chọn **Enable Auto Import** nếu tùy chọn này xuất hiện.
- Điều này sẽ giúp IntelliJ tự động tải xuống các phụ thuộc và cấu hình dự án dựa trên tệp `pom.xml`.

#### b. **Re-import Dự Án Maven:**
- Nếu tùy chọn **Enable Auto Import** không xuất hiện hoặc không khắc phục được lỗi, bạn có thể thực hiện **Re-import** dự án Maven thủ công:
  - Nhấp chuột phải vào tên dự án trong cửa sổ **Project**.
  - Chọn **Maven > Reimport**.
  - Maven sẽ tự động tải xuống các phụ thuộc và thiết lập dự án theo cấu hình trong `pom.xml`.

#### c. **Kiểm Tra và Sửa Lỗi:**
- Sau khi kích hoạt auto import hoặc re-import, kiểm tra lại cửa sổ **Run** để đảm bảo rằng dự án đã được build và chạy thành công.
- Nếu vẫn còn lỗi, hãy kiểm tra lại cấu hình JDK và các thiết lập Maven trong IntelliJ như đã hướng dẫn ở các bước trước.

### 8. **Kết Luận**

Bằng cách làm theo các bước trên, bạn đã:

- Tạo thành công một dự án Maven mới trong IntelliJ IDEA.
- Thiết lập cấu hình Maven Compiler Plugin để sử dụng Java 10.
- Tạo một lớp Java đơn giản để in ra thông điệp "Hello Maven".
- Chạy ứng dụng Maven và xử lý các cảnh báo liên quan đến phiên bản Java.
- Học cách khắc phục lỗi khi mở dự án Maven từ các vị trí khác hoặc từ internet bằng cách kích hoạt auto import hoặc re-import dự án.

### **Video Tiếp Theo:**
Trong video tiếp theo, chúng ta sẽ bắt đầu **thiết lập các plugin web** để tạo ứng dụng web với Spring MVC. Hãy chuẩn bị để tiếp tục hành trình học Spring MVC!
