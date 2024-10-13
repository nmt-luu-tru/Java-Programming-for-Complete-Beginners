Dòng mã này nằm trong lớp **`WebAppInitializer`**, và nhiệm vụ của nó là đăng ký **Dispatcher Servlet** với **`ServletContext`** khi ứng dụng web được khởi động. Hãy phân tích chi tiết từng dòng để hiểu rõ hơn:

### 1. **`ServletRegistration.Dynamic registration = servletContext.addServlet("dispatcher", dispatcherServlet);`**

- **Mục đích:** Dòng này tạo và đăng ký một đối tượng **DispatcherServlet** với **`ServletContext`**, gán cho nó tên "dispatcher".
- **`servletContext.addServlet("dispatcher", dispatcherServlet)`**: 
  - **`servletContext`**: Đây là đối tượng đại diện cho môi trường web của ứng dụng, nó chứa các thông tin và phương thức liên quan đến việc quản lý các servlet.
  - **`addServlet("dispatcher", dispatcherServlet)`**: Phương thức này thêm một servlet mới vào **`ServletContext`**. Ở đây, servlet mới được thêm là **`dispatcherServlet`** (một đối tượng của lớp **`DispatcherServlet`**) và nó được đặt tên là "dispatcher". Tên này được dùng để xác định servlet này trong các thành phần khác của ứng dụng.
- **Kết quả:** Phương thức trả về một đối tượng **`ServletRegistration.Dynamic`**, cho phép cấu hình thêm các thuộc tính của servlet.

### 2. **`registration.setLoadOnStartup(1);`**

- **Mục đích:** Thiết lập thứ tự khởi tạo của servlet khi ứng dụng được khởi động.
- **`setLoadOnStartup(1)`**: 
  - Tham số số nguyên (ở đây là **1**) xác định thứ tự khởi động servlet. Giá trị dương (ví dụ: 1) nghĩa là servlet này sẽ được khởi tạo ngay khi ứng dụng web khởi động, thay vì đợi đến khi có yêu cầu HTTP đầu tiên gửi tới servlet.
  - Giá trị càng thấp, servlet càng được khởi tạo sớm. Trong trường hợp này, servlet sẽ được khởi tạo ngay lập tức khi ứng dụng khởi chạy.
- **Kết quả:** Đảm bảo **Dispatcher Servlet** sẽ được khởi tạo sớm để sẵn sàng xử lý các yêu cầu HTTP ngay khi ứng dụng bắt đầu hoạt động.

### 3. **`registration.addMapping("/");`**

- **Mục đích:** Xác định URL pattern mà servlet sẽ xử lý.
- **`addMapping("/")`**:
  - Đây là phần định nghĩa URL pattern mà servlet sẽ xử lý. Trong trường hợp này, **`"/"`** nghĩa là **Dispatcher Servlet** sẽ chịu trách nhiệm xử lý **tất cả các yêu cầu HTTP** đến ứng dụng (mọi URL).
  - Dấu gạch chéo ("/") là ký tự đại diện cho root URL của ứng dụng. Tất cả các yêu cầu tới ứng dụng, ví dụ: `http://localhost:8080/` hoặc `http://localhost:8080/home`, sẽ được **Dispatcher Servlet** xử lý.
  
### Tóm tắt:

- **`ServletRegistration.Dynamic registration = servletContext.addServlet("dispatcher", dispatcherServlet);`**: Đăng ký servlet có tên "dispatcher" với **`ServletContext`**.
- **`registration.setLoadOnStartup(1);`**: Thiết lập cho servlet này được khởi động ngay khi ứng dụng khởi chạy.
- **`registration.addMapping("/");`**: Gán URL pattern để servlet xử lý tất cả các yêu cầu HTTP đến root URL.

Như vậy, mã này đảm bảo rằng **Dispatcher Servlet** (trung tâm trong Spring MVC) sẽ được khởi động ngay lập tức và sẵn sàng xử lý mọi yêu cầu HTTP gửi tới ứng dụng.
