### Tìm hiểu về Application Events trong Spring

Trong video này, chúng ta sẽ tìm hiểu về **Application Events** trong Spring, cách lắng nghe và xử lý các sự kiện này. Ngoài ra, chúng ta sẽ học cách sử dụng **annotation-based event listeners**.

#### **Application Events là gì?**
Spring cung cấp khả năng phát hành và lắng nghe sự kiện thông qua giao diện **ApplicationEventPublisher**. Các sự kiện này được triển khai theo mô hình **Observer Design Pattern**, nơi một số đối tượng sẽ được thông báo khi có sự kiện xảy ra. Mỗi khi một sự kiện ứng dụng được phát hành vào **ApplicationContext**, các bean thực hiện **ApplicationListener** sẽ được thông báo.

Chúng ta cũng có thể tạo **custom events**, nhưng trong video này, chúng ta sẽ tập trung vào sự kiện có sẵn **ContextRefreshedEvent**, được phát khi **ApplicationContext** được khởi tạo hoặc làm mới.

#### **Cách lắng nghe sự kiện Application Event**
Bây giờ, chúng ta sẽ tạo một class lắng nghe sự kiện **ContextRefreshedEvent**. Đây là các bước cụ thể:

#### **Bước 1: Tạo lớp lắng nghe sự kiện**
1. Tạo một lớp mới trong module **console**: **ConsoleNumberGuess**.
   - Nhấp chuột phải vào package **console** -> New -> Java Class -> Đặt tên là **ConsoleNumberGuess**.

2. Để lớp này có thể được Spring Container quản lý và lắng nghe sự kiện, chúng ta thêm annotation `@Component` trên lớp đó:
   
```java
@Component
public class ConsoleNumberGuess {
    private static final Logger log = LoggerFactory.getLogger(ConsoleNumberGuess.class);
    
    @EventListener
    public void start(ContextRefreshedEvent event) {
        log.info("Container ready for use.");
    }
}
```

3. Ở đây, chúng ta sử dụng **@EventListener** để đánh dấu phương thức `start()` sẽ được thực thi khi sự kiện **ContextRefreshedEvent** được phát hành.

#### **Bước 2: Giải thích về sự kiện ContextRefreshedEvent**
Sự kiện **ContextRefreshedEvent** được phát hành khi **ApplicationContext** được khởi tạo hoặc làm mới, tức là khi tất cả các bean được tải và sẵn sàng sử dụng.

Trong phương thức `start()`, chúng ta chỉ cần log một thông báo để xác nhận rằng sự kiện đã được xử lý và container đã sẵn sàng.

#### **Bước 3: Chạy và kiểm tra**
1. Chạy chương trình và kiểm tra log đầu ra. Bạn sẽ thấy thông báo: **"Container ready for use."** khi container sẵn sàng.

#### **Sử dụng @EventListener để lắng nghe nhiều sự kiện**
Nếu bạn muốn lắng nghe nhiều sự kiện, bạn có thể thêm nhiều lớp sự kiện vào annotation **@EventListener**, ví dụ:

```java
@EventListener({ContextRefreshedEvent.class, AnotherEvent.class})
public void handleMultipleEvents() {
    // Handle multiple events
}
```

#### **Xử lý lỗi không có tham số sự kiện**
Nếu bạn không sử dụng tham số sự kiện trong phương thức, như sau:

```java
@EventListener
public void start() {
    // Code
}
```

Chương trình sẽ gặp lỗi vì Spring yêu cầu phải xác định rõ loại sự kiện mà bạn muốn lắng nghe. Bạn có thể sử dụng cách truyền loại sự kiện qua annotation:

```java
@EventListener(ContextRefreshedEvent.class)
public void start() {
    log.info("Container ready for use.");
}
```

### **Tổng kết**
- **Application Events** trong Spring là cách để thực thi logic khi container khởi tạo hoặc khi có các sự kiện tùy chỉnh.
- Bạn có thể lắng nghe các sự kiện bằng cách triển khai **ApplicationListener** hoặc sử dụng **@EventListener**.
- **@EventListener** cung cấp sự linh hoạt hơn vì bạn có thể tùy chỉnh tên phương thức và lắng nghe nhiều sự kiện khác nhau.

Trong video tiếp theo, chúng ta sẽ hoàn thiện phần logic cho trò chơi và chuẩn bị để chạy trò chơi một cách hoàn chỉnh.
