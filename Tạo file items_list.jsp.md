Trong video này, chúng ta sẽ thảo luận về thẻ JSTL (JavaServer Pages Standard Tag Library) và cách sử dụng chúng trong file JSP để hiển thị dữ liệu dưới dạng bảng. Ngoài ra, chúng ta sẽ tạo file JSP để hiển thị danh sách các mục to-do trong bảng HTML.

### JSTL là gì?
JSTL là tập hợp các thẻ JSP hữu ích, giúp giảm thiểu việc phải viết mã Java trong file JSP. JSTL hỗ trợ các tác vụ phổ biến như lặp (iteration), điều kiện (conditionals), thao tác với tài liệu XML, và các thẻ SQL.

Các thẻ chính của JSTL bao gồm:
1. **Cơ bản (Core tags)**: Dùng để lặp và hiển thị dữ liệu.
2. **Định dạng (Formatting tags)**: Dùng để định dạng dữ liệu như số, ngày, thời gian.
3. **Thẻ SQL**: Dùng để thao tác với cơ sở dữ liệu SQL.
4. **Thẻ XML**: Dùng để thao tác với tài liệu XML.

Trong video này, chúng ta sẽ tập trung vào **Core tags**, bao gồm:
- **<c:forEach>**: Dùng để lặp qua một danh sách.
- **<c:out>**: Dùng để hiển thị dữ liệu.
- **<c:url>**: Dùng để tạo và định dạng URL.

### Bước 1: Thêm phụ thuộc JSTL vào `pom.xml`

Trước khi sử dụng JSTL, chúng ta cần thêm thư viện JSTL vào file `pom.xml`.

```xml
<properties>
    <jstl.version>1.2</jstl.version>
</properties>

<dependencies>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>${jstl.version}</version>
    </dependency>
</dependencies>
```

### Bước 2: Tạo file `items_list.jsp`

Chúng ta sẽ tạo một file JSP trong thư mục `WEB-INF/view` để hiển thị danh sách các mục to-do. File này sẽ sử dụng thẻ JSTL để lặp qua danh sách các mục và hiển thị chúng trong bảng HTML.

#### Tạo file `items_list.jsp`
Sao chép file `welcome.jsp` và đổi tên thành `items_list.jsp`.

#### Cập nhật file `items_list.jsp`
Dưới đây là mã nguồn của file `items_list.jsp`:

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>To-Do Items</title>
</head>
<body>
    <div align="center">
        <h2>To-Do Items</h2>
        <table border="1" cellpadding="5">
            <caption>To-Do List</caption>
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Deadline</th>
                </tr>
            </thead>
            <tbody>
                <c:forEach var="item" items="${toDoData.items}">
                    <tr>
                        <td><c:out value="${item.title}" /></td>
                        <td><c:out value="${item.deadline}" /></td>
                    </tr>
                </c:forEach>
            </tbody>
        </table>
    </div>
</body>
</html>
```

### Giải thích mã nguồn:
1. **Import thư viện JSTL**: Dòng đầu tiên `taglib` cho phép chúng ta sử dụng các thẻ JSTL trong file JSP.
   
2. **Cấu trúc bảng**: Chúng ta tạo bảng HTML với các cột `Title` và `Deadline`.

3. **Sử dụng thẻ `<c:forEach>`**: Chúng ta sử dụng thẻ `<c:forEach>` để lặp qua danh sách các mục to-do từ `toDoData.items`. Mỗi mục trong danh sách sẽ được hiển thị dưới dạng một dòng trong bảng.

4. **Sử dụng thẻ `<c:out>`**: Thẻ này được dùng để hiển thị giá trị của từng trường `title` và `deadline` trong danh sách các mục.

### Bước 3: Chạy ứng dụng

Bây giờ, chúng ta có thể chạy ứng dụng và kiểm tra xem bảng các mục to-do có hiển thị chính xác không.

1. Khởi động cấu hình Maven bằng cách chạy `cargo:run`.
2. Mở trình duyệt và truy cập vào URL `http://localhost:8080/todo-list/items`.

Nếu mọi thứ hoạt động đúng, bạn sẽ thấy bảng hiển thị các mục to-do.

### Kết luận:
Trong video này, chúng ta đã tìm hiểu về cách sử dụng các thẻ JSTL để hiển thị danh sách các mục to-do trong bảng HTML. Chúng ta đã sử dụng thẻ `<c:forEach>` để lặp qua danh sách và thẻ `<c:out>` để hiển thị dữ liệu. Ứng dụng đã thành công hiển thị danh sách các mục to-do dưới dạng bảng trong trình duyệt.

Hẹn gặp các bạn trong video tiếp theo, nơi chúng ta sẽ thực hiện một thử thách để củng cố kiến thức vừa học!
