Trong video này, chúng ta đã thảo luận về việc thiết lập **Spring MVC Dispatcher Servlet** sử dụng cấu hình Java, thay vì dùng tệp cấu hình XML truyền thống. Đây là bước đầu tiên để xây dựng một ứng dụng web bằng Spring MVC. Chúng ta sẽ tìm hiểu cách Dispatcher Servlet hoạt động và làm thế nào để cấu hình nó trong ứng dụng web. Dưới đây là phần tóm tắt chi tiết hơn dựa trên nội dung bạn cung cấp.

### 1. Spring MVC Dispatcher Servlet là gì?

**Dispatcher Servlet** là "front controller" trong mô hình Spring MVC. Nó chịu trách nhiệm xử lý các yêu cầu HTTP và chuyển hướng chúng đến các thành phần khác trong hệ thống, như các controller, service, hoặc view để xử lý dữ liệu và phản hồi lại cho người dùng. **Dispatcher Servlet** thực hiện vai trò trung tâm, giúp quản lý luồng dữ liệu trong ứng dụng web dựa trên mô hình **Model-View-Controller (MVC)**. 

### 2. Cách đăng ký Servlet trong Spring MVC:

Có hai cách để đăng ký Dispatcher Servlet trong ứng dụng Spring MVC:
- **Sử dụng XML-based configuration**: Đây là cách truyền thống, sử dụng tệp `web.xml` để cấu hình servlet.
- **Sử dụng Java-based configuration**: Đây là cách hiện đại hơn, cho phép cấu hình servlet bằng mã Java mà không cần dùng `web.xml`.

Vì Spring khuyến khích sử dụng cấu hình bằng Java, chúng ta sẽ chọn cách tiếp cận này để cấu hình **Dispatcher Servlet**.

### 3. Cấu hình Dispatcher Servlet bằng Java:

#### Bước 1: Tạo lớp cấu hình Web (`WebConfig`)

Để cấu hình các thành phần web của ứng dụng, chúng ta tạo một lớp Java có tên là `WebConfig`. Lớp này sẽ chứa các thông tin cấu hình cần thiết để Spring MVC hoạt động.

- **`@Configuration`**: Đây là annotation của Spring để đánh dấu rằng `WebConfig` là một lớp cấu hình.
- **`@ComponentScan`**: Chỉ định các package mà Spring cần quét để tìm các bean và các thành phần khác như controller, service, repository. Trong trường hợp này, chúng ta chỉ định package gốc là `academy.learnprogramming`.
- **`@EnableWebMvc`**: Kích hoạt các cấu hình mặc định của Spring MVC, bao gồm việc hỗ trợ các bean liên quan đến Spring MVC như `RequestMappingHandler`, `ViewResolver`, v.v.

```java
@Configuration
@ComponentScan(basePackages = "academy.learnprogramming")
@EnableWebMvc
public class WebConfig {
    // Các cấu hình web sẽ được thêm vào đây.
}
```

#### Bước 2: Thêm phụ thuộc Servlet API vào `pom.xml`

Vì chúng ta đang làm việc với servlet, cần phải thêm phụ thuộc Servlet API vào dự án. Chúng ta sử dụng phiên bản servlet API 3.1 và thiết lập `scope` là **provided**. Điều này có nghĩa là thư viện này sẽ được cung cấp bởi Tomcat khi ứng dụng chạy, do đó chúng ta không cần đóng gói thư viện này trong file WAR.

```xml
<properties>
    <servlet-api.version>3.1.0</servlet-api.version>
</properties>

<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>${servlet-api.version}</version>
    <scope>provided</scope>
</dependency>
```

#### Bước 3: Đăng ký Dispatcher Servlet thông qua lớp `WebAppInitializer`

Tiếp theo, chúng ta tạo một lớp có tên `WebAppInitializer` để đăng ký **Dispatcher Servlet** bằng cách sử dụng interface **`WebApplicationInitializer`**. Khi implement interface này, chúng ta sẽ ghi đè phương thức `onStartup()`, nơi chúng ta sẽ thực hiện các thao tác khởi tạo servlet. 

- **Tạo Spring ApplicationContext**: Chúng ta sử dụng `AnnotationConfigWebApplicationContext` để tạo context cho ứng dụng. Context này sẽ đọc các cấu hình từ lớp `WebConfig`.
- **Tạo và đăng ký DispatcherServlet**: Chúng ta tạo đối tượng `DispatcherServlet` và đăng ký nó với `ServletContext`. Cuối cùng, chúng ta thiết lập URL pattern cho servlet (ở đây là `"/"`), để servlet này xử lý tất cả các yêu cầu đến ứng dụng.

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
[Vai Trò của WebApplicationInitializer](https://github.com/nmt-luu-tru/Java-Programming-for-Complete-Beginners/blob/main/Vai%20Tr%C3%B2%20c%E1%BB%A7a%20WebApplicationInitializer.md)  
[Giải thích đoạn mã về **registration** ở trên](https://github.com/nmt-luu-tru/Java-Programming-for-Complete-Beginners/blob/main/Gi%E1%BA%A3i%20th%C3%ADch%20v%E1%BB%81%20%60registration%60%20%E1%BB%9F%20tr%C3%AAn.md)  
[Ví dụ thêm về addMapping](https://github.com/nmt-luu-tru/Java-Programming-for-Complete-Beginners/blob/main/V%C3%AD%20d%E1%BB%A5%20th%C3%AAm%20v%E1%BB%81%20addMapping.md)

### 4. Chạy và kiểm tra ứng dụng

Sau khi cấu hình xong, chúng ta sử dụng **Maven Cargo Plugin** để chạy Tomcat nhúng. Plugin này giúp chúng ta triển khai ứng dụng lên một Tomcat nhúng mà không cần cài đặt Tomcat riêng. 

Khi chạy ứng dụng, chúng ta kiểm tra console log để xác nhận rằng **Dispatcher Servlet** đã được khởi tạo thành công. Bạn sẽ thấy log ghi lại thông tin về servlet khi nó nhận yêu cầu HTTP từ trình duyệt.

Khi truy cập vào địa chỉ `http://localhost:8080/to-do-list/` trong trình duyệt, bạn sẽ thấy thông báo lỗi **404**. Điều này là bình thường vì chúng ta chưa tạo bất kỳ **controller** nào để xử lý yêu cầu đến URL đó.

### 5. Giải thích chi tiết log và lỗi 404:

Trong console log, bạn sẽ thấy dòng thông báo:

```
No mapping found for HTTP request with URI [/to-do-list/] in DispatcherServlet with name 'dispatcher'
```

Điều này có nghĩa là **Dispatcher Servlet** đã nhận được yêu cầu từ người dùng, nhưng nó không tìm thấy bất kỳ **controller** hoặc **handler method** nào để xử lý yêu cầu đó. Vì vậy, nó trả về mã lỗi **404** (Not Found). Điều này chứng tỏ rằng **Dispatcher Servlet** đã hoạt động chính xác, nhưng chúng ta cần tạo thêm các controller để xử lý yêu cầu.

### 6. Kết luận

- **Dispatcher Servlet** đã được cấu hình thành công và xử lý các yêu cầu đến ứng dụng web.
- Lỗi 404 xảy ra do chưa có controller nào được tạo ra để xử lý yêu cầu từ người dùng.
- Ở bước tiếp theo, chúng ta sẽ tạo các **controller** để xử lý các yêu cầu từ người dùng và hoàn thiện ứng dụng web của mình.

Trong video tiếp theo, chúng ta sẽ tiếp tục học về cách tạo controller và mapping các URL đến các controller tương ứng trong Spring MVC.
