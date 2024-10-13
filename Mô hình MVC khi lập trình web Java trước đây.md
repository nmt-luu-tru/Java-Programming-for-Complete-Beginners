Việc chỉ sử dụng **JSP (JavaServer Pages)**, **Servlet**, cùng với các công cụ hỗ trợ như **HTML**, **CSS**, và **cơ sở dữ liệu** vẫn hoàn toàn có thể xây dựng dự án trên mô hình **MVC (Model-View-Controller)**. Trước khi các framework hiện đại như **Spring MVC** xuất hiện, mô hình **MVC** đã được áp dụng rộng rãi bằng cách kết hợp **JSP** và **Servlet**. Hãy cùng tìm hiểu cách mô hình **MVC** có thể được thực hiện trong một dự án chỉ với các công nghệ này:

### 1. **Mô hình MVC là gì?**
Mô hình **MVC** tách biệt ứng dụng web thành ba phần chính:
- **Model**: Chịu trách nhiệm quản lý dữ liệu và logic nghiệp vụ. Model thường tương tác với cơ sở dữ liệu để lấy dữ liệu hoặc lưu trữ dữ liệu.
- **View**: Hiển thị thông tin cho người dùng, thường dưới dạng HTML. Trong bối cảnh Java web, **JSP** đóng vai trò làm **View**.
- **Controller**: Nhận các yêu cầu từ người dùng, xử lý yêu cầu đó (bằng cách gọi Model) và quyết định View nào sẽ được trả về cho người dùng. Trong trường hợp này, **Servlet** thường đóng vai trò là **Controller**.

### 2. **Cách triển khai MVC với JSP và Servlet**

#### a. **Model**
- **Model** chịu trách nhiệm quản lý dữ liệu, xử lý logic nghiệp vụ và tương tác với cơ sở dữ liệu. Model thường là các lớp Java đơn giản hoặc DAO (Data Access Object) để thực hiện việc kết nối và thao tác với cơ sở dữ liệu.
- Model không bao gồm mã hiển thị giao diện (HTML), mà tập trung vào xử lý dữ liệu và logic.

Ví dụ về Model xử lý dữ liệu:

```java
public class Product {
    private int id;
    private String name;
    private double price;

    // Constructor, getter và setter...
}

public class ProductDAO {
    public List<Product> getAllProducts() {
        // Kết nối và lấy dữ liệu từ cơ sở dữ liệu
        List<Product> products = new ArrayList<>();
        // ... thêm logic lấy dữ liệu từ cơ sở dữ liệu
        return products;
    }
}
```

#### b. **Controller (Servlet)**
- **Servlet** đóng vai trò là **Controller**, xử lý các yêu cầu HTTP từ phía người dùng. Controller sẽ gọi **Model** để xử lý logic, lấy dữ liệu cần thiết và sau đó chuyển tiếp dữ liệu này đến **View (JSP)** để hiển thị cho người dùng.
- Controller nhận yêu cầu từ trình duyệt, xử lý chúng và quyết định kết quả nào sẽ trả về cho người dùng.

Ví dụ về Servlet đóng vai trò Controller:

```java
@WebServlet("/products")
public class ProductController extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Tạo đối tượng model (ProductDAO) và lấy danh sách sản phẩm
        ProductDAO productDAO = new ProductDAO();
        List<Product> products = productDAO.getAllProducts();

        // Đặt danh sách sản phẩm vào request attribute để JSP có thể hiển thị
        request.setAttribute("products", products);

        // Chuyển tiếp request đến trang JSP để hiển thị kết quả
        RequestDispatcher dispatcher = request.getRequestDispatcher("products.jsp");
        dispatcher.forward(request, response);
    }
}
```

#### c. **View (JSP)**
- **JSP** đóng vai trò là **View**, hiển thị dữ liệu mà **Controller** gửi đến người dùng dưới dạng HTML. Trong JSP, bạn có thể sử dụng các thẻ như **JSTL** hoặc mã Java nhúng để hiển thị dữ liệu động từ request.

Ví dụ về trang **JSP** (products.jsp) để hiển thị danh sách sản phẩm:

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<head>
    <title>Danh sách sản phẩm</title>
</head>
<body>
    <h1>Danh sách sản phẩm</h1>
    <table border="1">
        <tr>
            <th>ID</th>
            <th>Tên</th>
            <th>Giá</th>
        </tr>
        <c:forEach var="product" items="${products}">
            <tr>
                <td>${product.id}</td>
                <td>${product.name}</td>
                <td>${product.price}</td>
            </tr>
        </c:forEach>
    </table>
</body>
</html>
```

### 3. **Dòng chảy xử lý trong MVC (sử dụng JSP và Servlet)**

1. **Người dùng gửi yêu cầu HTTP**: Khi người dùng truy cập vào **`/products`**, yêu cầu được gửi đến **Controller (Servlet)**.
2. **Controller xử lý yêu cầu**: **Servlet** nhận yêu cầu này, gọi các lớp **Model** (trong trường hợp này là **ProductDAO**) để lấy dữ liệu từ cơ sở dữ liệu.
3. **Controller chuyển tiếp dữ liệu đến View**: Sau khi lấy dữ liệu từ **Model**, **Servlet** đặt dữ liệu vào **request** và chuyển tiếp yêu cầu đến **View (JSP)**.
4. **View hiển thị dữ liệu**: **JSP** nhận dữ liệu từ **request** và hiển thị chúng cho người dùng dưới dạng HTML.

### 4. **Ưu và nhược điểm của mô hình này**

#### **Ưu điểm:**
- **Đơn giản và dễ hiểu**: Việc sử dụng **Servlet** và **JSP** theo mô hình **MVC** giúp tách biệt các phần khác nhau của ứng dụng, giúp việc phát triển và bảo trì dễ dàng hơn.
- **Kiểm soát tốt quy trình**: Bạn có thể kiểm soát rõ ràng cách các yêu cầu được xử lý, cách dữ liệu được quản lý, và cách nó được hiển thị.

#### **Nhược điểm:**
- **Thiếu linh hoạt và dễ mở rộng**: Khi dự án lớn lên, việc quản lý và bảo trì mã nguồn trở nên khó khăn do mã xử lý và hiển thị có thể trộn lẫn nhau (nhất là với các dự án sử dụng nhiều mã Java trong JSP).
- **Không có hỗ trợ mạnh mẽ như các framework hiện đại**: Các framework như **Spring MVC** cung cấp các tính năng mạnh mẽ hơn như quản lý session, hỗ trợ RESTful API, injection phụ thuộc (DI), AOP, và nhiều tính năng khác mà việc chỉ sử dụng **Servlet** và **JSP** không có.

### 5. **Tổng kết**
Việc chỉ sử dụng **JSP**, **Servlet**, và các công cụ hỗ trợ cơ bản (HTML, CSS, cơ sở dữ liệu) **hoàn toàn có thể triển khai mô hình MVC**. Tuy nhiên, với sự phát triển của các framework hiện đại như **Spring MVC**, việc áp dụng MVC trở nên mạnh mẽ, dễ mở rộng và bảo trì hơn nhiều, đặc biệt là trong các dự án lớn.
