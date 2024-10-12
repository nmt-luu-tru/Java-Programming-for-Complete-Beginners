# Giới Thiệu Về Wiring of Dependencies Và Spring Framework

## 1. Tổng Quan Về Wiring of Dependencies

Trong bước trước, chúng ta đã tạo đối tượng **PacmanGame** và truyền nó vào **GameRunner**. Có hai phần quan trọng trong mã:

1. **Tạo đối tượng**: Chúng ta tạo một đối tượng **PacmanGame**.
2. **Tiêm phụ thuộc**: Chúng ta truyền đối tượng **PacmanGame** vào **GameRunner** thông qua constructor.

Điều này được gọi là **wiring of dependencies**. **GameRunner** cần một trò chơi để chạy, vì vậy trò chơi này (ví dụ: **PacmanGame**) là một **phụ thuộc** của **GameRunner**. Khi chúng ta truyền **PacmanGame** vào **GameRunner**, chúng ta đang **tiêm phụ thuộc** vào **GameRunner**.

## 2. Vấn Đề Với Quản Lý Phụ Thuộc Thủ Công

Mặc dù mã này khá đơn giản, trong các ứng dụng lớn hơn với hàng nghìn lớp và phụ thuộc, việc quản lý tất cả các đối tượng và phụ thuộc thủ công có thể trở nên phức tạp. Mã mà chúng ta đã viết đang tạo và quản lý các đối tượng hoàn toàn bằng tay, điều này có thể gây khó khăn khi quy mô hệ thống tăng lên.

## 3. Giới Thiệu Spring Framework Để Quản Lý Phụ Thuộc

Thay vì tự tay tạo và quản lý các đối tượng, chúng ta có thể sử dụng **Spring Framework** để tự động tạo và quản lý chúng. Trong bước tiếp theo, chúng ta sẽ thử nghiệm việc sử dụng Spring để:

- **Tạo các đối tượng** (ví dụ: **PacmanGame** và **GameRunner**).
- **Wiring** (tiêm) các phụ thuộc mà không cần tự tay quản lý chúng.

Thay vì viết mã để tạo đối tượng **PacmanGame** và **GameRunner**, chúng ta sẽ để Spring Framework xử lý việc này.

## 4. Thử Nghiệm Đơn Giản Với Spring

Trước khi áp dụng Spring vào trò chơi của chúng ta, chúng ta sẽ bắt đầu với một ví dụ đơn giản hơn. Trong ví dụ này, Spring sẽ quản lý các đối tượng đơn giản như **Person** và **Address**. Điều này sẽ giúp chúng ta hiểu rõ hơn cách Spring tạo và quản lý đối tượng, trước khi chuyển sang các ví dụ phức tạp hơn.

Hãy sẵn sàng để Spring quản lý các đối tượng và phụ thuộc trong bước tiếp theo!
