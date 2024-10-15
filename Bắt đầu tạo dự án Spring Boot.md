Trong video này, chúng ta sẽ bắt đầu với việc **tạo một dự án Spring Boot đơn giản**.

### **Bắt đầu tạo dự án Spring Boot**
- Cách dễ nhất để tạo dự án Spring Boot là sử dụng **Spring Initializr**: [start.spring.io](https://start.spring.io).
- Khi truy cập, hãy chọn **các giá trị mặc định**: Maven, Java, và **phiên bản mới nhất của Spring Boot**.
- **Lưu ý**: Tránh các phiên bản **SNAPSHOT** hoặc **milestone** (được đánh dấu bằng M1, M2, M3).

### **Cấu hình dự án**
- **Group ID**: Đây là tên nhóm của dự án. Ví dụ: `com.in28minutes`.
- **Artifact ID**: Đây là tên dự án. Ví dụ: `learn-spring-boot`.
- **Thêm Dependency**: Tìm và chọn **Spring Web** để xây dựng ứng dụng REST API. Spring Web sẽ giúp xây dựng ứng dụng với **Spring MVC** và chạy trên **Tomcat**.

### **Tải về và cấu hình dự án**
- Nhấn vào **GENERATE** để tải về file zip của dự án.
- **Giải nén** và di chuyển thư mục đã giải nén vào một thư mục trên máy tính.
- Mở **Eclipse** và chọn **File -> Import -> Existing Maven Projects**.
- Chọn thư mục dự án đã giải nén và nhấn **Finish** để hoàn thành việc nhập dự án.

### **Cấu trúc thư mục**
- **src/main/java**: Nơi bạn sẽ viết mã Java của mình.
- **src/main/resources**: Nơi chứa các file cấu hình.
- **src/test/java**: Nơi viết các bài kiểm tra đơn vị (unit test).

### **Chạy ứng dụng Spring Boot**
- **Mở class `LearnSpringBootApplication`** trong **src/main/java**.
- Nhấn chuột phải và chọn **Run As -> Java Application** để khởi chạy ứng dụng.
- **Spring Boot** sẽ mất một chút thời gian để khởi chạy lần đầu tiên.

### **Kết quả**
- **Chúc mừng!** Bạn đã tạo và khởi chạy thành công ứng dụng Spring Boot đơn giản.
- Trong các bước tiếp theo, chúng ta sẽ xây dựng các chức năng khác để hiểu sâu hơn về **Spring Boot framework**.

Hẹn gặp lại bạn ở các bước tiếp theo để tiếp tục hành trình với Spring Boot!
