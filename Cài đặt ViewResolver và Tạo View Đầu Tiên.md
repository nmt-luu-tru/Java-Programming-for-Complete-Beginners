Trong video này, chúng ta sẽ tìm hiểu về **ViewResolver** và **View** trong Spring MVC và cách chúng giúp chúng ta hiển thị dữ liệu trong trình duyệt mà không cần phải sử dụng một công nghệ view cụ thể.

### 1. Tổng quan về ViewResolver và Views

Spring MVC định nghĩa hai khái niệm quan trọng:
- **ViewResolver**: Giúp ánh xạ tên view (chẳng hạn như tên file JSP, Thymeleaf, Freemarker, v.v.) với chính các view cụ thể. Khi ứng dụng nhận một yêu cầu từ người dùng, **ViewResolver** sẽ xác định view phù hợp để hiển thị dựa trên tên của view và các cấu hình được định nghĩa trước.
- **View**: Là các thành phần hiển thị dữ liệu, như trang HTML, các mẫu JSP, Thymeleaf, v.v.

### 2. Sử dụng JSP làm công nghệ View

**JSP** (Java Server Pages) là một công nghệ phổ biến trong Java web để tạo ra các trang web động. Các trang JSP bao gồm hai loại dữ liệu:
- **Dữ liệu tĩnh**: Có thể là HTML hoặc bất kỳ định dạng văn bản nào.
- **JSP elements**: Bao gồm các thẻ JSP cho phép xử lý dữ liệu động.

Chúng ta sẽ bắt đầu bằng việc sử dụng **JSP** làm công nghệ View, sau đó sẽ chuyển sang **Thymeleaf** ở các phần sau.

Ngoài ra, Spring MVC cũng hỗ trợ **JSTL** (Java Server Pages Standard Tag Library), một thư viện thẻ để thực hiện các tác vụ thông thường như lặp qua danh sách, xử lý điều kiện, v.v.

### 3. Cài đặt ViewResolver và Tạo View Đầu Tiên

#### Bước 1: Tạo View trong thư mục WEB-INF

Đầu tiên, chúng ta tạo một thư mục **view** bên trong **WEB-INF** để lưu trữ các file JSP. Thư mục này không thể truy cập trực tiếp từ trình duyệt, nhưng các controller của chúng ta có thể truy cập để hiển thị nội dung.

Tạo file **welcome.jsp** trong thư mục **view** với nội dung đơn giản hiển thị thông báo:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

#### Bước 2: Cấu hình ViewResolver

Tiếp theo, chúng ta sẽ cấu hình **ViewResolver** trong lớp **WebConfig**. Đây là nơi chúng ta định nghĩa các thuộc tính như **prefix** (tiền tố) và **suffix** (hậu tố) cho các view.

```java
@Configuration
@EnableWebMvc
@ComponentScan(basePackages = "academy.learnprogramming")
public class WebConfig {

    public static final String RESOLVER_PREFIX = "/WEB-INF/view/";
    public static final String RESOLVER_SUFFIX = ".jsp";

    @Bean
    public ViewResolver viewResolver() {
        InternalResourceViewResolver viewResolver = new InternalResourceViewResolver();
        viewResolver.setPrefix(RESOLVER_PREFIX);
        viewResolver.setSuffix(RESOLVER_SUFFIX);
        return viewResolver;
    }
}
```

Trong đoạn mã trên:
- **RESOLVER_PREFIX**: Định nghĩa đường dẫn đến thư mục chứa các file view, ở đây là **/WEB-INF/view/**.
- **RESOLVER_SUFFIX**: Xác định phần mở rộng của file view, ở đây là **.jsp**.
- **InternalResourceViewResolver**: Là lớp con của **UrlBasedViewResolver**, nó giúp ánh xạ view name (tên view) tới các file JSP cụ thể dựa trên prefix và suffix.

#### Bước 3: Tạo Controller và Map URL với View

Chúng ta sẽ cập nhật **DemoController** để xử lý các yêu cầu và trả về view **welcome.jsp**.

```java
@Controller
public class DemoController {

    @GetMapping("/welcome")
    public String welcome() {
        return "welcome";  // tên view (không cần đường dẫn và phần mở rộng vì ViewResolver sẽ thêm vào)
    }
}
```

Phương thức **welcome()** sẽ trả về tên view là **welcome**. ViewResolver sẽ tự động thêm **prefix** và **suffix** để tìm đúng file JSP: **/WEB-INF/view/welcome.jsp**.

#### Bước 4: Chạy ứng dụng và kiểm tra kết quả

Cuối cùng, chúng ta chạy ứng dụng, sử dụng **Maven** để thực hiện **clean install** và sau đó khởi chạy **Tomcat** bằng **cargo run**.

Truy cập vào URL sau trong trình duyệt:
```
http://localhost:8080/todo-list/welcome
```
Kết quả sẽ hiển thị nội dung của file **welcome.jsp**, tức là thông báo **Hello World**.

### 4. Kiểm tra log và quá trình xử lý yêu cầu

Khi kiểm tra log trong IntelliJ, chúng ta có thể thấy thông tin liên quan đến quá trình xử lý yêu cầu:
- **DispatcherServlet** nhận yêu cầu GET cho **/welcome**.
- **ViewResolver** ánh xạ tên view **welcome** tới file **/WEB-INF/view/welcome.jsp**.
- **DispatcherServlet** hoàn thành xử lý yêu cầu và trả về kết quả cho trình duyệt.

### 5. Kết luận

Trong video này, chúng ta đã tìm hiểu cách tạo một **ViewResolver** trong Spring MVC, sử dụng JSP làm công nghệ view, và cấu hình controller để xử lý yêu cầu và trả về view. Chúng ta cũng thấy cách **ViewResolver** tự động thêm prefix và suffix để ánh xạ tên view tới file JSP cụ thể. 

Trong các video tiếp theo, chúng ta sẽ tiếp tục tìm hiểu về quá trình xử lý yêu cầu trong Spring MVC và cách sử dụng các công nghệ view khác như Thymeleaf.
