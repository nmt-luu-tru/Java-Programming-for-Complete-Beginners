Trong video này, chúng ta sẽ tạo lớp **ToDoData** để mô phỏng nguồn dữ liệu (data source) cho ứng dụng to-do list. Lớp này sẽ đại diện cho một cơ sở dữ liệu trong bộ nhớ (in-memory database), sử dụng **ArrayList** để lưu trữ các mục to-do.

### 1. Tạo lớp ToDoData

#### Bước 1: Tạo lớp ToDoData trong package `model`

Trước tiên, chúng ta sẽ tạo một lớp mới tên là **ToDoData** trong package `model`.

```java
package academy.learnprogramming.model;

import lombok.NonNull;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Iterator;
import java.util.List;

public class ToDoData {
    // Biến static để tạo ID tự động tăng
    private static int idValue = 1;

    // Danh sách các to-do items
    private final List<ToDoItem> items = new ArrayList<>();

    // Constructor mặc định
    public ToDoData() {
        // Thêm một số dữ liệu mẫu (dummy data)
        addItem(new ToDoItem("First", "First details", LocalDate.now()));
        addItem(new ToDoItem("Second", "Second details", LocalDate.now()));
        addItem(new ToDoItem("Third", "Third details", LocalDate.now()));
    }

    // Phương thức public để lấy danh sách các to-do items
    public List<ToDoItem> getItems() {
        return Collections.unmodifiableList(items);
    }

    // Thêm một to-do item vào danh sách
    public void addItem(@NonNull ToDoItem toAdd) {
        toAdd.setId(idValue++);
        items.add(toAdd);
    }

    // Xóa một to-do item khỏi danh sách dựa vào ID
    public void removeItem(int id) {
        Iterator<ToDoItem> itemIterator = items.iterator();

        while (itemIterator.hasNext()) {
            ToDoItem item = itemIterator.next();
            if (item.getId() == id) {
                itemIterator.remove();
                break;
            }
        }
    }

    // Lấy một to-do item dựa vào ID
    public ToDoItem getItem(int id) {
        for (ToDoItem item : items) {
            if (item.getId() == id) {
                return item;
            }
        }
        return null;
    }

    // Cập nhật một to-do item
    public void updateItem(@NonNull ToDoItem toUpdate) {
        Iterator<ToDoItem> itemIterator = items.iterator();

        while (itemIterator.hasNext()) {
            ToDoItem item = itemIterator.next();
            if (item.equals(toUpdate)) {
                itemIterator.set(toUpdate);
                break;
            }
        }
    }
}
```

### 2. Giải thích mã nguồn

- **idValue**: Một biến `static` để giữ giá trị ID duy nhất cho từng to-do item. ID sẽ tự động tăng mỗi khi một mục mới được thêm vào.
  
- **items**: Danh sách các to-do items được lưu trữ trong **ArrayList**. Biến này được đánh dấu là `final` để không thể thay đổi danh sách này từ bên ngoài lớp.

#### Phương thức **getItems()**

```java
public List<ToDoItem> getItems() {
    return Collections.unmodifiableList(items);
}
```

Phương thức này trả về danh sách các to-do items. Tuy nhiên, chúng ta trả về một danh sách không thể sửa đổi (unmodifiable) để đảm bảo rằng các lớp khác không thể thay đổi danh sách này trực tiếp.

#### Phương thức **addItem()**

```java
public void addItem(@NonNull ToDoItem toAdd) {
    toAdd.setId(idValue++);
    items.add(toAdd);
}
```

Phương thức này thêm một to-do item mới vào danh sách. Chúng ta sử dụng annotation `@NonNull` từ Lombok để đảm bảo rằng tham số **toAdd** không phải là null. Nếu null, Lombok sẽ ném ra một ngoại lệ **NullPointerException**.

#### Phương thức **removeItem()**

```java
public void removeItem(int id) {
    Iterator<ToDoItem> itemIterator = items.iterator();

    while (itemIterator.hasNext()) {
        ToDoItem item = itemIterator.next();
        if (item.getId() == id) {
            itemIterator.remove();
            break;
        }
    }
}
```

Phương thức này loại bỏ một mục khỏi danh sách dựa trên ID của nó. Chúng ta sử dụng **Iterator** để duyệt qua danh sách và xóa mục khi tìm thấy ID phù hợp.

#### Phương thức **getItem()**

```java
public ToDoItem getItem(int id) {
    for (ToDoItem item : items) {
        if (item.getId() == id) {
            return item;
        }
    }
    return null;
}
```

Phương thức này trả về một to-do item dựa trên ID của nó. Nếu không tìm thấy mục nào với ID tương ứng, nó sẽ trả về `null`.

#### Phương thức **updateItem()**

```java
public void updateItem(@NonNull ToDoItem toUpdate) {
    Iterator<ToDoItem> itemIterator = items.iterator();

    while (itemIterator.hasNext()) {
        ToDoItem item = itemIterator.next();
        if (item.equals(toUpdate)) {
            itemIterator.set(toUpdate);
            break;
        }
    }
}
```

Phương thức này cập nhật một to-do item trong danh sách. Nếu tìm thấy mục cần cập nhật, nó sẽ thay thế bằng mục mới.

### 3. Kết luận

Trong video này, chúng ta đã tạo lớp **ToDoData** để mô phỏng một cơ sở dữ liệu trong bộ nhớ cho ứng dụng **to-do list**. Chúng ta đã triển khai các thao tác CRUD cơ bản (Create, Read, Update, Delete) cho các mục to-do. Lớp này sẽ hoạt động như một nguồn dữ liệu tạm thời cho ứng dụng của chúng ta. Trong video tiếp theo, chúng ta sẽ tạo **controller** cho ứng dụng và hiển thị các to-do items trên trang web.

Hẹn gặp các bạn trong video tiếp theo, nơi chúng ta sẽ xây dựng **ToDoItemController** để xử lý yêu cầu từ phía người dùng.
