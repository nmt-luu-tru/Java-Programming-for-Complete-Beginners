
Trong video này, chúng ta sẽ đi sâu vào khái niệm **Model** và chú thích **ModelAttribute** trong Spring MVC. Trước tiên, chúng ta sẽ thảo luận về giao diện **Model** và cách nó hoạt động trong quá trình tương tác giữa Controller và View.

### Giao diện Model là gì?

Giao diện **Model** định nghĩa một "bộ chứa" (holder) để lưu trữ các thuộc tính của model, và chủ yếu được sử dụng để thêm các thuộc tính vào model. Những thuộc tính này sau đó sẽ được hiển thị trong View. Nói cách khác, model đại diện cho dữ liệu mà bạn muốn hiển thị trên giao diện người dùng (ví dụ như JSP). Những dữ liệu này sẽ được chuyển từ Controller tới View thông qua model.

### Áp dụng Model trong DemoController

Bây giờ, hãy mở lớp **DemoController** của chúng ta và thực hiện một số thay đổi để minh họa cách sử dụng model. 

Hiện tại, phương thức **welcome()** của chúng ta chưa có tham số. Ta có thể bổ sung một tham số kiểu **Model** vào phương thức để thêm dữ liệu vào model. Ta sẽ thay đổi phương thức như sau:

```java
@Controller
@Slf4j
public class DemoController {

    @GetMapping("/welcome")
    public String welcome(Model model) {
        model.addAttribute("user", "Tim");
        log.info("Model = {}", model);
        return "welcome";
    }
}
```

Ở đây, chúng ta thêm một thuộc tính với khóa là `"user"` và giá trị là `"Tim"` vào **model**. Khi đó, chúng ta có thể truy cập thuộc tính này trong **JSP** để hiển thị lên trang web. Trước khi làm điều này, chúng ta cũng thêm một câu lệnh log để hiển thị model trên console.

### Hiển thị dữ liệu từ Model trong JSP

Bây giờ, trong file **welcome.jsp**, chúng ta sẽ sửa đổi để hiển thị dữ liệu từ model. Chúng ta sẽ thay đổi nội dung `Hello World` thành:

```jsp
Hello ${user}
```

Cú pháp `${}` là cú pháp chuẩn của **JSP** để hiển thị giá trị của một thuộc tính từ model.

### Chạy và Kiểm tra

Sau khi cấu hình xong, chúng ta sẽ chạy ứng dụng và kiểm tra kết quả trong trình duyệt. Khi vào URL `/welcome`, chúng ta sẽ thấy chuỗi `"Hello Tim"` được hiển thị.

### Chú thích ModelAttribute

Một cách khác để thêm dữ liệu vào model là sử dụng chú thích **@ModelAttribute**. Chúng ta có thể sử dụng chú thích này trên một phương thức để tự động thêm thuộc tính vào model. Ví dụ:

```java
@Controller
@Slf4j
public class DemoController {

    @ModelAttribute("welcomeMessage")
    public String welcomeMessage() {
        log.info("Welcome message called");
        return "Welcome to this demo application";
    }

    @GetMapping("/welcome")
    public String welcome(Model model) {
        model.addAttribute("user", "Tim");
        log.info("Model = {}", model);
        return "welcome";
    }
}
```

Khi sử dụng chú thích **@ModelAttribute**, phương thức sẽ được gọi trước mỗi lần Controller xử lý yêu cầu. Thuộc tính `"welcomeMessage"` sẽ được thêm vào model, và ta có thể sử dụng nó trong JSP:

```jsp
<h2>${welcomeMessage}</h2>
```

### Chạy lại và Kiểm tra

Chạy lại ứng dụng, và khi vào trang **/welcome**, ta sẽ thấy dòng `"Welcome to this demo application"` hiển thị trên trang web. Điều này xác nhận rằng thuộc tính đã được thêm vào model và hiển thị chính xác trên view.

### Tổng kết

- **Model** được sử dụng để truyền dữ liệu từ Controller đến View.
- Có hai cách thêm dữ liệu vào model:
  - Sử dụng phương thức **model.addAttribute()** trong Controller.
  - Sử dụng chú thích **@ModelAttribute** để thêm dữ liệu tự động vào model trước khi phương thức trong Controller được gọi.

Trong các video tiếp theo, chúng ta sẽ đi sâu hơn vào việc sử dụng **Model** khi xử lý các form và lấy dữ liệu từ người dùng.  

---  
### So sánh với sử dụng JSP và Servlet truyền thống  

Nếu không sử dụng **Spring MVC** mà chỉ sử dụng **JSP** và **Servlet** truyền thống, bạn vẫn có thể thực hiện các ví dụ tương tự như trong Spring MVC, nhưng cách thức sẽ khác một chút. Cụ thể, bạn sẽ phải quản lý việc chuyển dữ liệu từ **Servlet** sang **JSP** theo cách thủ công hơn. Hãy cùng phân tích từng phần và cách triển khai với **JSP** và **Servlet**.

#### Cách làm tương tự trong Servlet và JSP:
Thay vì sử dụng **Model**, bạn sẽ sử dụng đối tượng **`HttpServletRequest`** để thêm thuộc tính vào request, sau đó chuyển tiếp request đó đến **JSP** để hiển thị dữ liệu.

**Servlet (WelcomeServlet.java):**

```java
@WebServlet("/welcome")
public class WelcomeServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Thêm thuộc tính vào request
        request.setAttribute("user", "Tim");
        
        // Chuyển tiếp yêu cầu đến trang welcome.jsp
        RequestDispatcher dispatcher = request.getRequestDispatcher("welcome.jsp");
        dispatcher.forward(request, response);
    }
}
```

**JSP (welcome.jsp):**

```jsp
<html>
<head>
    <title>Welcome Page</title>
</head>
<body>
    <h1>Hello ${user}</h1>
</body>
</html>
```

Trong trường hợp này, thuộc tính `"user"` được đặt vào **request** thông qua **`request.setAttribute()`** và sau đó có thể được truy cập trong JSP sử dụng cú pháp **`${}`** tương tự như trong Spring MVC.
