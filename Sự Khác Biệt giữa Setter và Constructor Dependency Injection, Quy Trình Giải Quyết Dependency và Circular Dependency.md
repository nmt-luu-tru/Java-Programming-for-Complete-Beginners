### Sự Khác Biệt giữa Setter và Constructor Dependency Injection, Quy Trình Giải Quyết Dependency và Circular Dependency

Trong video này, chúng ta sẽ tìm hiểu chi tiết về sự khác biệt giữa **setter-based** và **constructor-based dependency injection** trong Spring, đồng thời xem xét quy trình giải quyết dependency và khái niệm **circular dependency**.

#### 1. **Sự Khác Biệt giữa Setter và Constructor Dependency Injection**

- **Constructor-based Dependency Injection**: Nên được sử dụng cho các dependency bắt buộc. Khi sử dụng constructor injection, Spring sẽ đảm bảo rằng các đối tượng được inject sẽ không bị `null`, và lớp được khởi tạo trong trạng thái đầy đủ.
    - Ưu điểm: Hỗ trợ tạo ra các đối tượng bất biến (immutable) và đảm bảo rằng tất cả các dependency cần thiết đã được cung cấp ngay khi đối tượng được khởi tạo.
    - Nhược điểm: Nếu có quá nhiều đối số trong constructor (hơn 3), điều này có thể là dấu hiệu của việc thiết kế lớp không tốt, vi phạm nguyên tắc **Separation of Concerns** (Tách biệt trách nhiệm).

- **Setter-based Dependency Injection**: Nên được sử dụng cho các dependency tùy chọn (optional). Với setter injection, bạn có thể dễ dàng cung cấp các giá trị mặc định cho các dependency.
    - Ưu điểm: Cho phép các dependency có thể được tái cấu hình hoặc tái inject vào đối tượng sau khi nó đã được khởi tạo.
    - Nhược điểm: Bạn phải kiểm tra `null` khi sử dụng các dependency vì không có gì đảm bảo rằng chúng đã được inject.

**Quy tắc chung**: Sử dụng **constructor injection** cho các dependency bắt buộc và **setter injection** cho các dependency tùy chọn.

#### 2. **Quy Trình Giải Quyết Dependency**

Spring thực hiện quy trình giải quyết dependency của bean theo các bước sau:

- **Khởi tạo ApplicationContext**: Spring khởi tạo **ApplicationContext** với metadata chứa định nghĩa của tất cả các bean trong ứng dụng.
- **Cung cấp Dependency**: Khi một bean được tạo, các dependency của nó (được mô tả dưới dạng thuộc tính hoặc đối số constructor) sẽ được cung cấp cho bean.
- **Chuyển đổi kiểu dữ liệu**: Nếu dependency được cung cấp dưới dạng chuỗi (String), Spring sẽ tự động chuyển đổi nó sang kiểu dữ liệu tương ứng (ví dụ: int, boolean).
- **Xác thực Cấu Hình**: Spring luôn kiểm tra tính hợp lệ của cấu hình của mỗi bean khi container được khởi tạo, nhưng các thuộc tính của bean chỉ được gán giá trị khi bean thực sự được tạo ra.

Điều này có thể dẫn đến việc một biểu đồ các bean được tạo ra, khi mỗi bean phụ thuộc vào các bean khác.

#### 3. **Circular Dependency**

**Circular Dependency** xảy ra khi hai hoặc nhiều bean phụ thuộc lẫn nhau. Ví dụ:
- **Class A** yêu cầu một thể hiện của **Class B** thông qua constructor injection.
- **Class B** lại yêu cầu một thể hiện của **Class A** cũng thông qua constructor injection.

Điều này sẽ tạo ra vòng lặp không thể giải quyết, và Spring sẽ ném ra lỗi **BeanCurrentlyInCreationException**.

Một giải pháp cho vấn đề này là sử dụng **setter-based injection** cho ít nhất một trong hai bean, để tránh tình trạng circular dependency. Khi sử dụng setter injection, một trong hai bean có thể được inject vào bean còn lại trước khi nó được khởi tạo đầy đủ, điều này giúp tránh lỗi nhưng có thể dẫn đến tình huống đối tượng chưa được khởi tạo hoàn toàn.

#### Tổng Kết

- **Constructor Injection**: Tốt hơn cho các dependency bắt buộc, giúp đảm bảo đối tượng được khởi tạo ở trạng thái đầy đủ và không `null`.
- **Setter Injection**: Tốt hơn cho các dependency tùy chọn, dễ dàng tái cấu hình và tái inject.

Trong video tiếp theo, chúng ta sẽ tìm hiểu về **bean life cycle callbacks** trong Spring. Đây là các phương thức callback được Spring gọi tại các thời điểm khác nhau trong vòng đời của một bean. Hẹn gặp lại bạn trong video tiếp theo!
