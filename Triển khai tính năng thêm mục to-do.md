
### Bước 1: Tạo tệp JSP cho form thêm mục mới

Đầu tiên, chúng ta sao chép tệp **items_list.jsp** và đổi tên thành **add_item.jsp** để tạo form cho việc thêm mục mới vào danh sách to-do.

**Tạo tệp `add_item.jsp`:**

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

<html>
<head>
    <title>Add To-Do Item</title>
</head>
<body>
    <div align="center">
        <h2>Add New To-Do Item</h2>
        <form:form method="POST" modelAttribute="${attributeNames.todo_item}">
            <table>
                <tr>
                    <td>Title:</td>
                    <td><form:input path="title" /></td>
                </tr>
                <tr>
                    <td>Details:</td>
                    <td><form:input path="details" /></td>
                </tr>
                <tr>
                    <td>Deadline:</td>
                    <td><form:input path="deadline" /></td>
                </tr>
                <tr>
                    <td colspan="2">
                        <input type="submit" value="Add Item" />
                    </td>
                </tr>
            </table>
        </form:form>
    </div>
</body>
</html>
```

**Giải thích:**
- **form:form**: Tạo biểu mẫu để nhập dữ liệu. `modelAttribute` liên kết form với một đối tượng trong controller (ở đây là `todoItem`).
- **form:input**: Tạo các trường nhập liệu cho các thuộc tính `title`, `details`, và `deadline`.

### Bước 2: Cập nhật Controller để xử lý dữ liệu từ form

Trong controller, chúng ta sẽ tạo một phương thức mới để xử lý dữ liệu được gửi từ form. Phương thức này sử dụng yêu cầu POST để thêm mục mới vào danh sách.

**Phương thức trong `TodoItemController.java`:**

```java
import model.TodoItem;
import service.TodoItemService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/todo-list")
public class TodoItemController {

    private final TodoItemService todoItemService;

    @Autowired
    public TodoItemController(TodoItemService todoItemService) {
        this.todoItemService = todoItemService;
    }

    @PostMapping("/add-item")
    public String processItem(@ModelAttribute("todoItem") TodoItem todoItem) {
        todoItemService.addItem(todoItem);
        return "redirect:/todo-list/items";
    }
}
```

**Giải thích:**
- **@Controller**: Đánh dấu lớp này là một Spring MVC Controller.
- **@PostMapping("/add-item")**: Xử lý các yêu cầu POST tới `/add-item`. Sau khi xử lý, người dùng sẽ được chuyển hướng tới trang hiển thị danh sách các mục.
- **@ModelAttribute("todoItem")**: Dữ liệu từ form sẽ được **tự động chuyển thành một đối tượng** `TodoItem` và sau đó thêm vào danh sách thông qua phương thức `addItem()` của `TodoItemService`.
- **return "redirect:/todo-list/items"**: Sau khi thêm mục mới thành công, người dùng sẽ được chuyển hướng về trang liệt kê các mục to-do.
