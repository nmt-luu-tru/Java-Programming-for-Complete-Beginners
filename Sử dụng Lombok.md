Được rồi, giờ là lúc sử dụng Lombok trong mã của chúng ta để thấy cách nó hoạt động như thế nào. Bây giờ Lombok đã được cấu hình và hoạt động trong dự án, chúng ta có thể bắt đầu sử dụng nó. Chúng ta sẽ bắt đầu bằng cách refactor một số phần của dự án để sử dụng Lombok, nhằm loại bỏ một số mã boilerplate đã tạo trước đó.

### **Bước 1: Refactor Lớp GameImpl**
- Mở lớp `GameImpl`.
- Nếu bạn cuộn xuống cuối lớp, bạn sẽ thấy có khoảng 130 dòng mã, bao gồm nhiều getter và setter.

### **Bước 2: Thêm Annotation SLF4J**
- Xóa logger hiện tại.
- Thêm annotation `@Slf4j` vào lớp để Lombok tự động tạo logger.
  
```java
@Slf4j
public class GameImpl {
    // Nội dung lớp
}
```

### **Bước 3: Tạo Getter**
- Bạn có thể thấy rằng nhiều thuộc tính như `guessCount`, `number`, `guess`,... có các phương thức getter. Lombok có thể giúp chúng ta tự động tạo các getter này.
- Đầu tiên, thêm annotation `@Getter` vào cấp lớp để Lombok tạo getter cho tất cả các thuộc tính.

```java
@Getter
public class GameImpl {
    // Nội dung lớp
}
```

### **Bước 4: Ngoại lệ cho Một Số Thuộc Tính**
- Đối với thuộc tính `numberGenerator`, không cần getter, do đó ta có thể sử dụng `@Getter(access = AccessLevel.NONE)`.

```java
@Getter
public class GameImpl {
    @Getter(AccessLevel.NONE)
    private NumberGenerator numberGenerator;

    // Các thuộc tính khác
}
```

### **Bước 5: Xóa Các Getter Thủ Công**
- Sau khi thêm `@Getter`, ta có thể xóa tất cả các phương thức getter thủ công trong lớp. Điều này sẽ giảm đáng kể số dòng mã.

### **Bước 6: Thêm Annotation Setter**
- Ta có thể thêm `@Setter` cho thuộc tính `guess`, vì cần có setter cho nó.

```java
@Setter
private int guess;
```

- Đặt `@Setter` ngay sau `guess` để tránh nhầm lẫn rằng setter áp dụng cho tất cả các thuộc tính.

### **Bước 7: Kiểm tra Lớp GameImpl**
- Sau khi xóa tất cả các getter và setter không cần thiết, kiểm tra lại lớp. Kết quả là bạn đã giảm đáng kể số lượng dòng mã cần duy trì, giúp mã dễ đọc và bảo trì hơn.

### **Bước 8: Kiểm tra Dự án**
- Sau khi thực hiện thay đổi, hãy chạy lại ứng dụng để đảm bảo nó vẫn hoạt động bình thường.

```java
public static void main(String[] args) {
    SpringApplication.run(GameImpl.class, args);
}
```

### **Kết quả**
- Sau khi thực hiện tất cả các bước trên, mã của bạn sẽ gọn gàng hơn, tiết kiệm được khoảng 25% dòng mã không cần thiết. Điều này chỉ là một ví dụ nhỏ. Nếu lớp của bạn phức tạp hơn, số lượng mã giảm sẽ lớn hơn nhiều.

Trong video tiếp theo, mình sẽ đưa ra một thử thách để bạn tự cải thiện thêm một số phần khác của dự án, bằng cách sử dụng Lombok để loại bỏ mã boilerplate.
