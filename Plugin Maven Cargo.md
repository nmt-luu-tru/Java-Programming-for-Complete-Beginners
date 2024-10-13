Chúng ta sẽ tiếp tục thảo luận về plugin Maven Cargo và cách sử dụng nó để triển khai ứng dụng web.

### Maven Cargo Plugin:
Maven Cargo là một plugin mạnh mẽ cho phép chúng ta quản lý các ứng dụng web Java bằng cách sử dụng các container như Tomcat, Jetty dưới chế độ nhúng (embedded). Điều này có nghĩa là bạn không cần phải cài đặt riêng Tomcat trên máy tính của mình. Plugin này cho phép bạn chạy và triển khai ứng dụng một cách nhanh chóng.

### Cài đặt Maven Cargo Plugin:
1. **Thêm Maven Cargo Plugin vào `pom.xml`:**
   Trước tiên, chúng ta cần cấu hình plugin Maven Cargo trong file `pom.xml` để có thể sử dụng Tomcat nhúng.

   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.codehaus.cargo</groupId>
               <artifactId>cargo-maven2-plugin</artifactId>
               <version>1.6.7</version>
               <configuration>
                   <container>
                       <containerId>tomcat9x</containerId>
                       <type>embedded</type>
                   </container>
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

   - `containerId`: chỉ định phiên bản Tomcat bạn muốn sử dụng. Trong trường hợp này, là Tomcat 9 (`tomcat9x`).
   - `type`: chỉ định kiểu container, ở đây chúng ta dùng `embedded` để chạy Tomcat nhúng.

2. **Cấu hình thư mục và file:**
   - Chúng ta đã tạo thư mục `webapp` chứa file `index.html` và thư mục `WEB-INF`. File `index.html` rất đơn giản chỉ để kiểm tra kết quả triển khai.

3. **Chạy lệnh Maven Cargo:**
   Sau khi cấu hình xong, chúng ta cần chạy các lệnh Maven để kiểm tra và triển khai ứng dụng. Bước đầu tiên là thực hiện `clean install` để đảm bảo tất cả các phụ thuộc và cấu hình được thiết lập chính xác. Sau đó, chúng ta chạy lệnh `cargo:run` để khởi chạy Tomcat nhúng và triển khai ứng dụng.

   - Trong IntelliJ, mở cửa sổ Maven Projects, tìm plugin Cargo, và chọn `cargo:run`.

   Maven sẽ tải về phiên bản Tomcat nhúng và khởi chạy ứng dụng. Bạn có thể kiểm tra kết quả bằng cách truy cập địa chỉ: `http://localhost:8080/to-do-list/index.html`.

### Kiểm tra và tắt Tomcat:
- Sau khi chạy thành công, bạn có thể mở trình duyệt và truy cập vào ứng dụng tại địa chỉ đã đề cập. Nếu muốn dừng Tomcat, bạn chỉ cần quay lại IntelliJ và nhấn `Ctrl + C` để dừng container.
  
### Tổng kết:
Plugin Maven Cargo giúp bạn dễ dàng phát triển và triển khai ứng dụng web mà không cần phải cài đặt và cấu hình phức tạp các server độc lập như Tomcat. Điều này rất hữu ích trong quá trình phát triển nhanh chóng và triển khai ứng dụng web Java.

Trong video tiếp theo, chúng ta sẽ bắt đầu thiết lập Dispatcher Servlet và tiếp tục xây dựng các phần tiếp theo của ứng dụng.
