Khi bạn sử dụng **`@ModelAttribute`** trong Spring MVC, phương thức có annotation này sẽ tự động được gọi **trước khi bất kỳ request nào được xử lý** bởi controller, không phụ thuộc vào URL cụ thể (ví dụ: `/welcome` hay bất kỳ URL nào khác). Điều này có nghĩa là thuộc tính được thêm vào **Model** sẽ có sẵn cho tất cả các **View** tương ứng trong các request khác nhau mà controller xử lý.

### Cách hoạt động của **`@ModelAttribute`**:

1. **Phương thức có annotation `@ModelAttribute`**:
   - Mỗi lần một request được gửi đến controller, Spring sẽ gọi tất cả các phương thức có annotation **`@ModelAttribute`** trước khi gọi các phương thức xử lý request (như **`@GetMapping`**, **`@PostMapping`**). Những dữ liệu được thêm vào **Model** bởi các phương thức này sẽ được chia sẻ cho tất cả các view tương ứng với các request khác nhau.

2. **Phạm vi áp dụng**:
   - Nếu bạn khai báo **`@ModelAttribute`** ở cấp độ phương thức trong controller, thì phương thức đó sẽ được gọi cho mọi request đến controller đó.
   - Nếu bạn cần gắn một thuộc tính **chỉ cho một URL cụ thể**, bạn sẽ phải thêm nó trong phương thức xử lý request (chẳng hạn như trong một phương thức có **`@GetMapping`**).

### Ví dụ:

```java
@Controller
public class DemoController {

    // Phương thức @ModelAttribute sẽ được gọi trước mỗi request đến controller này
    @ModelAttribute("welcomeMessage")
    public String welcomeMessage() {
        return "Welcome to this demo application";
    }

    @GetMapping("/welcome")
    public String welcome(Model model) {
        model.addAttribute("user", "Tim");
        return "welcome";  // Chuyển tiếp đến welcome.jsp
    }

    @GetMapping("/goodbye")
    public String goodbye(Model model) {
        model.addAttribute("user", "Tom");
        return "goodbye";  // Chuyển tiếp đến goodbye.jsp
    }
}
```

### Giải thích:
- Phương thức **`welcomeMessage()`** có **`@ModelAttribute("welcomeMessage")`**. Điều này nghĩa là mỗi khi có bất kỳ request nào đến **`DemoController`**, thuộc tính **`welcomeMessage`** với giá trị **"Welcome to this demo application"** sẽ được tự động thêm vào model trước khi Spring gọi các phương thức xử lý khác (như **`welcome()`** hay **`goodbye()`**).
  
- **Model dữ liệu chung**: Khi truy cập vào **`/welcome`** hay **`/goodbye`**, thuộc tính **`welcomeMessage`** sẽ luôn có sẵn trong model để sử dụng trong các view như **`welcome.jsp`** và **`goodbye.jsp`**.

### **JSP (welcome.jsp)**:
```jsp
<html>
<head>
    <title>Welcome Page</title>
</head>
<body>
    <h1>${welcomeMessage}</h1>
    <h2>Hello ${user}</h2>
</body>
</html>
```

### **JSP (goodbye.jsp)**:
```jsp
<html>
<head>
    <title>Goodbye Page</title>
</head>
<body>
    <h1>${welcomeMessage}</h1>
    <h2>Goodbye ${user}</h2>
</body>
</html>
```

### Chạy ứng dụng:
- Khi bạn truy cập **`/welcome`**, bạn sẽ thấy:
  - **`welcomeMessage`**: `"Welcome to this demo application"`
  - **`user`**: `"Tim"`

  Kết quả trên trang sẽ là:  
  ```
  Welcome to this demo application
  Hello Tim
  ```

- Khi bạn truy cập **`/goodbye`**, bạn sẽ thấy:
  - **`welcomeMessage`**: `"Welcome to this demo application"`
  - **`user`**: `"Tom"`

  Kết quả trên trang sẽ là:  
  ```
  Welcome to this demo application
  Goodbye Tom
  ```

### **Lưu ý:**
- **`@ModelAttribute`** có thể sử dụng không chỉ để thêm dữ liệu cho **Model** mà còn để xử lý các đối tượng phức tạp, chẳng hạn như form binding hoặc các đối tượng domain.
- **Phương thức `@ModelAttribute`** được gọi trước mỗi phương thức xử lý request trong controller, nghĩa là nó sẽ có sẵn cho bất kỳ request nào mà controller này nhận.

### Tổng kết:
Khi sử dụng **`@ModelAttribute`** trong controller, Spring sẽ gọi phương thức này trước khi xử lý bất kỳ request nào và tự động thêm các thuộc tính vào **Model**, bất kể URL cụ thể. Điều này rất tiện lợi nếu bạn cần cung cấp một số dữ liệu chung cho nhiều view khác nhau trong ứng dụng.
