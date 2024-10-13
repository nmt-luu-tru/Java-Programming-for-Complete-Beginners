Đây là phần giới thiệu về **Spring MVC**.

Chúng ta sẽ tìm hiểu về Spring MVC, cụ thể là nó là gì và hoạt động như thế nào. Spring Web MVC là một framework web gốc được xây dựng dựa trên **Servlet API** và đã xuất hiện từ khi Spring Framework được phát hành. Nó thường được biết đến với cái tên **Spring MVC**.

Spring MVC, giống như nhiều framework web khác, được thiết kế dựa trên **mẫu Front Controller**. Chúng ta sẽ nói thêm về điều này trong chốc lát. **MVC** là viết tắt của **Model, View, và Controller**, và đây là một mẫu thiết kế (design pattern). Mẫu thiết kế này chia ứng dụng thành ba phần chính để tách biệt phần đại diện thông tin bên trong khỏi cách thức thông tin được trình bày với người dùng.

### **Ba thành phần trong Spring MVC:**
1. **Model** (M trong MVC): 
   - Model chịu trách nhiệm quản lý dữ liệu, logic kinh doanh và quy tắc nghiệp vụ của ứng dụng.

2. **View** (V trong MVC): 
   - View là cách hiển thị thông tin ra bên ngoài, ví dụ như biểu mẫu web hoặc biểu đồ để trình bày thông tin cho người dùng.

3. **Controller** (C trong MVC): 
   - Controller chịu trách nhiệm gọi các model để thực hiện logic nghiệp vụ và sau đó cập nhật view dựa trên kết quả từ model.

### **Dispatcher Servlet trong Spring MVC:**
- Trong Spring MVC, chúng ta có một **central servlet** (servlet trung tâm) được gọi là **DispatcherServlet**. Servlet này cung cấp một thuật toán chung cho việc xử lý các yêu cầu.
- Công việc thực sự được thực hiện bởi các thành phần có thể được cấu hình, được gọi là **controllers** (bộ điều khiển) để xử lý các yêu cầu. Thiết kế này linh hoạt và hỗ trợ nhiều luồng công việc khác nhau.
- **DispatcherServlet** yêu cầu một **web application context** (ngữ cảnh ứng dụng web), một phần mở rộng của **plain application context** cho việc cấu hình của nó. DispatcherServlet chuyển giao công việc cho các **bean** đặc biệt để xử lý các yêu cầu và đưa ra các phản hồi phù hợp.

### **Tích hợp Spring MVC:**
- Với Spring MVC, chúng ta có thể sử dụng các công nghệ view khác nhau để hiển thị trang web, ví dụ như **Groovy Markup**, **FreeMarker**, **Thymeleaf**, v.v. Trong khóa học này, chúng ta sẽ sử dụng **Thymeleaf**.
- Spring MVC cũng tích hợp với các framework web khác, cho phép linh hoạt trong việc lựa chọn và kết hợp các công cụ để phát triển ứng dụng web.

### **Tóm tắt:**
Đây chỉ là phần giới thiệu ngắn gọn về Spring MVC và các thành phần của nó. Nếu có một số thuật ngữ khiến bạn cảm thấy khó hiểu, đừng lo lắng, vì trong các video tiếp theo, chúng ta sẽ đi vào chi tiết hơn từng phần. 

Hẹn gặp bạn trong video tiếp theo, nơi chúng ta sẽ bắt đầu tạo một ứng dụng mới trong IntelliJ để thực hành Spring MVC.
