### Quản Lý Phụ Thuộc Trong Dự Án Maven Đa Module

Trong video này, chúng ta sẽ tìm hiểu cách quản lý các **phụ thuộc (dependencies)** trong dự án **Maven đa module**. Chúng ta sẽ thêm các phụ thuộc vào dự án đa module và cũng xem xét **các thuộc tính Maven** (Maven properties). Hãy cùng bắt đầu nhé.

#### Bước 1: Sao chép tệp logback.xml
Trước tiên, chúng ta sẽ cần sao chép tệp **logback.xml** từ dự án **hello Maven** trước đó. Nếu chưa mở dự án này, bạn có thể mở nó bằng cách vào **File > Open Recent** và chọn dự án **hello Maven**.

- Mở thư mục **resources** trong dự án **hello Maven**.
- Sao chép tệp **logback.xml** từ đó.
- Quay lại dự án **guess-the-number**.
- Mở thư mục **src/main/resources** và dán tệp **logback.xml** vào đó.

#### Bước 2: Quản lý phụ thuộc qua pom.xml của dự án cha
Việc quản lý các phụ thuộc chung cho toàn bộ các module con có thể trở nên cồng kềnh nếu bạn phải khai báo lại nhiều lần. Thay vì khai báo phụ thuộc trong từng module, chúng ta có thể quản lý chúng trong **pom.xml** của dự án cha bằng cách sử dụng thẻ **dependencyManagement**. Điều này cho phép các module con chỉ cần khai báo **group ID** và **artifact ID** mà không cần phải lặp lại các phiên bản hay cấu hình khác.

##### Ví dụ:
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>${logback.version}</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```
Trong đoạn trên, phiên bản của **logback** được khai báo thông qua một **thuộc tính Maven**.

#### Bước 3: Khai báo thuộc tính Maven
Khai báo thuộc tính giúp chúng ta dễ dàng quản lý các phiên bản phụ thuộc từ một nơi duy nhất. Để khai báo thuộc tính trong **pom.xml** của dự án cha, thêm thẻ **properties** dưới thẻ **packaging**:
```xml
<properties>
    <logback.version>1.2.3</logback.version>
</properties>
```
Bây giờ, chúng ta có thể sử dụng thuộc tính này ở bất cứ đâu trong **pom.xml** bằng cú pháp:
```xml
<version>${logback.version}</version>
```
Điều này giúp chúng ta dễ dàng cập nhật phiên bản cho tất cả các module chỉ bằng cách thay đổi một giá trị.

#### Bước 4: Thêm phụ thuộc cho Spring Context
Tiếp theo, chúng ta sẽ thêm phụ thuộc **Spring Context** từ kho **Maven Central**:
1. Truy cập trang **mvnrepository.com** và tìm kiếm **Spring Context**.
2. Chọn phiên bản mới nhất (ví dụ: 5.0.5) và sao chép mã phụ thuộc.
3. Dán mã phụ thuộc vào thẻ **dependencyManagement** trong **pom.xml** của dự án cha.

Ví dụ:
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>${spring.version}</version>
</dependency>
```

Đồng thời, bạn có thể thêm thuộc tính cho phiên bản Spring:
```xml
<properties>
    <spring.version>5.0.5.RELEASE</spring.version>
</properties>
```

#### Bước 5: Cấu hình Maven Compiler Plugin
Thêm plugin **Maven Compiler** vào **pom.xml** của dự án cha để tất cả các module có thể sử dụng cùng cấu hình biên dịch. Chúng ta sẽ thêm đoạn sau vào thẻ **build**:
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.7.0</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>
                <release>${java.version}</release>
            </configuration>
        </plugin>
    </plugins>
</build>
```
Bạn cũng cần khai báo phiên bản Java:
```xml
<properties>
    <java.version>10</java.version>
</properties>
```

#### Bước 6: Thêm phụ thuộc vào sub-module "core"
Trong **pom.xml** của module **core**, bạn không cần khai báo phiên bản của phụ thuộc vì chúng đã được quản lý trong dự án cha. Bạn chỉ cần khai báo **group ID** và **artifact ID**:
```xml
<dependencies>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
    </dependency>
</dependencies>
```

#### Bước 7: Kiểm tra dự án bằng lệnh Maven
Sau khi hoàn tất các cấu hình, hãy kiểm tra lại dự án bằng cách chạy các lệnh Maven:
1. Mở **Maven Projects**.
2. Chọn **guess-the-number-game** (root project).
3. Chạy lệnh **clean install**.

Điều này sẽ biên dịch toàn bộ dự án và các module con, kiểm tra xem có lỗi hay không.

#### Bước 8: Tạo mã kiểm tra logback
Cuối cùng, chúng ta sẽ kiểm tra xem cấu hình logback có hoạt động hay không bằng cách tạo một lớp **Main** trong module **core**:
```java
package academy.learnprogramming;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Main {
    private static final Logger log = LoggerFactory.getLogger(Main.class);

    public static void main(String[] args) {
        log.info("Guess the Number Game");
    }
}
```
Chạy chương trình và bạn sẽ thấy thông báo log được hiển thị theo định dạng mà bạn đã cấu hình trong **logback.xml**.

### Kết Luận
Chúng ta đã học cách quản lý phụ thuộc trong dự án Maven đa module bằng cách sử dụng **dependencyManagement** và **thuộc tính Maven**. Điều này giúp quản lý các phụ thuộc dễ dàng hơn và tránh việc lặp lại các cấu hình trong từng module. Chúng ta cũng đã kiểm tra hoạt động của cấu hình logback và đảm bảo rằng mọi thứ đều hoạt động đúng.
