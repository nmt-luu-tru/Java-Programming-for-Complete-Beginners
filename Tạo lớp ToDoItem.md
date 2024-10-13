Trong video này, chúng ta sẽ cùng tạo lớp **ToDoItem** để đại diện cho một nhiệm vụ trong ứng dụng **to-do list** của chúng ta. Lớp này sẽ bao gồm các thuộc tính như **ID**, **title**, **details**, và **deadline**. Chúng ta cũng sẽ tìm hiểu cách sử dụng thư viện Lombok để giảm thiểu việc viết mã lặp lại (boilerplate code).

### Tạo lớp ToDoItem

#### 1. Tạo package và lớp ToDoItem
Chúng ta sẽ bắt đầu bằng cách tạo một package mới gọi là **model** trong project của bạn, sau đó tạo lớp **ToDoItem** bên trong package đó.

- **Package**: `academy.learnprogramming.model`
- **Lớp**: `ToDoItem`

```java
package academy.learnprogramming.model;

import java.time.LocalDate;

public class ToDoItem {
    // Các trường dữ liệu
    private int id;
    private String title;
    private String details;
    private LocalDate deadline;

    // Constructor không bao gồm ID
    public ToDoItem(String title, String details, LocalDate deadline) {
        this.title = title;
        this.details = details;
        this.deadline = deadline;
    }

    // Getter và Setter (sẽ sử dụng Lombok ở phần sau)
}
```

#### 2. Sử dụng Lombok để giảm mã lặp lại
Thay vì tạo thủ công các phương thức **getter**, **setter**, **equals**, **hashCode**, và **toString**, chúng ta sẽ sử dụng **Lombok** để tự động sinh ra các phương thức này. Điều này giúp giảm lượng mã cần viết và duy trì.

##### Thêm phụ thuộc Lombok vào `pom.xml`
Nếu chưa có Lombok trong dự án của bạn, hãy thêm Lombok vào file `pom.xml`:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
    <scope>provided</scope>
</dependency>
```

##### Sử dụng Lombok trong lớp ToDoItem
Sau khi thêm Lombok, chúng ta sẽ thêm annotation `@Data` và `@EqualsAndHashCode` để Lombok tự động tạo các phương thức cần thiết:

```java
import lombok.Data;
import lombok.EqualsAndHashCode;
import java.time.LocalDate;

@Data
@EqualsAndHashCode(of = "id")  // Sử dụng ID để so sánh các đối tượng
public class ToDoItem {
    private int id;
    private String title;
    private String details;
    private LocalDate deadline;

    public ToDoItem(String title, String details, LocalDate deadline) {
        this.title = title;
        this.details = details;
        this.deadline = deadline;
    }
}
```

- **@Data**: Annotation này bao gồm các phương thức **getter**, **setter**, **equals**, **hashCode**, và **toString**.
- **@EqualsAndHashCode(of = "id")**: Chỉ sử dụng trường **id** để so sánh hai đối tượng khi thực hiện phương thức `equals()` và `hashCode()`.

### Kết quả
Với Lombok, chúng ta chỉ cần viết khoảng **20 dòng mã**, thay vì khoảng **80 dòng mã** nếu viết thủ công các phương thức getter, setter, equals, hashCode, và toString.

Khi mở phần **Structure** trong IntelliJ, bạn sẽ thấy Lombok đã tự động tạo các phương thức tương ứng, giúp code trở nên gọn gàng hơn.

---

### Tổng kết
Chúng ta đã tạo lớp **ToDoItem** đại diện cho nhiệm vụ trong ứng dụng **to-do list** của mình. Sử dụng **Lombok** đã giúp chúng ta loại bỏ phần lớn mã lặp lại, làm cho việc phát triển nhanh hơn và dễ bảo trì hơn. Trong các video tiếp theo, chúng ta sẽ tiếp tục xây dựng các lớp khác để mô phỏng nguồn dữ liệu và hoàn thiện ứng dụng.

Hẹn gặp lại các bạn trong video tiếp theo, nơi chúng ta sẽ tạo lớp tiếp theo để mô phỏng nguồn dữ liệu (data source).
