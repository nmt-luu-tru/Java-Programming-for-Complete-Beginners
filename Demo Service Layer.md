
### Thử thách Simple Service:

**Mục tiêu:** Tạo một interface gọi là `DemoService` với hai phương thức. Tiếp đó, tạo một class thực thi interface này và sử dụng nó trong lớp `DemoController` thông qua tiêm phụ thuộc.

#### Các bước thực hiện:

1. **Tạo Interface `DemoService`:**
   Interface này sẽ có hai phương thức:
   - `getHelloMessage(String user)` trả về chuỗi "Hello" kết hợp với tên người dùng.
   - `getWelcomeMessage()` trả về chuỗi "Welcome to this demo application".

```java
public interface DemoService {
    String getHelloMessage(String user);
    String getWelcomeMessage();
}
```

2. **Tạo lớp `DemoServiceImpl`**:
   Lớp này sẽ triển khai interface `DemoService` và được chú thích với `@Service`. 

```java
import org.springframework.stereotype.Service;

@Service
public class DemoServiceImpl implements DemoService {

    @Override
    public String getHelloMessage(String user) {
        return "Hello " + user;
    }

    @Override
    public String getWelcomeMessage() {
        return "Welcome to this demo application";
    }
}
```

3. **Sử dụng `DemoService` trong `DemoController`:**
   Trong lớp `DemoController`, tiêm phụ thuộc `DemoService` bằng cách sử dụng **Constructor Injection** với chú thích `@Autowired`. 

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import lombok.extern.slf4j.Slf4j;

@Controller
@Slf4j
public class DemoController {

    private final DemoService demoService;

    // Constructor Injection
    @Autowired
    public DemoController(DemoService demoService) {
        this.demoService = demoService;
    }

    // Request Method
    @GetMapping("/welcome")
    public String welcome(Model model) {
        // Sử dụng DemoService để lấy thông điệp
        model.addAttribute("helloMessage", demoService.getHelloMessage("Tim"));
        return "welcome";
    }

    // Model attribute method
    @ModelAttribute("welcomeMessage")
    public String welcomeMessage() {
        return demoService.getWelcomeMessage();
    }
}
```

- Ở đây, chúng ta đã thay đổi phương thức `welcome` để sử dụng phương thức `getHelloMessage` của `DemoService` thay vì truyền trực tiếp chuỗi. Chúng ta cũng sử dụng phương thức `getWelcomeMessage` trong phương thức model attribute.

4. **Cập nhật file `welcome.jsp`**:
   Trong file **welcome.jsp**, cập nhật để hiển thị giá trị của các thuộc tính mới:

```jsp
<h1>${helloMessage}</h1>
<h2>${welcomeMessage}</h2>
```

### Giải thích:

- **@Service**: Chú thích này là một **stereotype annotation** (giống như `@Controller` hoặc `@Component`), dùng để đánh dấu một class là một **service layer** trong ứng dụng. Các lớp service thường chứa logic nghiệp vụ và được tiêm vào các lớp khác (như controller) để sử dụng.
- **@Autowired**: Chú thích này được sử dụng để yêu cầu Spring tiêm phụ thuộc. Ở đây, chúng ta sử dụng **Constructor Injection** để tiêm `DemoService` vào `DemoController`.
- **@ModelAttribute**: Chú thích này được dùng để thêm thuộc tính vào model, giúp hiển thị trên view.

### Kiểm tra:

Chạy ứng dụng, vào URL `http://localhost:8080/todo-list/welcome`, bạn sẽ thấy các thông báo `"Hello Tim"` và `"Welcome to this demo application"` được hiển thị.

### Tổng kết:

Trong thử thách này, bạn đã:

- Tạo interface và triển khai nó bằng một lớp.
- Tiêm phụ thuộc `DemoService` vào `DemoController` bằng cách sử dụng **Constructor Injection**.
- Cập nhật JSP để sử dụng các thuộc tính model mới.
