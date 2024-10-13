Trong video này, chúng ta sẽ tiếp tục xây dựng tính năng thêm mục to-do bằng cách sử dụng thẻ Spring Form và thiết lập các phương thức trong controller để xử lý yêu cầu từ người dùng. Đầu tiên, chúng ta sẽ tạo một form để người dùng có thể nhập thông tin của mục to-do mới, sau đó, chúng ta sẽ cập nhật controller để xử lý dữ liệu từ form này và thêm mục to-do vào hệ thống.

### Bước 1: Tạo file JSP cho form

Đầu tiên, chúng ta cần tạo một file JSP mới để chứa form cho việc thêm mục to-do. Bạn có thể sao chép file `items_list.jsp` đã có trước đó và đổi tên thành `add_item.jsp`. Sau đó, chỉnh sửa nội dung để phù hợp với form nhập liệu.

Dưới đây là mã HTML cho form thêm mục to-do:

```jsp
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

<html>
<head>
    <title>Add To-Do Item</title>
</head>
<body>
    <div align="center">
        <h2>Add To-Do Item</h2>
        <form:form method="POST" modelAttribute="${attributeNames.todo_item}">
            <table>
                <tr>
                    <td>Id:</td>
                    <td>
                        <form:input path="id" disabled="true"/>
                    </td>
                </tr>
                <tr>
                    <td>Title:</td>
                    <td>
                        <form:input path="title"/>
                    </td>
                </tr>
                <tr>
                    <td>Details:</td>
                    <td>
                        <form:textarea path="details"/>
                    </td>
                </tr>
                <tr>
                    <td>Deadline:</td>
                    <td>
                        <form:input path="deadline"/>
                    </td>
                </tr>
                <tr>
                    <td colspan="2">
                        <input type="submit" value="Submit"/>
                    </td>
                </tr>
            </table>
        </form:form>
    </div>
</body>
</html>
```

### Diễn giải:

1. **Thẻ form:form**: Sử dụng thẻ `form:form` của Spring để tạo form. Thuộc tính `modelAttribute` chỉ ra rằng form này được liên kết với đối tượng `todo_item`, được định nghĩa trong controller.
  
2. **Trường nhập liệu**:
   - **Id**: Trường này bị vô hiệu hóa bằng cách sử dụng thuộc tính `disabled="true"`, do ID sẽ được tạo tự động và người dùng không cần nhập vào.
   - **Title, Details, Deadline**: Các trường này cho phép người dùng nhập tiêu đề, chi tiết và thời hạn của mục to-do.

3. **Nút Submit**: Thẻ `<input type="submit"/>` sẽ gửi form khi người dùng nhấn nút.

### Bước 2: Thiết lập Controller

Tiếp theo, chúng ta cần thiết lập controller để xử lý form này. Trong lớp `ToDoItemController`, chúng ta sẽ thêm các phương thức để hiển thị form và xử lý dữ liệu khi form được gửi.

```java
@Controller
public class ToDoItemController {

    private final ToDoItemService toDoItemService;

    @Autowired
    public ToDoItemController(ToDoItemService toDoItemService) {
        this.toDoItemService = toDoItemService;
    }

    // Hiển thị form thêm mục to-do
    @GetMapping("/todo-list/add")
    public String addItem(Model model) {
        ToDoItem newItem = new ToDoItem("", "", LocalDate.now());
        model.addAttribute("todo_item", newItem);
        return "add_item";
    }

    // Xử lý khi form được gửi
    @PostMapping("/todo-list/add")
    public String processItem(@ModelAttribute("todo_item") ToDoItem toDoItem) {
        toDoItemService.addItem(toDoItem);
        return "redirect:/todo-list/items";
    }
}
```

### Diễn giải controller:

- **Phương thức `addItem` (GET)**:
   - Tạo một đối tượng **ToDoItem** mới và thêm nó vào `model` với tên thuộc tính `"todo_item"`.
   - Trả về tên view `"add_item"`, hiển thị form để thêm mục mới.

- **Phương thức `processItem` (POST)**:
   - Dữ liệu từ form sẽ được truyền vào dưới dạng đối tượng **ToDoItem** nhờ cơ chế binding của Spring. Spring tự động liên kết các trường từ form với các thuộc tính của đối tượng.
   - Gọi phương thức `addItem` từ **ToDoItemService** để thêm mục mới vào hệ thống.
   - Sau đó, người dùng sẽ được chuyển hướng trở lại trang danh sách các mục **to-do** bằng cách sử dụng kỹ thuật **Post-Redirect-Get**.

### Bước 3: Kiểm tra dữ liệu đầu vào và nhật ký

Trong phương thức `processItem`, chúng ta có thể thêm một dòng nhật ký để kiểm tra dữ liệu từ form được nhận đúng hay không:

```java
@PostMapping("/todo-list/add")
public String processItem(@ModelAttribute("todo_item") ToDoItem toDoItem) {
    log.info("To-Do Item from form = {}", toDoItem);
    toDoItemService.addItem(toDoItem);
    return "redirect:/todo-list/items";
}
```

Nhật ký này sẽ giúp chúng ta kiểm tra xem đối tượng **ToDoItem** được tạo ra từ dữ liệu form có đúng hay không.

### Bước 4: Hoàn thành tính năng thêm mục to-do

Khi bạn đã hoàn tất việc thêm các phương thức vào controller và xây dựng giao diện form, hãy khởi chạy ứng dụng và truy cập vào đường dẫn `/todo-list/add` trên trình duyệt. Khi người dùng nhập dữ liệu và nhấn Submit, mục to-do mới sẽ được thêm vào hệ thống và hiển thị trong danh sách.

### Kết luận

Trong video này, chúng ta đã tạo một form để người dùng thêm các mục **to-do** vào hệ thống bằng cách sử dụng thẻ **Spring Form**. Chúng ta đã thiết lập các phương thức trong **ToDoItemController** để hiển thị form và xử lý dữ liệu khi form được gửi. Chúng ta cũng đã sử dụng mô hình **Post-Redirect-Get** để đảm bảo rằng sau khi gửi form, người dùng được chuyển hướng đến trang danh sách mà không bị gửi lại form khi tải lại trang.

Trong các video tiếp theo, chúng ta sẽ tiếp tục xây dựng các tính năng như cập nhật và xóa mục to-do, cùng với các bước kiểm tra và tối ưu hóa ứng dụng.
