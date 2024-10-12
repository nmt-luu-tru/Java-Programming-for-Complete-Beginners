### Hướng Dẫn Về Maven Lifecycle, Plugins và Goals

Trong video này, chúng ta sẽ học về **Maven Lifecycle**, **Maven Plugins** và **Maven Goals**. Đây là những khái niệm cơ bản nhưng rất quan trọng để hiểu cách Maven quản lý quá trình xây dựng và triển khai dự án phần mềm của bạn.

#### **1. Maven Lifecycle Là Gì?**

**Maven Lifecycle** là một khái niệm cốt lõi trong Maven, định nghĩa rõ ràng quá trình xây dựng và phân phối một artifact hoặc dự án phần mềm. Điều này có nghĩa là với Maven, quá trình build được chia thành các giai đoạn (phases) cụ thể, giúp nhà phát triển chỉ cần học một tập hợp nhỏ các lệnh để xây dựng bất kỳ dự án Maven nào, và tệp `pom.xml` sẽ đảm bảo rằng bạn nhận được kết quả mong muốn.

##### **Các Lifecycle Chính trong Maven:**
Maven có **ba lifecycle** tích hợp sẵn:
1. **default**: Xử lý việc triển khai dự án.
2. **clean**: Xử lý việc dọn dẹp dự án.
3. **site**: Xử lý việc tạo tài liệu trang web của dự án.

Mỗi lifecycle này được xác định bởi một danh sách các **build phases** khác nhau, mỗi phase đại diện cho một giai đoạn trong quá trình build.

##### **Các Phases Chính trong Default Lifecycle:**
Dưới đây là một số phase chính trong **default lifecycle**:
- **validate**: Kiểm tra xem dự án có đúng cấu trúc và thông tin cần thiết không.
- **compile**: Biên dịch mã nguồn của dự án.
- **test**: Chạy các bài kiểm thử đơn vị.
- **package**: Đóng gói ứng dụng vào định dạng phân phối, ví dụ như JAR hoặc WAR.
- **verify**: Kiểm tra các kết quả build để đảm bảo chất lượng.
- **install**: Cài đặt artifact vào kho lưu trữ cục bộ để sử dụng trong các dự án khác.
- **deploy**: Triển khai artifact lên kho lưu trữ từ xa để chia sẻ với các nhà phát triển khác.

#### **2. Maven Plugins Là Gì?**

**Maven Plugins** là các thành phần mở rộng cho Maven, cung cấp các chức năng bổ sung để thực hiện các nhiệm vụ cụ thể trong quá trình build. Thực chất, Maven chỉ là một framework lõi, và các plugin là nơi chứa phần lớn các hành động thực tế như tạo tệp JAR, WAR, biên dịch mã, chạy kiểm thử đơn vị, và tạo tài liệu dự án.

##### **Các Loại Maven Plugins:**
- **Build Plugins**: Được thực thi trong quá trình build và cấu hình trong phần `<build>` của tệp `pom.xml`. Ví dụ:
  - **maven-compiler-plugin**: Biên dịch mã nguồn Java.
  - **maven-jar-plugin**: Tạo tệp JAR từ mã nguồn đã biên dịch.
- **Reporting Plugins**: Được thực thi trong quá trình tạo tài liệu trang web và cấu hình trong phần `<reporting>` của tệp `pom.xml`. Ví dụ:
  - **maven-site-plugin**: Tạo trang web tài liệu cho dự án.

##### **Cách Thêm Plugin Vào Dự Án Maven:**
Để thêm một plugin vào dự án Maven, bạn cần cấu hình nó trong tệp `pom.xml` của bạn. Dưới đây là ví dụ về cách thêm **maven-compiler-plugin**:

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

#### **3. Maven Goals Là Gì?**

**Maven Goals** là các hành động cụ thể mà một plugin có thể thực hiện. Mỗi plugin có thể có một hoặc nhiều goals, mỗi goal tương ứng với một chức năng nhất định. Ví dụ, **maven-compiler-plugin** có hai goals chính:
- **compile**: Biên dịch mã nguồn chính của dự án.
- **testCompile**: Biên dịch mã nguồn kiểm thử của dự án.

##### **Cách Sử Dụng Goals:**
Bạn có thể thực thi các goals của một plugin bằng cách sử dụng lệnh Maven trong terminal. Ví dụ, để biên dịch dự án, bạn có thể sử dụng lệnh:

```bash
mvn compile
```

Để chạy kiểm thử đơn vị, bạn có thể sử dụng lệnh:

```bash
mvn test
```

#### **4. Thực Hành: Hiểu Rõ Maven Lifecycle và Plugins**

Bây giờ, hãy cùng nhau thực hành và hiểu rõ hơn về **Maven Lifecycle**, **Plugins**, và **Goals** thông qua dự án **hello-maven** mà chúng ta đã tạo trước đó.

##### **Bước 1: Tạo Dự Án Maven Mới trong IntelliJ IDEA**
- Mở IntelliJ IDEA.
- Chọn **Create New Project** > **Maven** > **Next**.
- Điền thông tin:
  - **Group ID**: `academy.learn.programming`
  - **Artifact ID**: `hello-maven`
  - **Version**: `1.0-SNAPSHOT` (giữ nguyên hoặc thay đổi theo ý bạn)
- Đặt tên và vị trí dự án, sau đó nhấn **Finish**.

##### **Bước 2: Cấu Hình Maven Compiler Plugin**
- Mở tệp `pom.xml`.
- Thêm cấu hình cho **maven-compiler-plugin** trong phần `<build>`:

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

##### **Bước 3: Tạo Lớp Chính (Main Class)**
- Trong thư mục `src/main/java/academy.learn.programming`, tạo một package mới.
- Tạo một lớp Java mới tên là `HelloMaven` và thêm phương thức `main`:

```java
package academy.learn.programming;

public class HelloMaven {
    public static void main(String[] args) {
        System.out.println("Hello Maven");
    }
}
```

##### **Bước 4: Build và Chạy Dự Án**
- Mở terminal trong IntelliJ IDEA hoặc sử dụng cửa sổ Maven Projects.
- Chạy lệnh build:

```bash
mvn clean install
```

- Sau khi build thành công, bạn có thể chạy lớp `HelloMaven` bằng cách nhấn vào **Green Arrow** bên cạnh phương thức `main` trong IntelliJ IDEA.
- Kết quả sẽ hiển thị trong cửa sổ **Run**:

```
Hello Maven
```

##### **Bước 5: Xử Lý Cảnh Báo về Phiên Bản Java**
- Nếu bạn thấy cảnh báo liên quan đến phiên bản nguồn Java (ví dụ: **source level 1.5 is obsolete**), đảm bảo rằng bạn đã cấu hình đúng **maven-compiler-plugin** như ở Bước 2.
- Kiểm tra lại cấu hình JDK trong IntelliJ IDEA:
  - Nhấp chuột phải vào dự án > **Open Module Settings**.
  - Trong tab **Project**, đảm bảo rằng **Project SDK** được đặt là **Java 10**.
  - Trong **Project language level**, chọn **10**.
  - Nhấn **OK** và chạy lại dự án nếu cần thiết.

#### **5. Khắc Phục Lỗi Khi Mở Dự Án Maven Từ Vị Trí Khác hoặc Tải Xuống Từ Internet**

Khi bạn cố gắng mở một dự án Maven từ một thư mục khác hoặc tải xuống từ internet, bạn có thể gặp lỗi do IntelliJ không tự động nhận diện và cấu hình đúng các phụ thuộc và cấu trúc dự án. Dưới đây là cách khắc phục:

##### **a. Kích Hoạt Tự Động Nhập (Auto Import):**
- Khi IntelliJ thông báo rằng dự án Maven cần được nhập lại, hãy chọn **Enable Auto Import** nếu tùy chọn này xuất hiện.
- Điều này sẽ giúp IntelliJ tự động tải xuống các phụ thuộc và cấu hình dự án dựa trên tệp `pom.xml`.

##### **b. Re-import Dự Án Maven Thủ Công:**
- Nếu tùy chọn **Enable Auto Import** không xuất hiện hoặc không khắc phục được lỗi, bạn có thể thực hiện **Re-import** dự án Maven thủ công:
  - Nhấp chuột phải vào tên dự án trong cửa sổ **Project**.
  - Chọn **Maven > Reimport**.
  - Maven sẽ tự động tải xuống các phụ thuộc và thiết lập dự án theo cấu hình trong `pom.xml`.

##### **c. Kiểm Tra và Sửa Lỗi:**
- Sau khi kích hoạt auto import hoặc re-import, kiểm tra lại cửa sổ **Run** để đảm bảo rằng dự án đã được build và chạy thành công.
- Nếu vẫn còn lỗi, hãy kiểm tra lại cấu hình JDK và các thiết lập Maven trong IntelliJ như đã hướng dẫn ở các bước trước.

#### **6. Kết Luận**

Trong video này, chúng ta đã:
- Tìm hiểu về **Maven Lifecycle**, **Plugins**, và **Goals**.
- Tạo và cấu hình một dự án Maven mới trong IntelliJ IDEA.
- Thêm và cấu hình **maven-compiler-plugin** để sử dụng Java 10.
- Tạo một lớp Java đơn giản để in ra thông điệp "Hello Maven".
- Xây dựng và chạy dự án Maven, đồng thời xử lý các cảnh báo liên quan đến phiên bản Java.
- Học cách khắc phục lỗi khi mở dự án Maven từ các vị trí khác hoặc từ internet bằng cách kích hoạt auto import hoặc re-import dự án.

### **Video Tiếp Theo:**
Trong video tiếp theo, chúng ta sẽ bắt đầu **thiết lập các plugin web** để tạo ứng dụng web với **Spring MVC**. Hãy chuẩn bị để tiếp tục hành trình học Spring MVC và Maven!
