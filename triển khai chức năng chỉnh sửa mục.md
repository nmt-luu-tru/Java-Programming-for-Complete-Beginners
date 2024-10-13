Trong video này, chúng ta sẽ thảo luận và triển khai chức năng **chỉnh sửa mục** trong ứng dụng to-do list. Mục tiêu của chúng ta là cho phép người dùng chỉnh sửa các mục đã tồn tại như tiêu đề, mô tả, hoặc ngày tháng của mục. Để làm điều này, chúng ta sẽ thêm một cột **chỉnh sửa** (Edit) vào bảng hiển thị danh sách các mục và cho phép người dùng nhấn vào để chỉnh sửa một mục cụ thể.

### Các bước triển khai

#### Bước 1: Thêm tiêu đề **Edit** vào bảng trong file `items_list.jsp`
Chúng ta bắt đầu bằng cách mở file **items_list.jsp** và thêm tiêu đề cột **Edit** vào bảng, giữa các cột hiện tại là **Deadline** và **Delete**. Ngoài ra, chúng ta sẽ sửa một lỗi nhỏ với thẻ `<tr>` đã được đóng sai chỗ. Đây là mã nguồn:

```html
<tr>
    <th>Title</th>
    <th>Deadline</th>
    <th>Edit</th> <!-- Thêm cột Edit -->
    <th>Delete</th>
</tr>
```

#### Bước 2: Thêm liên kết chỉnh sửa (Edit) vào từng mục trong bảng
Tương tự như cách chúng ta đã tạo liên kết xóa (Delete), chúng ta sẽ sử dụng thẻ **`<c:url>`** để tạo liên kết **Edit**. Mã nguồn như sau:

```html
<!-- Thêm liên kết chỉnh sửa cho mỗi mục -->
<c:url var="editUrl" value="${mappings.EDIT_ITEM}">
    <c:param name="id" value="${item.id}" />
</c:url>
<td><a href="${editUrl}">Edit</a></td>
```

Ở đây, chúng ta tạo ra một URL chứa ID của mục và sử dụng biến **`editUrl`** để hiển thị liên kết chỉnh sửa.

#### Bước 3: Cập nhật Controller để hỗ trợ chỉnh sửa mục
Bây giờ chúng ta cần cập nhật lớp **ToDoItemController** để hỗ trợ chức năng chỉnh sửa mục. Thay vì tạo phương thức hoàn toàn mới cho việc chỉnh sửa, chúng ta sẽ sửa đổi phương thức **addEditItem** hiện có để xử lý cả việc thêm và chỉnh sửa mục. Chúng ta sẽ sử dụng ID của mục được truyền dưới dạng query parameter để xác định xem mục có tồn tại hay không và từ đó quyết định chỉnh sửa hay tạo mới.

```java
@GetMapping(Mappings.ADD_ITEM)
public String addEditItem(@RequestParam(value = "id", required = false, defaultValue = "-1") int id, Model model) {
    ToDoItem toDoItem;
    if (id == -1) {
        // Tạo mục mới nếu ID không tồn tại
        toDoItem = new ToDoItem("", "", LocalDate.now());
    } else {
        // Lấy mục từ service để chỉnh sửa
        toDoItem = toDoItemService.getItem(id);
        if (toDoItem == null) {
            toDoItem = new ToDoItem("", "", LocalDate.now());
        }
    }
    model.addAttribute(AttributeNames.TODO_ITEM, toDoItem);
    return ViewNames.ADD_ITEM;
}
```

Trong mã trên:
- **`@RequestParam(value = "id", required = false, defaultValue = "-1")`**: Chúng ta đánh dấu tham số **ID** là tùy chọn, với giá trị mặc định là **-1**. Nếu ID không được truyền, chúng ta tạo một mục mới.
- Nếu **ID** được truyền, chúng ta gọi **toDoItemService.getItem(id)** để lấy mục và hiển thị nó trong form.

#### Bước 4: Xử lý khi submit form (processItem)
Phương thức **processItem** sẽ cần sửa đổi để xử lý cả việc thêm mới và cập nhật mục hiện có. Chúng ta kiểm tra ID của mục: nếu là 0, đó là mục mới, ngược lại là chỉnh sửa mục.

```java
@PostMapping(Mappings.ADD_ITEM)
public String processItem(@ModelAttribute(AttributeNames.TODO_ITEM) ToDoItem toDoItem) {
    if (toDoItem.getId() == 0) {
        toDoItemService.addItem(toDoItem);
    } else {
        toDoItemService.updateItem(toDoItem);
    }
    return "redirect:/" + Mappings.ITEMS;
}
```

Trong mã này:
- Nếu **ID** của mục là **0**, chúng ta gọi **addItem** để thêm mới.
- Nếu không, chúng ta gọi **updateItem** để cập nhật mục.

#### Bước 5: Kiểm tra ứng dụng
Sau khi hoàn tất các bước trên, chúng ta có thể chạy ứng dụng để kiểm tra chức năng chỉnh sửa:
1. Truy cập trang **Items** để thấy cột **Edit** mới.
2. Nhấn vào liên kết **Edit** để chỉnh sửa mục và thay đổi tiêu đề hoặc ngày tháng.
3. Lưu lại và kiểm tra xem mục đã được chỉnh sửa thành công.

### Tổng kết
Chúng ta đã triển khai chức năng chỉnh sửa mục trong ứng dụng to-do list bằng cách thêm liên kết **Edit** vào bảng và cập nhật controller để xử lý cả việc thêm mới và chỉnh sửa. Trong video tiếp theo, chúng ta sẽ tiếp tục với chức năng xem chi tiết từng mục (View Item) và thảo luận về một thử thách để bạn có thể thực hành.
