Trong video này, chúng ta sẽ đi sâu vào chi tiết hơn về quá trình xử lý yêu cầu (request processing) trong Spring MVC. Quy trình xử lý yêu cầu trong Spring MVC có thể được chia thành 10 bước. Tôi sẽ giải thích từng bước để bạn hiểu rõ hơn về cách ứng dụng Spring MVC xử lý các yêu cầu từ trình duyệt và trả lại kết quả.

### Bước 1 & 2: Trình duyệt tạo yêu cầu và DispatcherServlet nhận yêu cầu

- **Bước 1: Trình duyệt gửi yêu cầu đến một URL cụ thể**. Ví dụ, khi người dùng nhập URL hoặc nhấp vào liên kết trên trang web, yêu cầu HTTP (ví dụ: GET hoặc POST) sẽ được gửi từ trình duyệt tới máy chủ. URL này có thể là bất kỳ URL nào, chẳng hạn `/welcome` hoặc `/hello`. Đây là nơi mà yêu cầu bắt đầu.
  
- **Bước 2: DispatcherServlet nhận yêu cầu**. Trong kiến trúc **Spring MVC**, **DispatcherServlet** đóng vai trò là **front controller**. Nó là một điểm trung tâm nhận mọi yêu cầu HTTP gửi từ phía client (trình duyệt). **DispatcherServlet không tự xử lý các yêu cầu mà nó sẽ chuyển tiếp các yêu cầu này đến các thành phần khác trong ứng dụng để xử lý.** Trong bước này, **DispatcherServlet** tiếp nhận yêu cầu từ trình duyệt và bắt đầu quá trình xử lý.

### Bước 3 & 4: DispatcherServlet tìm phương thức xử lý và gọi phương thức đó

- **Bước 3: DispatcherServlet sử dụng Handler Mapping để tìm phương thức xử lý thích hợp**. Khi yêu cầu đến, **DispatcherServlet** cần xác định controller nào và phương thức nào trong controller sẽ xử lý yêu cầu này. Nó sử dụng một thành phần gọi là **Handler Mapping** để ánh xạ yêu cầu đến phương thức tương ứng trong một controller cụ thể. Ví dụ, nếu yêu cầu là `/hello`, **Handler Mapping** sẽ ánh xạ yêu cầu này đến phương thức `hello()` trong controller có nhiệm vụ xử lý URL đó.

- **Bước 4: DispatcherServlet gọi phương thức trong Controller**. Khi đã xác định được phương thức thích hợp, **DispatcherServlet** sẽ gọi phương thức đó trong controller để xử lý yêu cầu. Ví dụ, nếu yêu cầu là `/hello`, phương thức `hello()` sẽ được gọi và bắt đầu quá trình xử lý logic của ứng dụng, chẳng hạn như tính toán dữ liệu hoặc chuẩn bị dữ liệu để hiển thị.

### Bước 5 & 6: Phương thức xử lý trả về Model và tên view

- **Bước 5: Phương thức trong Controller trả về một Model và tên view (view name)**. Khi phương thức trong controller xử lý yêu cầu xong, nó sẽ trả về hai thông tin chính: **Model** và **tên view**. **Model** chứa dữ liệu mà chúng ta muốn hiển thị trên trang web, chẳng hạn như danh sách sản phẩm, thông tin người dùng,... **Tên view** là tên của file view (ví dụ: file JSP hoặc Thymeleaf) sẽ được sử dụng để hiển thị kết quả. Trong ví dụ trước, khi phương thức `welcome()` trả về chuỗi "welcome", đây chính là **tên view logic** (logical view name) mà hệ thống sẽ dùng để tìm tệp JSP tương ứng.

- **Bước 6: DispatcherServlet tìm kiếm ViewResolver để xác định tệp view cụ thể**. Sau khi nhận được tên view logic (ví dụ "welcome"), **DispatcherServlet** sẽ không tự động biết đó là file nào. Thay vào đó, nó sẽ sử dụng một thành phần gọi là **ViewResolver** để ánh xạ từ tên view logic sang tệp view thực tế. **ViewResolver** được cấu hình để biết rằng các view nằm trong thư mục `WEB-INF/view/` và có phần mở rộng `.jsp`. Vì vậy, khi nhận được tên view logic "welcome", **ViewResolver** sẽ kết hợp với các cấu hình để tìm tệp `WEB-INF/view/welcome.jsp`.

### Bước 7 & 8: DispatcherServlet thực thi view và đưa dữ liệu vào model

- **Bước 7: ViewResolver trả về tệp JSP tương ứng**. Sau khi **ViewResolver** xác định được tệp view thực tế, nó sẽ trả về tệp này cho **DispatcherServlet**. Trong trường hợp này, đó là tệp `welcome.jsp`. Tệp JSP này sẽ chứa mã HTML và có thể chứa thêm các phần tử JSP để hiển thị dữ liệu động từ model.

- **Bước 8: DispatcherServlet xử lý tệp JSP và làm cho dữ liệu trong model sẵn sàng cho view**. **DispatcherServlet** sẽ xử lý tệp JSP và kết hợp dữ liệu từ **Model** (nếu có) để hiển thị kết quả. Tất cả dữ liệu mà controller đã đưa vào model sẽ được truyền vào JSP và hiển thị cho người dùng. Ví dụ, nếu model chứa một danh sách sản phẩm, JSP có thể sử dụng dữ liệu này để tạo danh sách sản phẩm động trên trang web.

### Bước 9 & 10: Trả về phản hồi cho trình duyệt

- **Bước 9: Tệp JSP được xử lý và trả về cho DispatcherServlet**. Sau khi JSP được xử lý và dữ liệu từ model được kết hợp vào, tệp JSP (với mã HTML động) sẽ được trả về cho **DispatcherServlet**. Đây chính là bước mà nội dung trang web được tạo ra và sẵn sàng gửi tới người dùng.

- **Bước 10: DispatcherServlet trả về kết quả cho trình duyệt**. Cuối cùng, **DispatcherServlet** sẽ gửi kết quả là trang HTML được tạo bởi tệp JSP về cho trình duyệt. Trình duyệt của người dùng sẽ hiển thị trang web này và người dùng sẽ thấy kết quả yêu cầu của họ, chẳng hạn như trang "Welcome" hoặc "Hello".

### Tổng kết

Các bước trên mô tả toàn bộ quá trình từ khi người dùng gửi yêu cầu từ trình duyệt, thông qua **DispatcherServlet**, cho đến khi nhận được phản hồi và hiển thị trên trình duyệt. Hiện tại, trong dự án **to-do list**, chúng ta đang sử dụng view đơn giản (JSP) và chưa có **model**. Trong các phần tiếp theo của khóa học, chúng ta sẽ khám phá sâu hơn về **model** và cách sử dụng **model attributes** để tạo ra các trang web động hơn.

### Kết luận

Hy vọng rằng việc hiểu rõ 10 bước xử lý yêu cầu này giúp bạn có cái nhìn sâu hơn về cách Spring MVC hoạt động, từ việc tiếp nhận yêu cầu đến khi trả kết quả lại cho người dùng. Trong các video tiếp theo, chúng ta sẽ học cách sử dụng **model** để truyền dữ liệu động từ controller tới view.
