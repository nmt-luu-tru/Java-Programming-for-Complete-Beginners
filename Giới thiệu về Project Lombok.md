Trong video này, chúng ta đã giới thiệu về **Project Lombok** và cách nó có thể giúp các nhà phát triển Spring viết mã gọn gàng hơn bằng cách tự động sinh ra mã lặp đi lặp lại (boilerplate code). Dưới đây là những điểm chính của Lombok:

### **Lợi ích của Lombok:**
- **Giảm bớt mã boilerplate**: Lombok tự động tạo ra các getter, setter, các phương thức `equals()`, `hashCode()`, và `toString()` mà không cần phải tự viết thủ công.
- **Giữ mã gọn gàng**: Mã nguồn trở nên sạch hơn, dễ đọc hơn, vì nhiều đoạn mã lặp không cần thiết được ẩn đi.
- **Năng suất tăng cao**: Giảm thời gian viết và duy trì các phương thức lặp đi lặp lại, cho phép bạn tập trung vào logic thực sự của ứng dụng.
  
### **Các Annotation Thông Dụng của Lombok:**
- **@Getter**: Tự động sinh ra getter cho các trường của lớp.
- **@Setter**: Tự động sinh ra setter cho các trường của lớp.
- **@ToString**: Sinh ra phương thức `toString()` cho lớp.
- **@EqualsAndHashCode**: Sinh ra các phương thức `equals()` và `hashCode()`.
- **@RequiredArgsConstructor**: Sinh ra constructor với các trường bắt buộc (trường có `final`).
- **@Slf4j**: Tạo ra một logger `Slf4j` cho lớp.
- **@Data**: Tổng hợp nhiều annotation như `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, và `@RequiredArgsConstructor` trong một annotation duy nhất.

### **Cách Lombok Hoạt Động:**
Lombok sử dụng **Annotation Processor API** để tự động tạo ra các phương thức khi dự án được biên dịch. Tại thời điểm chạy, mã đã được biên dịch có sự hiện diện của Lombok sẽ giống hệt như khi viết thủ công, nhưng mã nguồn ban đầu sẽ đơn giản và ngắn gọn hơn nhiều.

### **Ví dụ với Lombok:**
1. **Mã Java thông thường:**
   ```java
   public class Person {
       private String firstName;
       private String lastName;
       
       public String getFirstName() {
           return firstName;
       }
       
       public void setFirstName(String firstName) {
           this.firstName = firstName;
       }
       
       public String getLastName() {
           return lastName;
       }
       
       public void setLastName(String lastName) {
           this.lastName = lastName;
       }
   }
   ```
   **Với Lombok:**
   ```java
   @Getter @Setter
   public class Person {
       private String firstName;
       private String lastName;
   }
   ```
   Như bạn thấy, mã với Lombok ngắn gọn hơn rất nhiều.

### **Tích Hợp Lombok:**
Trong video tiếp theo, chúng ta sẽ thêm **Lombok dependency** vào dự án của mình và bắt đầu sử dụng Lombok. Điều này giúp làm rõ hơn cách Lombok có thể tối ưu hóa quá trình phát triển Java của bạn, đặc biệt là trong các dự án Spring lớn.

Lombok là một công cụ mạnh mẽ, giúp bạn tiết kiệm thời gian và công sức, đồng thời giúp mã nguồn dễ bảo trì và dễ đọc hơn.
