Phương thức **`addMapping()`** trong Java Servlet API được sử dụng để chỉ định các URL pattern mà servlet sẽ chịu trách nhiệm xử lý. Bạn có thể sử dụng các URL pattern khác nhau tùy thuộc vào cách bạn muốn servlet xử lý các yêu cầu.

Dưới đây là một số ví dụ thêm về cách sử dụng **`addMapping()`**:

### 1. **Mapping theo một đường dẫn cụ thể**

Nếu bạn chỉ muốn servlet xử lý các yêu cầu cho một đường dẫn cụ thể, bạn có thể sử dụng một URL cụ thể như sau:

```java
registration.addMapping("/home");
```

- **Mô tả:** Servlet này sẽ chỉ xử lý các yêu cầu đến URL `http://localhost:8080/home`.
- **Ví dụ:** Khi người dùng truy cập `http://localhost:8080/home`, servlet này sẽ được gọi. Nhưng các URL khác như `http://localhost:8080/about` sẽ không được servlet này xử lý.

### 2. **Mapping theo tiền tố đường dẫn (path prefix)**

Nếu bạn muốn servlet xử lý tất cả các yêu cầu bắt đầu với một tiền tố cụ thể, bạn có thể sử dụng ký tự đại diện `"/*"`:

```java
registration.addMapping("/api/*");
```

- **Mô tả:** Servlet này sẽ xử lý tất cả các yêu cầu có đường dẫn bắt đầu bằng `/api/`.
- **Ví dụ:** Các URL như `http://localhost:8080/api/users` hoặc `http://localhost:8080/api/products` sẽ được servlet này xử lý. Tuy nhiên, các URL khác như `http://localhost:8080/home` sẽ không được xử lý bởi servlet này.

### 3. **Mapping theo phần mở rộng tệp (file extension mapping)**

Bạn có thể chỉ định servlet xử lý các yêu cầu có phần mở rộng tệp cụ thể (ví dụ: `.html`, `.do`, `.action`):

```java
registration.addMapping("*.html");
```

- **Mô tả:** Servlet này sẽ xử lý tất cả các yêu cầu có phần mở rộng `.html`.
- **Ví dụ:** Các URL như `http://localhost:8080/home.html` hoặc `http://localhost:8080/about.html` sẽ được servlet này xử lý, nhưng các URL như `http://localhost:8080/home.jsp` hoặc `http://localhost:8080/contact.do` sẽ không được xử lý.

### 4. **Mapping tất cả các yêu cầu**

Nếu bạn muốn servlet xử lý mọi yêu cầu đến ứng dụng, bạn có thể sử dụng ký tự đại diện `"/*"`:

```java
registration.addMapping("/*");
```

- **Mô tả:** Servlet này sẽ xử lý tất cả các yêu cầu đến bất kỳ URL nào trong ứng dụng.
- **Ví dụ:** Bất kỳ URL nào như `http://localhost:8080/home`, `http://localhost:8080/products`, hoặc `http://localhost:8080/api/users` đều sẽ được servlet này xử lý.

### 5. **Mapping với sự kết hợp giữa tiền tố và phần mở rộng**

Bạn cũng có thể kết hợp tiền tố đường dẫn và phần mở rộng tệp:

```java
registration.addMapping("/admin/*.do");
```

- **Mô tả:** Servlet này sẽ xử lý tất cả các yêu cầu có đường dẫn bắt đầu với `/admin/` và kết thúc bằng `.do`.
- **Ví dụ:** Các URL như `http://localhost:8080/admin/create.do` hoặc `http://localhost:8080/admin/delete.do` sẽ được xử lý, nhưng các URL như `http://localhost:8080/user/login.do` hoặc `http://localhost:8080/admin/view.html` sẽ không được servlet này xử lý.

### 6. **Mapping với pattern cụ thể cho RESTful API**

Trong ứng dụng RESTful, bạn có thể sử dụng các pattern cụ thể như sau:

```java
registration.addMapping("/api/v1/*");
```

- **Mô tả:** Servlet này sẽ xử lý tất cả các yêu cầu liên quan đến phiên bản 1 của API (`/api/v1/`).
- **Ví dụ:** Các URL như `http://localhost:8080/api/v1/products` hoặc `http://localhost:8080/api/v1/users/123` sẽ được xử lý, nhưng các URL khác như `http://localhost:8080/api/v2/products` sẽ không được xử lý.

### Tổng kết:

- **`"/home"`:** Chỉ xử lý URL cụ thể `/home`.
- **`"/api/*"`:** Xử lý tất cả các yêu cầu bắt đầu bằng `/api/`.
- **`"*.html"`:** Xử lý các yêu cầu có phần mở rộng `.html`.
- **`"/*"`:** Xử lý tất cả các yêu cầu trong ứng dụng.
- **`"/admin/*.do"`:** Xử lý các yêu cầu bắt đầu bằng `/admin/` và kết thúc bằng `.do`.

Tùy thuộc vào nhu cầu của bạn, bạn có thể sử dụng các kiểu mapping này để điều khiển cách servlet của bạn xử lý các yêu cầu HTTP.
