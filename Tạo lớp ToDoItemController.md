Trong video này, chúng ta sẽ tạo lớp **ToDoItemController** để xử lý các yêu cầu liên quan đến các mục to-do (to-do items) trong ứng dụng của chúng ta. Controller này sẽ chứa các phương thức yêu cầu để xem, xóa và quản lý các mục to-do. Trong video này, chúng ta sẽ bắt đầu bằng cách tạo lớp controller và sau đó, trong video tiếp theo, chúng ta sẽ tạo file JSP để hiển thị các mục trong một bảng HTML.

### Bước 1: Tạo lớp **ToDoItemController**

#### Tạo lớp controller trong package `controller`

```java
package academy.learnprogramming.controller;

import academy.learnprogramming.model.ToDoData;
import academy.learnprogramming.util.Mappings;
import academy.learnprogramming.util.ViewNames;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;

@Controller
public class ToDoItemController {

    // Phần này để định nghĩa model attributes
    @ModelAttribute
    public ToDoData toDoData() {
        return new ToDoData();
    }

    // Phương thức handler cho việc hiển thị tất cả các mục to-do
    @GetMapping(Mappings.ITEMS)
    public String items() {
        return ViewNames.ITEMS_LIST;
    }
}
```

### Giải thích mã nguồn

- **@Controller**: Đây là annotation định nghĩa lớp này là một controller của Spring.
  
- **@ModelAttribute**: Annotation này cho phép chúng ta thêm các thuộc tính (attributes) vào model. Trong ví dụ này, phương thức `toDoData()` sẽ cung cấp một instance của lớp **ToDoData** cho model.

- **@GetMapping**: Chúng ta sử dụng annotation này để ánh xạ các yêu cầu HTTP GET vào một phương thức cụ thể. Trong trường hợp này, URL `/items` sẽ được ánh xạ tới phương thức `items()`, trả về tên của view là `items_list`, được định nghĩa trong **ViewNames**.

### Bước 2: Sử dụng hằng số để quản lý các mappings và view names

Việc sử dụng hằng số (constants) giúp chúng ta dễ dàng duy trì và tránh lỗi trong quá trình phát triển, đặc biệt là khi có nhiều nơi sử dụng cùng một URL hay tên view.

#### Tạo lớp **Mappings**

Chúng ta sẽ tạo một lớp chứa các hằng số cho tất cả các mappings trong ứng dụng.

```java
package academy.learnprogramming.util;

public final class Mappings {

    // Constructor private để ngăn không cho lớp này bị khởi tạo
    private Mappings() {}

    // Hằng số cho URL /items
    public static final String ITEMS = "items";
}
```

#### Tạo lớp **ViewNames**

Tương tự như lớp **Mappings**, lớp **ViewNames** sẽ chứa hằng số cho tất cả các tên view.

```java
package academy.learnprogramming.util;

public final class ViewNames {

    // Constructor private để ngăn không cho lớp này bị khởi tạo
    private ViewNames() {}

    // Hằng số cho view items_list
    public static final String ITEMS_LIST = "items_list";
}
```

### Bước 3: Cập nhật **ToDoItemController** để sử dụng hằng số

Bây giờ chúng ta quay lại lớp **ToDoItemController** và cập nhật các phương thức để sử dụng các hằng số mà chúng ta vừa tạo.

```java
package academy.learnprogramming.controller;

import academy.learnprogramming.model.ToDoData;
import academy.learnprogramming.util.Mappings;
import academy.learnprogramming.util.ViewNames;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;

@Controller
public class ToDoItemController {

    // Định nghĩa model attribute
    @ModelAttribute
    public ToDoData toDoData() {
        return new ToDoData();
    }

    // Phương thức xử lý yêu cầu GET tới /items
    @GetMapping(Mappings.ITEMS)
    public String items() {
        return ViewNames.ITEMS_LIST;
    }
}
```

- **Mappings.ITEMS**: Đây là hằng số đại diện cho URL `/items`.
  
- **ViewNames.ITEMS_LIST**: Đây là hằng số đại diện cho tên của view `items_list`.

### Kết luận

Trong video này, chúng ta đã tạo lớp **ToDoItemController** để xử lý các yêu cầu liên quan đến các mục to-do. Chúng ta cũng đã tạo các lớp **Mappings** và **ViewNames** để quản lý các hằng số, giúp mã nguồn dễ duy trì và tránh lỗi. Trong video tiếp theo, chúng ta sẽ tạo file JSP để hiển thị các mục to-do trong một bảng HTML.

Hẹn gặp các bạn trong video tiếp theo!
