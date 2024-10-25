### Khi Nào `WebApplicationInitializer` Được Khởi Chạy?

- **Khởi Động Khi Ứng Dụng Bắt Đầu**:
  - `WebApplicationInitializer` được khởi động tự động khi ứng dụng web của bạn khởi động trên một servlet container như Tomcat hoặc Jetty. Khi servlet container khởi động, nó sẽ quét các class trong ứng dụng để tìm các implementation của interface `WebApplicationInitializer`.

- **Không Cần Tệp `web.xml`**:
  - Với việc sử dụng `WebApplicationInitializer`, bạn không cần phải có tệp `web.xml` để cấu hình servlet hoặc context. Thay vào đó, tất cả các cấu hình đều nằm trong mã Java, làm cho việc quản lý và cấu hình trở nên linh hoạt và dễ dàng hơn.

### Vai Trò của `WebApplicationInitializer`

1. **Khởi Tạo Spring Application Context**: 
   - `WebApplicationInitializer` cho phép bạn tạo một `ApplicationContext` cho ứng dụng web. Điều này có nghĩa là bạn có thể định nghĩa các bean và cấu hình Spring mà không cần một tệp cấu hình XML.

2. **Đăng Ký Servlets**: 
   - Bạn có thể dễ dàng đăng ký các servlet như `DispatcherServlet` trong phương thức `onStartup()`. Điều này cho phép bạn xác định cách mà Spring sẽ xử lý các yêu cầu HTTP trong ứng dụng.

3. **Cấu Hình Chạy Ứng Dụng**: 
   - `WebApplicationInitializer` giúp tách biệt mã cấu hình từ mã ứng dụng, làm cho mã dễ đọc và bảo trì hơn.

### Hoạt Động của `WebApplicationInitializer`

- **Phương thức `onStartup(ServletContext servletContext)`**:
  - Đây là phương thức chính mà bạn sẽ ghi đè để thực hiện cấu hình cho ứng dụng web. Bên trong phương thức này, bạn có thể:
    - Tạo một `ApplicationContext` (ví dụ: `AnnotationConfigWebApplicationContext`).
    - Đăng ký servlet, filter, listener, hoặc bất kỳ thành phần nào khác cần thiết cho ứng dụng web của bạn.

### Ví Dụ

```java
@Slf4j
public class WebAppInitializer implements WebApplicationInitializer {
    @Override
    public void onStartup(ServletContext servletContext) throws ServletException {
        // Tạo Spring ApplicationContext
        AnnotationConfigWebApplicationContext context = new AnnotationConfigWebApplicationContext();
        context.register(WebConfig.class);

        // Tạo và đăng ký DispatcherServlet
        DispatcherServlet dispatcherServlet = new DispatcherServlet(context);
        ServletRegistration.Dynamic registration = servletContext.addServlet("dispatcher", dispatcherServlet);
        registration.setLoadOnStartup(1);
        registration.addMapping("/");
    }
}
```

- Trong ví dụ trên, khi ứng dụng được khởi động, `onStartup()` sẽ được gọi. Phương thức này sẽ tạo một `ApplicationContext`, đăng ký `DispatcherServlet`, và cấu hình nó để xử lý các yêu cầu đến ứng dụng.

### Kết Luận

- `WebApplicationInitializer` đóng vai trò quan trọng trong việc cấu hình và khởi tạo ứng dụng web Spring mà không cần `web.xml`.
- Nó cho phép bạn đăng ký các servlet, filters, và listeners một cách linh hoạt và dễ dàng.
- Phương thức `onStartup()` được gọi tự động khi servlet container khởi động ứng dụng, giúp thiết lập mọi thứ cần thiết cho hoạt động của ứng dụng.
