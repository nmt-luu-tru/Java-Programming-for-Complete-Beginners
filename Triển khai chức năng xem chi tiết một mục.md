Trong video này, chúng ta sẽ thực hiện một thử thách có tên **View Item Challenge**. Mục tiêu của thử thách là triển khai chức năng xem chi tiết một mục trong ứng dụng to-do list. Chúng ta sẽ đi qua từng bước để thực hiện.

### Các bước thực hiện:

#### 1. Tạo view `view_item.jsp`
Trước tiên, chúng ta cần tạo một file JSP mới có tên `view_item.jsp`. File này sẽ hiển thị thông tin chi tiết của một mục trong bảng HTML. Bên dưới bảng, chúng ta cần thêm một liên kết để điều hướng người dùng trở lại bảng chứa tất cả các mục (file `items_list.jsp`).

##### Các bước thực hiện:

- Mở **ViewNames** class và thêm hằng số cho view mới:

```java
public static final String VIEW_ITEM = "view_item";
```

- Sau đó, sao chép file **add_item.jsp** để tạo file **view_item.jsp**:

```jsp
<!-- Tạo file view_item.jsp -->
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ page import="com.example.util.Mappings" %>

<!DOCTYPE html>
<html>
<head>
    <title>View Item</title>
</head>
<body>
    <h2>To-Do Item Details</h2>
    <table>
        <tr>
            <td>ID:</td>
            <td><c:out value="${todoItem.id}"/></td>
        </tr>
        <tr>
            <td>Title:</td>
            <td><c:out value="${todoItem.title}"/></td>
        </tr>
        <tr>
            <td>Deadline:</td>
            <td><c:out value="${todoItem.deadline}"/></td>
        </tr>
        <tr>
            <td>Details:</td>
            <td><c:out value="${todoItem.details}"/></td>
        </tr>
    </table>

    <!-- Liên kết quay lại trang chính -->
    <c:url var="tableUrl" value="${Mappings.ITEMS}"/>
    <a href="${tableUrl}">Show Table</a>
</body>
</html>
```

Trong file JSP này:
- **`<c:out>`** được sử dụng để hiển thị giá trị của từng thuộc tính của mục to-do.
- **`c:url`** giúp tạo URL cho liên kết quay lại trang hiển thị tất cả các mục (`items_list.jsp`).

#### 2. Thêm liên kết **View** vào bảng trong file `items_list.jsp`
Tương tự như các liên kết **Edit** và **Delete**, chúng ta sẽ thêm một liên kết **View** để cho phép người dùng xem chi tiết của từng mục.

```jsp
<th>View</th>
<!-- Dòng này thêm vào các cột hiện có -->
<tr>
    <td>${item.title}</td>
    <td>${item.deadline}</td>
    <td>${item.details}</td>
    <td><a href="${viewUrl}">View</a></td>
    <td><a href="${editUrl}">Edit</a></td>
    <td><a href="${deleteUrl}">Delete</a></td>
</tr>
```

Liên kết **View** sẽ điều hướng người dùng đến trang chi tiết của mục, giống như cách chúng ta đã làm với **Edit** và **Delete**.

#### 3. Thêm phương thức `viewItem()` vào `TodoItemController`
Phương thức này sẽ nhận ID của mục cần xem và hiển thị nó trong view `view_item.jsp`. Chúng ta sẽ sử dụng **@RequestParam** để lấy ID từ URL và thêm mục đó vào mô hình (model) để truyền đến view.

```java
@GetMapping(Mappings.VIEW_ITEM)
public String viewItem(@RequestParam("id") int id, Model model) {
    // Lấy mục từ service
    ToDoItem todoItem = todoItemService.getItem(id);
    
    // Thêm mục vào model
    model.addAttribute(AttributeNames.TODO_ITEM, todoItem);
    
    // Trả về view
    return ViewNames.VIEW_ITEM;
}
```

Trong phương thức này:
- **`@RequestParam("id")`** lấy tham số ID từ URL.
- **`todoItemService.getItem(id)`** gọi phương thức để lấy mục từ service.
- Sau đó, chúng ta thêm mục vào model bằng cách sử dụng **model.addAttribute()**.

#### 4. Kiểm tra ứng dụng
Sau khi hoàn thành các bước trên, chúng ta cần kiểm tra xem chức năng đã hoạt động đúng hay chưa. Chạy ứng dụng và kiểm tra:
- Truy cập trang **Items** để thấy cột **View** mới.
- Nhấn vào liên kết **View** để xem chi tiết một mục.

### Tổng kết
Chúng ta đã hoàn thành việc triển khai chức năng **View Item** bằng cách thêm liên kết **View** vào bảng và tạo view để hiển thị chi tiết từng mục. Chúng ta cũng đã cập nhật controller để xử lý yêu cầu từ người dùng và hiển thị thông tin đúng cách. Trong video tiếp theo, chúng ta sẽ tiếp tục với phần triển khai chức năng **Spring Boot Two**.
