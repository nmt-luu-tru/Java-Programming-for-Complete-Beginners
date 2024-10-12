# Giải Pháp Cho Bài Tập Tạo Pac-Man Game

## 1. Giới Thiệu

Chào mừng trở lại! Hy vọng bạn đã hoàn thành bài tập và tạo trò chơi **Pac-Man** bằng cách triển khai giao diện **GamingConsole**. Trong bước này, chúng ta sẽ nhanh chóng xem xét giải pháp và kiểm tra cách **Pac-Man** được tích hợp vào hệ thống.

## 2. Giải Pháp Tạo Pac-Man Game

### Bước 1: Sao Chép Lớp MarioGame

Bước đầu tiên để tạo **Pac-Man** là sao chép mã từ lớp **MarioGame**:

1. Mở lớp **MarioGame**.
2. Sao chép toàn bộ nội dung (Ctrl + C) và tạo một lớp mới cho **PacMan**.
3. Đổi tên lớp mới từ **MarioGame** thành **PacmanGame**.

### Bước 2: Tạo Lớp `PacmanGame`

Sau khi sao chép mã từ **MarioGame**, chỉnh sửa lớp mới và đặt tên là **PacmanGame**. Lớp này cũng sẽ thực thi giao diện **GamingConsole** và có các hành động **up**, **down**, **left**, **right**. Dưới đây là mã cho lớp **PacmanGame**:

```java
public class PacmanGame implements GamingConsole {
    @Override
    public void up() {
        System.out.println("Move up in Pac-Man");
    }

    @Override
    public void down() {
        System.out.println("Move down in Pac-Man");
    }

    @Override
    public void left() {
        System.out.println("Move left in Pac-Man");
    }

    @Override
    public void right() {
        System.out.println("Move right in Pac-Man");
    }
}
```

### Bước 3: Sử Dụng PacmanGame Trong AppGamingBasicJava

Bây giờ, chúng ta có thể sử dụng **PacmanGame** trong lớp **AppGamingBasicJava** mà không cần thay đổi mã của **GameRunner**. Chỉ cần thay thế trò chơi hiện tại bằng **PacmanGame**.

```java
public class AppGamingBasicJava {
    public static void main(String[] args) {
        var game = new PacmanGame();
        var gameRunner = new GameRunner(game);
        gameRunner.run();
    }
}
```

### Bước 4: Chạy Ứng Dụng

Sau khi cập nhật mã, hãy chạy ứng dụng:

1. Nhấp chuột phải vào **AppGamingBasicJava**.
2. Chọn **Run As** -> **Java Application**.

Bạn sẽ thấy kết quả trong **console**, nơi các hành động của **Pac-Man** được in ra:

```
Move up in Pac-Man
Move down in Pac-Man
Move left in Pac-Man
Move right in Pac-Man
```

## 3. Lợi Ích Của Loose Coupling

Nhờ có giao diện **GamingConsole**, chúng ta có thể dễ dàng thêm trò chơi mới như **Pac-Man** mà không cần thay đổi mã của **GameRunner**. **GameRunner** không còn phụ thuộc chặt chẽ vào bất kỳ trò chơi cụ thể nào, và chúng ta có thể chuyển đổi trò chơi chỉ bằng cách thay đổi lớp trò chơi mà không cần chỉnh sửa lớp **GameRunner**.

## 4. Kết Luận

- Chúng ta đã tạo thành công trò chơi **Pac-Man** và triển khai giao diện **GamingConsole**.
- **GameRunner** giờ đây có thể chạy bất kỳ trò chơi nào thực thi giao diện này mà không cần thay đổi mã nguồn của chính nó.
- Đây là một ví dụ điển hình về **loose coupling** trong phát triển phần mềm.

Ở bước tiếp theo, chúng ta sẽ bắt đầu tích hợp **Spring Framework** để cải thiện hơn nữa mã nguồn và giúp tự động hóa các thành phần thông qua **Dependency Injection**. Hẹn gặp lại bạn trong bước tiếp theo!
