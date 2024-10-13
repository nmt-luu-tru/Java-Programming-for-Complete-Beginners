### Sử dụng Dependency Injection dựa trên Setter

Trong video này, chúng ta sẽ học cách sử dụng **setter-based dependency injection** trong Spring. Đây là một phương pháp khác để inject các dependency vào các lớp trong Spring, khác với phương pháp **constructor-based dependency injection** mà chúng ta đã học trước đó.

#### Bước 1: Loại bỏ Constructor

Trước tiên, chúng ta sẽ loại bỏ constructor đã sử dụng để inject **NumberGenerator** trong lớp **GameImpl**. Điều này đảm bảo rằng Spring sẽ không sử dụng constructor để inject dependency nữa.

```java
// Xóa constructor hiện tại trong GameImpl
```

#### Bước 2: Thêm Setter cho `NumberGenerator`

Tiếp theo, chúng ta cần tạo một setter cho trường **NumberGenerator** trong lớp **GameImpl** để Spring có thể sử dụng phương thức này để inject dependency.

```java
public void setNumberGenerator(NumberGenerator numberGenerator) {
    this.numberGenerator = numberGenerator;
}
```

- Phương thức này đơn giản chỉ nhận một đối tượng **NumberGenerator** và gán giá trị của nó vào trường **numberGenerator** trong lớp.

#### Bước 3: Cập nhật `beans.xml` để Sử dụng Setter-Based Dependency Injection

Tiếp theo, chúng ta sẽ chỉnh sửa tệp **beans.xml** để Spring container sử dụng **setter-based dependency injection** thay vì **constructor-based dependency injection**.

```xml
<bean id="game" class="Academy.learnprogramming.GameImpl">
    <property name="numberGenerator" ref="numberGenerator"/>
</bean>

<bean id="numberGenerator" class="Academy.learnprogramming.NumberGeneratorImpl"/>
```

- Trong đoạn mã trên, chúng ta sử dụng thẻ **property** thay cho **constructor-arg**. Thuộc tính **name** của thẻ **property** phải khớp với tên của trường trong lớp **GameImpl** (tức là **numberGenerator**), và **ref** trỏ đến bean mà chúng ta muốn inject (trong trường hợp này là **numberGenerator**).

#### Bước 4: Kiểm Tra Chương Trình

Bây giờ, chúng ta có thể chạy chương trình để kiểm tra kết quả sau khi sử dụng **setter-based dependency injection**.

```java
// Chạy lại ứng dụng trong lớp Main
```

Kết quả đầu ra sẽ tương tự như khi sử dụng **constructor-based dependency injection**, nhưng lần này Spring đã sử dụng setter để inject dependency.

### Kết Luận

Trong video này, chúng ta đã học cách sử dụng **setter-based dependency injection** trong Spring. Phương pháp này cho phép Spring container tự động gọi các phương thức setter để inject các dependency vào đối tượng sau khi gọi constructor không có tham số.

So sánh với **constructor-based dependency injection**, phương pháp **setter-based** linh hoạt hơn khi có thể thêm hoặc thay đổi dependency mà không cần sửa đổi constructor, nhưng cũng có thể làm giảm sự an toàn vì đối tượng có thể được tạo mà không có đủ các dependency cần thiết. Trong video tiếp theo, chúng ta sẽ so sánh chi tiết giữa hai phương pháp này và thảo luận khi nào nên sử dụng từng phương pháp.
