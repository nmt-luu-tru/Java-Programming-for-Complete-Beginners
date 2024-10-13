Trong video này, chúng ta đã thảo luận về các **Controller** và cách xử lý các **request** (yêu cầu) trong Spring MVC, tập trung vào các annotation và phương thức mà chúng ta sử dụng để map các yêu cầu HTTP vào các phương thức của controller.

### 1. Tổng quan về Spring MVC và Dispatcher Servlet

**Spring MVC** hoạt động dựa trên mô hình **Model-View-Controller** (MVC). Trong mô hình này:
- **Model** quản lý dữ liệu và logic của ứng dụng.
- **View** chịu trách nhiệm hiển thị thông tin cho người dùng.
- **Controller** xử lý các yêu cầu từ người dùng, tương tác với Model để lấy dữ liệu và chuyển đến View để hiển thị.

**Dispatcher Servlet** đóng vai trò là **front controller** trong Spring MVC, nhận tất cả các yêu cầu từ người dùng và phân phối chúng đến các controller thích hợp. Nó là thành phần trung gian giữa trình duyệt (người dùng) và ứng dụng Spring.

### 2. Controller trong Spring MVC

Trong Spring MVC, **Controller** là thành phần chịu trách nhiệm xử lý các yêu cầu HTTP và trả về kết quả dưới dạng dữ liệu hoặc view.

- Chúng ta sử dụng **`@Controller`** annotation để đánh dấu một lớp là controller, để Spring có thể tự động phát hiện và xử lý.
- Phương thức trong controller có thể được gán các mapping cụ thể (ví dụ như **GET**, **POST**) sử dụng các annotation tương ứng như **`@GetMapping`**, **`@PostMapping`**.

Ví dụ:
```java
@Controller
public class DemoController {
    @GetMapping("/hello")
    public String hello() {
        return "hello";
    }
}
```

Ở đây, khi người dùng truy cập vào **`/hello`**, phương thức `hello()` sẽ được gọi và trả về kết quả.

### 3. Request Mapping và các phương thức HTTP

Trong Spring MVC, chúng ta có thể sử dụng **`@RequestMapping`** hoặc các phiên bản rút gọn của nó như:
- **`@GetMapping`**: xử lý các yêu cầu **GET**.
- **`@PostMapping`**: xử lý các yêu cầu **POST**.
- **`@PutMapping`**, **`@DeleteMapping`**, **`@PatchMapping`**: xử lý các yêu cầu **PUT**, **DELETE**, **PATCH** tương ứng.

### 4. Xây dựng Controller Đầu Tiên

#### Bước 1: Tạo một package và class controller

Trong IntelliJ, chúng ta bắt đầu bằng cách tạo một package có tên **controller** và một lớp mới tên **DemoController**. Lớp này sẽ đóng vai trò là một controller đơn giản trong ứng dụng của chúng ta.

```java
package academy.learnprogramming.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class DemoController {
    @GetMapping("/hello")
    public String hello() {
        return "hello";
    }
}
```

- **`@Controller`**: Đánh dấu lớp này là một controller.
- **`@GetMapping("/hello")`**: Map yêu cầu HTTP GET với URL `/hello` vào phương thức `hello()`. Khi người dùng truy cập vào địa chỉ **`/hello`**, phương thức này sẽ trả về một chuỗi `"hello"`. Tuy nhiên, chuỗi `"hello"` này là tên view và sẽ cần một **view resolver** để hiển thị.

#### Bước 2: Xử lý lỗi thiếu view

Khi chạy ứng dụng và truy cập vào **`/hello`**, chúng ta gặp lỗi **HTTP 500** (Internal Server Error) với thông báo lỗi liên quan đến **circular view path**. Điều này xảy ra vì Spring đang cố gắng tìm một view tên là `"hello"`, nhưng chúng ta chưa cấu hình view resolver hoặc không có view nào được định nghĩa.

#### Bước 3: Sửa lỗi bằng cách thêm **`@ResponseBody`**

Để khắc phục lỗi này mà không cần định nghĩa view, chúng ta có thể sử dụng **`@ResponseBody`**. Annotation này cho phép phương thức trả về dữ liệu trực tiếp thay vì tìm một view.

```java
@Controller
public class DemoController {
    @GetMapping("/hello")
    @ResponseBody
    public String hello() {
        return "hello";
    }
}
```

Với **`@ResponseBody`**, chuỗi `"hello"` sẽ được trả về dưới dạng dữ liệu thô và hiển thị trực tiếp trên trình duyệt, thay vì Spring cố gắng tìm một view tên `"hello"`.  

(Trong mô hình MVC chỉ sử dụng **Servlet** và **JSP** ngày trước, khi chưa sử dụng **Spring MVC**, bạn sẽ phải chuyển tiếp dữ liệu từ Servlet đến JSP để hiển thị. Việc này yêu cầu thêm bước sử dụng `RequestDispatcher` để điều hướng đến trang JSP tương ứng.)

#### Bước 4: Chạy lại ứng dụng

Chúng ta chạy lại các lệnh **clean install** và **cargo run** để khởi động Tomcat và kiểm tra lại ứng dụng trên trình duyệt. Bây giờ, khi truy cập vào **`http://localhost:8080/to-do-list/hello`**, chuỗi `"hello"` sẽ được hiển thị trực tiếp trên trình duyệt, điều này chứng tỏ ứng dụng đã xử lý thành công yêu cầu GET.

### 5. Kiểm tra log và quá trình xử lý yêu cầu

Khi kiểm tra log trong IntelliJ, chúng ta có thể thấy rằng Dispatcher Servlet đã nhận yêu cầu GET và chuyển tiếp đến phương thức `hello()` trong controller. Quá trình xử lý diễn ra đúng như mong đợi và kết quả được trả về thành công.

### 6. Kết luận

Trong video này, chúng ta đã học cách tạo **Controller** trong Spring MVC và sử dụng annotation **`@GetMapping`** để map các yêu cầu HTTP GET vào các phương thức trong controller. Chúng ta cũng đã sử dụng **`@ResponseBody`** để trả về dữ liệu thô từ controller mà không cần phải sử dụng view.

Ở các video tiếp theo, chúng ta sẽ đi sâu hơn vào cách xử lý request và các khái niệm liên quan đến view trong Spring MVC.
