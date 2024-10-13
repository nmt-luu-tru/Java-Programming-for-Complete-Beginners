Trong video này, chúng ta đã thảo luận về cách cài đặt và cấu hình **Project Lombok** trong IntelliJ IDEA cũng như cách bắt đầu sử dụng nó trong một dự án Java dựa trên Spring. Dưới đây là tóm tắt các bước và chi tiết:

### **Các bước thực hiện: Cài đặt Lombok trong IntelliJ IDEA**

#### 1. **Cài đặt Plugin Lombok trong IntelliJ IDEA:**
   - Mở **IntelliJ** và vào:
     - **File > Settings** (hoặc **IntelliJ > Preferences** trên macOS).
   - Điều hướng đến **Plugins** và tìm "Lombok."
   - Nhấp **Install** bên cạnh plugin Lombok.
   - Sau khi cài đặt, **khởi động lại IntelliJ** để kích hoạt plugin.

#### 2. **Kích hoạt Annotation Processing:**
   - Vào **File > Settings** (hoặc **Preferences**).
   - Điều hướng đến **Build, Execution, Deployment > Compiler > Annotation Processors**.
   - Tích chọn **Enable annotation processing**.
   - Đảm bảo rằng **Obtain processors from project classpath** đã được chọn.

#### 3. **Thêm dependency của Lombok:**
   - **Nếu bạn sử dụng Maven**, bạn có thể thêm dependency Lombok trực tiếp từ Maven. Nếu bạn cần phiên bản mới nhất hoặc phiên bản tùy chỉnh (như chúng ta đã làm trong video này do tương thích với JDK), thực hiện các bước sau:
     - Truy cập **https://projectlombok.org/download** để tải về phiên bản mới nhất nếu cần (cho JDK 10+).
     - Tạo một thư mục `libs` trong dự án của bạn và đặt tệp Lombok `.jar` vào đó nếu bạn sử dụng bản sao cục bộ.
   - **Thêm dependency** vào **`pom.xml`** cho các dự án Maven:
     ```xml
     <dependency>
         <groupId>org.projectlombok</groupId>
         <artifactId>lombok</artifactId>
         <version>${lombok.version}</version>
         <scope>provided</scope>
     </dependency>
     ```
     Bạn có thể đặt `${lombok.version}` là `1.16.21` hoặc bất kỳ phiên bản nào bạn đang sử dụng.

   - Nếu bạn sử dụng tệp `.jar` cục bộ:
     ```xml
     <dependency>
         <groupId>org.projectlombok</groupId>
         <artifactId>lombok</artifactId>
         <version>${lombok.version}</version>
         <scope>system</scope>
         <systemPath>${basedir}/libs/lombok-edge.jar</systemPath>
     </dependency>
     ```

#### 4. **Kiểm tra Lombok hoạt động:**
   - Trong mã, bây giờ bạn có thể sử dụng các annotation của Lombok như `@Getter`, `@Setter`, và `@Slf4j`.
   - Ví dụ, trong lớp **Main**, thêm:
     ```java
     @Slf4j
     public class Main {
         public static void main(String[] args) {
             log.info("Ứng dụng đã khởi động");
         }
     }
     ```
   - Với annotation `@Slf4j`, Lombok sẽ tự động tạo trường `log` cho bạn. Trường này không hiện diện trong mã nguồn, nhưng tại thời điểm biên dịch, nó có và hoạt động.
   - **Biên dịch và chạy** dự án để kiểm tra chức năng của Lombok. Bạn sẽ thấy logger hoạt động mà không cần định nghĩa thủ công.

### **Lợi ích của Lombok trong Java:**
   - **Loại bỏ mã lặp lại**: Các annotation của Lombok thay thế việc viết thủ công các phương thức getter, setter, constructor, logger, v.v.
   - **Mã sạch và dễ bảo trì hơn**: Có ít dòng mã hơn để xử lý các phần lặp lại.
   - **Nhất quán**: Bạn không cần lo lắng về việc duy trì các phương thức thường dùng như `toString()`, `equals()`, v.v.
   - **Tiết kiệm thời gian**: Nhanh chóng triển khai logging, constructor, và các tính năng khác chỉ với một annotation.

### **Bước tiếp theo:**
   - Trong video tiếp theo, chúng ta sẽ khám phá thêm các annotation và tính năng khác của Lombok như `@Data`, `@RequiredArgsConstructor`, và nhiều hơn nữa.
   - Chúng ta sẽ bắt đầu tích hợp những annotation này vào các lớp của chúng ta để thấy cách Lombok đơn giản hóa mã hơn nữa.

Đây mới chỉ là phần khởi đầu của việc sử dụng Lombok hiệu quả. Với Lombok, bạn có thể tối ưu hóa dự án Spring và tập trung vào các phần phức tạp hơn mà không cần bận tâm đến việc sinh mã lặp lại.
