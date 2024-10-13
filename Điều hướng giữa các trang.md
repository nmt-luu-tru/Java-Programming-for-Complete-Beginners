Trong video này, chúng ta sẽ thảo luận về cách tạo trang chủ (**home view**) và triển khai điều hướng giữa các trang (**views**) bằng cách sử dụng các liên kết (**hyperlinks**). Đầu tiên, chúng ta sẽ tạo trang chủ và sau đó sẽ thêm các liên kết để điều hướng giữa các trang JSP trong ứng dụng của chúng ta. 

### Điều hướng giữa các trang

Khi nói về **views**, chúng ta đề cập đến các file JSP. Hiện tại, chúng ta đã tạo hai view là **items** và **add_item**. Trang **items** là nơi hiển thị danh sách các mục to-do dưới dạng bảng. Trong video này, chúng ta sẽ tạo thêm **home view** và sau này sẽ tạo **view_item** để hiển thị chi tiết của một mục to-do. 

Về cơ bản, **home view** sẽ có liên kết tới trang **items**, nơi hiển thị danh sách các mục to-do. Từ **items view**, chúng ta sẽ có liên kết tới trang **add_item**, nơi người dùng có thể thêm mục to-do mới mà không cần nhập URL thủ công. Sau cùng, **view_item** sẽ hiển thị chi tiết của một mục cụ thể và cung cấp liên kết quay lại bảng danh sách.

### Bước 1: Tạo **Home View**

Trước tiên, chúng ta sẽ tạo **home.jsp**. Bạn có thể sao chép file **items_list.jsp** và đổi tên thành **home.jsp**. Sau đó, chúng ta sẽ chỉnh sửa nội dung để phù hợp với mục đích của trang chủ.

```jsp
<%@ page import="Academy.learnprogramming.util.Mappings" %>
<html>
<head>
    <title>To-Do List Application</title>
</head>
<body>
    <div align="center">
        <h2>To-Do List Application</h2>
        <c:url var="itemsLink" value="${Mappings.items}" />
        <a href="${itemsLink}">Show To-Do Items</a>
    </div>
</body>
</html>
```

### Diễn giải:
- **`c:url`**: Sử dụng thẻ JSTL để tạo URL từ biến **itemsLink**, liên kết đến trang danh sách các mục to-do.
- **Liên kết**: Chúng ta tạo một liên kết HTML với văn bản hiển thị là **"Show To-Do Items"** để điều hướng đến trang danh sách mục.

### Bước 2: Đăng ký **Home View** mà không cần Controller

Vì **home view** chỉ là nội dung tĩnh với một liên kết đơn giản, chúng ta không cần thêm logic trong controller. Thay vào đó, chúng ta có thể sử dụng **view controller** để định tuyến trang mà không cần tạo một phương thức controller.

Trong file cấu hình Spring, chúng ta sẽ thêm phương thức **addViewControllers** để đăng ký trang chủ.

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName(ViewNames.HOME);
    }
}
```

- **`addViewControllers`**: Phương thức này cho phép đăng ký một trang JSP mà không cần thêm controller, giúp đơn giản hóa việc hiển thị các trang tĩnh.

### Bước 3: Cập nhật các constants trong **ViewNames**

Chúng ta cần thêm một constant mới trong lớp **ViewNames** để đại diện cho **home.jsp**.

```java
public class ViewNames {
    public static final String HOME = "home";
    public static final String ITEMS = "items";
    public static final String ADD_ITEM = "add_item";
    // Các constants khác
}
```

### Bước 4: Thêm liên kết trong **Items View**

Trong file **items_list.jsp**, chúng ta sẽ thêm các liên kết điều hướng tới trang thêm mục to-do và trang xóa mục. Đầu tiên, chúng ta cần nhập lớp **Mappings** để sử dụng các URL constants.

```jsp
<%@ page import="Academy.learnprogramming.util.Mappings" %>
<html>
<head>
    <title>To-Do Items</title>
</head>
<body>
    <div align="center">
        <h2>To-Do Items</h2>
        <c:url var="addURL" value="${Mappings.add_item}" />
        <a href="${addURL}">New Item</a>
        <table border="1">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Deadline</th>
                    <th>Delete</th>
                </tr>
            </thead>
            <tbody>
                <c:forEach var="item" items="${todoData.items}">
                    <tr>
                        <td>${item.title}</td>
                        <td>${item.deadline}</td>
                        <td>
                            <c:url var="deleteURL" value="${Mappings.delete_item}">
                                <c:param name="id" value="${item.id}" />
                            </c:url>
                            <a href="${deleteURL}">Delete</a>
                        </td>
                    </tr>
                </c:forEach>
            </tbody>
        </table>
    </div>
</body>
</html>
```

### Diễn giải:
- **Liên kết "New Item"**: Tạo một liên kết tới trang **add_item.jsp** để thêm mục mới.
- **Liên kết "Delete"**: Tạo liên kết tới hành động xóa mục, sử dụng **c:param** để truyền **id** của mục cần xóa vào URL.

### Bước 5: Kiểm tra và Chạy Ứng Dụng

Cuối cùng, bạn có thể chạy ứng dụng và kiểm tra điều hướng giữa các trang:
- Truy cập **/home** sẽ hiển thị trang chủ với liên kết đến danh sách mục.
- Từ trang danh sách mục, bạn có thể điều hướng đến trang thêm mục mới hoặc xóa một mục cụ thể.

### Kết luận

Trong video này, chúng ta đã tạo **home view** và triển khai điều hướng giữa các trang JSP trong ứng dụng của mình bằng cách sử dụng các liên kết. Chúng ta đã học cách sử dụng **view controllers** để đăng ký các trang tĩnh mà không cần thêm controller. Điều này giúp đơn giản hóa việc điều hướng và xây dựng ứng dụng một cách rõ ràng và dễ quản lý.
