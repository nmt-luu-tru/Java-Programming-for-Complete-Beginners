Trong thử thách này, mục tiêu của chúng ta là triển khai chức năng **xóa mục** (delete item) mà chúng ta đã thảo luận trong video trước. Chúng ta sẽ tạo một phương thức trong lớp **ToDoItemController** với tên là `deleteItem`, được ánh xạ với URL để xóa mục. Chúng ta sẽ sử dụng **constant** từ lớp **Mappings** để đảm bảo sử dụng URL nhất quán. Phương thức này sẽ lấy một tham số **ID** kiểu `int` thông qua **@RequestParam**, sau đó gọi phương thức **removeItem** của service để thực hiện xóa mục và cuối cùng chuyển hướng người dùng trở lại trang danh sách các mục.

### Các bước triển khai

#### Bước 1: Mở lớp **ToDoItemController** và thêm phương thức `deleteItem`

Chúng ta sẽ thêm phương thức `deleteItem` vào cuối lớp **ToDoItemController**. Đây là mã nguồn chi tiết:

```java
@Controller
public class ToDoItemController {

    private final ToDoItemService toDoItemService;

    @Autowired
    public ToDoItemController(ToDoItemService toDoItemService) {
        this.toDoItemService = toDoItemService;
    }

    @GetMapping(Mappings.DELETE_ITEM)
    public String deleteItem(@RequestParam("id") int id) {
        // Ghi log việc xóa item
        log.info("Deleting item with ID = {}", id);

        // Gọi phương thức của service để xóa item
        toDoItemService.removeItem(id);

        // Chuyển hướng về trang danh sách item
        return "redirect:/" + Mappings.ITEMS;
    }
}
```

#### Diễn giải:

- **`@GetMapping(Mappings.DELETE_ITEM)`**: Chúng ta sử dụng annotation này để ánh xạ phương thức `deleteItem` tới URL xóa mục được định nghĩa trong lớp **Mappings**.
- **`@RequestParam("id") int id`**: Annotation này giúp lấy giá trị tham số **ID** từ URL. Đây là ID của mục cần xóa.
- **`log.info`**: Ghi thông tin log khi mục bị xóa, điều này giúp kiểm tra lại các hoạt động trong hệ thống.
- **`toDoItemService.removeItem(id)`**: Gọi phương thức trong lớp **ToDoItemService** để thực hiện xóa mục khỏi danh sách.
- **`return "redirect:/" + Mappings.ITEMS`**: Sau khi xóa xong, chúng ta chuyển hướng người dùng quay lại trang danh sách các mục.

#### Bước 2: Kiểm tra và chạy ứng dụng

Sau khi hoàn thành mã, hãy chạy lại ứng dụng và kiểm tra xem tính năng xóa có hoạt động đúng không. Hãy đảm bảo rằng khi bạn nhấn vào liên kết **delete** cho một mục cụ thể, mục đó sẽ biến mất khỏi danh sách và không còn xuất hiện nữa.

### Kiểm tra trong trình duyệt

Khi chúng ta chạy ứng dụng, mở trình duyệt và truy cập trang danh sách các mục. Bây giờ bạn có thể nhấn vào liên kết **delete** để xóa một mục cụ thể.

Ví dụ:
1. Nhấn vào nút **delete** cho mục thứ hai.
2. Trang sẽ làm mới và bạn sẽ thấy mục đó không còn trong danh sách.
3. Bạn cũng có thể kiểm tra các log trong IntelliJ để đảm bảo rằng mục đã được xóa thành công.

### Kiểm tra log trong IntelliJ

Sau khi thực hiện xóa, bạn có thể kiểm tra log trong IntelliJ để đảm bảo rằng hệ thống đã ghi nhận việc xóa đúng cách.

Ví dụ về log:
```
INFO  - Deleting item with ID = 2
INFO  - Deleting item with ID = 4
```

### Tổng kết

Chúng ta đã hoàn thành thử thách xóa mục bằng cách tạo phương thức `deleteItem` trong **ToDoItemController**. Phương thức này sử dụng **@RequestParam** để lấy ID của mục cần xóa, gọi phương thức **removeItem** từ service, và sau đó chuyển hướng người dùng trở lại trang danh sách các mục. Hãy đảm bảo rằng bạn kiểm tra lại tính năng bằng cách thử xóa các mục và kiểm tra log để đảm bảo mọi thứ hoạt động đúng cách.

Hẹn gặp bạn trong video tiếp theo, nơi chúng ta sẽ tiếp tục với tính năng **chỉnh sửa mục** (edit item).
