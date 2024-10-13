Thử thách của bạn là thiết lập chương trình với Maven và thêm các phụ thuộc cần thiết vào dự án của chúng ta.

### Cụ thể:
Bạn cần chỉnh sửa file `pom.xml` của dự án để thêm các phụ thuộc cho các artifact sau đây:
- **spring-web MVC**
- **Lombok**
- **logback-classic**
- **javax.annotation-api**

Sau đó, bạn cần thiết lập **Maven Compiler Plugin** giống như chúng ta đã làm ở dự án trước. Cuối cùng, sao chép file `logback.xml` từ dự án trước và dán nó vào dự án hiện tại trong thư mục `resources`.

Khi hoàn tất, hãy thực hiện các mệnh lệnh Maven **clean** và **install** để đảm bảo rằng mọi thứ hoạt động chính xác.

---

### Giải pháp:

Bây giờ, tôi sẽ hướng dẫn bạn từng bước thực hiện giải pháp cho thử thách này.

#### 1. **Thêm các thuộc tính Maven (Maven Properties):**
Trong file `pom.xml`, thêm các thuộc tính để quản lý các phiên bản của các phụ thuộc:

```xml
<properties>
    <java.version>10</java.version>
    <spring.version>5.3.9</spring.version>
    <logback.version>1.2.3</logback.version>
    <annotation-api.version>1.3.2</annotation-api.version>
</properties>
```

#### 2. **Thêm các phụ thuộc (Dependencies):**

Thêm các phần phụ thuộc vào dự án trong phần `<dependencies>`:

```xml
<dependencies>
    <!-- Spring MVC -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <!-- Lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.20</version>
        <scope>provided</scope>
    </dependency>

    <!-- Logback Classic -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>${logback.version}</version>
    </dependency>

    <!-- Javax Annotation API -->
    <dependency>
        <groupId>javax.annotation</groupId>
        <artifactId>javax.annotation-api</artifactId>
        <version>${annotation-api.version}</version>
    </dependency>
</dependencies>
```

#### 3. **Thêm Maven Compiler Plugin:**

Thêm plugin để biên dịch đúng với phiên bản Java bạn đang sử dụng:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

#### 4. **Sao chép file logback.xml:**

Sao chép file `logback.xml` từ dự án trước và dán nó vào thư mục `src/main/resources` của dự án hiện tại.

#### 5. **Chạy Maven Clean và Install:**

Sau khi thiết lập xong, bạn cần mở tab **Maven** trong IntelliJ và thực hiện lệnh **clean** và **install** để xây dựng dự án và kiểm tra xem mọi thứ đã hoạt động tốt chưa.

---

Sau khi hoàn tất các bước trên, dự án của bạn sẽ sẵn sàng và được cấu hình đúng để phát triển với Spring MVC. Hãy tiếp tục thử thách bản thân với các bước tiếp theo của dự án!
