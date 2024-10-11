# Xây Dựng Ứng Dụng Với Java, Spring Và Spring Boot

## Giới Thiệu Về Mục Tiêu Của Phần Học

Trong phần này, chúng ta sẽ tìm hiểu cách xây dựng nhiều loại ứng dụng khác nhau bằng **Java**, **Spring**, và **Spring Boot**. Những ứng dụng này bao gồm:

- **Ứng dụng web**
- **REST API**
- **Ứng dụng full stack**
- **Microservices**
- Và nhiều loại ứng dụng khác.

Dù bạn đang xây dựng loại ứng dụng nào, **Spring Framework** vẫn cung cấp tất cả các tính năng cốt lõi cần thiết. Hiểu rõ Spring Framework không chỉ giúp bạn dễ dàng học **Spring Boot**, mà còn giúp bạn nhanh chóng tìm ra và sửa lỗi khi phát sinh vấn đề trong ứng dụng.

Trong module này, chúng ta sẽ tập trung nhiều vào **Spring Framework**, vì đây là nền tảng quan trọng nhất để xây dựng ứng dụng Java hiện đại.

## Mục Tiêu Của Phần Học Này

### 1. Hiểu Các Tính Năng Cốt Lõi Của Spring Framework

Mục tiêu hàng đầu của phần học này là giúp bạn hiểu rõ các tính năng cốt lõi của Spring Framework. Để làm điều này, chúng ta sẽ áp dụng phương pháp tiếp cận thực hành. Chúng ta sẽ xây dựng một ứng dụng **Hello World** đơn giản, nhưng với cách tiếp cận **Spring hiện đại**, nhằm minh họa các khái niệm chính.

Chúng ta sẽ tạo ra một ứng dụng để chạy các trò chơi nổi tiếng như **Mario**, **Super Contra**, và **PacMan**. Trong quá trình đó, bạn sẽ tìm hiểu:

- Tại sao cần sử dụng Spring Framework.
- Các thuật ngữ quan trọng trong Spring Framework như:
  - **Tight coupling** (Liên kết chặt)
  - **Loose coupling** (Liên kết lỏng)
  - **IOC container** (Container kiểm soát ngược)
  - **Application Context** (Ngữ cảnh ứng dụng)
  - **Component Scan** (Quét thành phần)
  - **Dependency Injection** (Tiêm phụ thuộc)
  - **Spring Beans**
  - **Auto wiring** (Tự động kết nối)

## Quy Trình Xây Dựng Ứng Dụng Game

### Iteration 1: Xây Dựng Mã Java Tightly Coupled

Trong lần lặp đầu tiên, chúng ta sẽ xây dựng mã Java với liên kết chặt (tightly coupled). Ở bước này, chúng ta sẽ:

- Tạo lớp **Game Runner** để chạy các trò chơi.
- Sử dụng lớp **Game Runner** để gọi các lớp game như Mario, Super Contra, và PacMan.

### Iteration 2: Hiểu Về Loose Coupling Với Giao Diện Java

Ở lần lặp thứ hai, chúng ta sẽ tìm hiểu về khái niệm **liên kết lỏng (loose coupling)** và cách sử dụng các giao diện (interfaces) trong Java để đạt được mục tiêu này. Các bước cụ thể bao gồm:

- Tạo một giao diện có tên **Gaming Console**.
- Tất cả các lớp game như Mario, Super Contra, PacMan sẽ triển khai (implement) giao diện này.

Nếu bạn chưa quen với giao diện Java, đừng lo lắng. Tôi sẽ hướng dẫn bạn một cách dễ hiểu.

### Iteration 3: Đưa Spring Framework Vào Sử Dụng

Trong lần lặp thứ ba, chúng ta sẽ bắt đầu áp dụng **Spring Framework** để đạt đến mức liên kết lỏng đầu tiên. Các bước cụ thể:

- Tạo ra một số **Spring beans**.
- Để **Spring Framework** quản lý việc tạo đối tượng và kết nối các thành phần với nhau.

### Iteration 4: Liên Kết Lỏng Cấp Độ Hai Với Spring Framework

Trong lần lặp thứ tư, chúng ta sẽ đạt đến mức liên kết lỏng cấp độ hai với sự hỗ trợ của **Spring Framework** và các chú thích (annotations) mạnh mẽ của Spring. Kết quả:

- **Spring Framework** sẽ chịu trách nhiệm tạo, quản lý và tự động kết nối các đối tượng với nhau.
  
## Kết Luận

Các thuật ngữ và khái niệm như **IOC container**, **Spring Beans**, và **Auto wiring** có thể nghe có vẻ khó hiểu lúc đầu. Nhưng đừng lo lắng, tôi sẽ làm cho chúng trở nên dễ hiểu bằng cách sử dụng các ví dụ thực tế và phương pháp tiếp cận từng bước.

Bây giờ, hãy bắt đầu bước vào thực hành! Chúng ta sẽ cùng nhau xây dựng một ứng dụng **Spring** trong bước tiếp theo.
