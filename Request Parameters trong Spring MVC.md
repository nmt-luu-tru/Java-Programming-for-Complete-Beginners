
### Request Parameters trong Spring MVC

Trong video này, chúng ta sẽ cùng thảo luận về **request parameters** (tham số yêu cầu) và cách sử dụng **@RequestParam** để lấy dữ liệu từ yêu cầu HTTP.

#### Bước 1: Sửa lỗi nhỏ trong tên lớp

Trước khi tiếp tục, tôi muốn sửa một lỗi nhỏ về tên lớp đã tồn tại trong mã nguồn. Để sửa, hãy mở lớp **WebAppInitializer** (đúng tên là WebAppInitializer chứ không phải WebAppInitilizer như trước đây). Sau đó, hãy nhấp chuột phải vào tên lớp, chọn **Refactor > Rename** để đổi tên chính xác thành **WebAppInitializer**.

#### Bước 2: Sử dụng @RequestParam

Bây giờ, hãy mở lớp **DemoController** và thêm logic để xử lý **request parameters**.

Hiện tại, khi truy cập trang chào mừng, luôn hiển thị thông báo `"Hello Tim"`. Tuy nhiên, bây giờ chúng ta muốn thông báo được hiển thị dựa trên **request parameters**.

**Request Parameters** trong Spring MVC là các tham số truyền qua URL. Chúng ta có thể sử dụng **@RequestParam** để lấy các giá trị này.

#### Cập nhật phương thức `welcome` trong **DemoController**:

```java
import org.springframework.web.bind.annotation.RequestParam;

@GetMapping("/welcome")
public String welcome(@RequestParam String user, Model model) {
    // Sử dụng request parameter 'user'
    model.addAttribute("helloMessage", demoService.getHelloMessage(user));
    return "welcome";
}
```

- **@RequestParam**: Chú thích này dùng để gắn tham số yêu cầu từ URL với tham số trong phương thức. Ở đây, tham số "user" sẽ được lấy từ URL và truyền vào phương thức.

Ví dụ, URL sẽ trông như thế này:  
`http://localhost:8080/todo-list/welcome?user=Tim`

Trong URL này, chúng ta truyền tham số `user=Tim`, và phương thức `welcome` sẽ nhận được chuỗi "Tim" thông qua **@RequestParam**.

#### Thêm thuộc tính mới cho mô hình (model):

Trong phương thức `welcome`, chúng ta cũng thêm thuộc tính `"helloMessage"` vào mô hình để hiển thị trên trang **JSP**.

#### Sử dụng tham số không bắt buộc:

Mặc định, tham số trong **@RequestParam** là bắt buộc. Nếu không truyền giá trị, bạn sẽ gặp lỗi. Nếu muốn cho phép tham số không bắt buộc, chúng ta có thể cấu hình như sau:

```java
@RequestParam(value = "user", required = false, defaultValue = "Guest")
```

- **required**: Đặt là `false` để cho phép tham số không bắt buộc.
- **defaultValue**: Nếu không có giá trị, giá trị mặc định là `"Guest"`.

#### Ví dụ với nhiều tham số yêu cầu:

Bây giờ, giả sử bạn muốn thêm một tham số mới là **age**. Chúng ta chỉ cần thêm một tham số khác với **@RequestParam**.

Cập nhật phương thức `welcome`:

```java
@GetMapping("/welcome")
public String welcome(@RequestParam String user, @RequestParam int age, Model model) {
    model.addAttribute("helloMessage", demoService.getHelloMessage(user));
    model.addAttribute("age", age);
    return "welcome";
}
```

- Tham số **age** sẽ được lấy từ URL và thêm vào mô hình (model) để hiển thị trên trang **JSP**.

#### Cập nhật **welcome.jsp** để hiển thị thông báo:

```jsp
<h1>${helloMessage}</h1>
<h2>Your age is: ${age}</h2>
<h2>${welcomeMessage}</h2>
```

Bây giờ, khi bạn truy cập URL sau:

`http://localhost:8080/todo-list/welcome?user=John&age=30`

Trang web sẽ hiển thị thông điệp như sau:

```
Hello John
Your age is: 30
Welcome to this demo application
```

#### Kiểm tra:

1. Chạy cấu hình Maven (`clean install` và `cargo run`).
2. Mở trình duyệt và truy cập URL với query parameters.
3. Xem kết quả hiển thị trong JSP, đảm bảo rằng tham số yêu cầu hoạt động chính xác.

---

### Tổng kết

- **@RequestParam**: Dùng để lấy tham số từ yêu cầu HTTP. Chúng ta có thể sử dụng nó với nhiều loại dữ liệu khác nhau và có thể đặt tham số là không bắt buộc.
- **Model**: Chứa dữ liệu được chuyển từ controller sang view (JSP).
- URL có thể bao gồm nhiều **request parameters** với cú pháp `?parameter1=value1&parameter2=value2`.

Video tiếp theo sẽ hướng dẫn về yêu cầu và mục tiêu của ứng dụng quản lý to-do list.
