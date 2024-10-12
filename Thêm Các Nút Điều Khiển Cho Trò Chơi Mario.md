# Thêm Các Nút Điều Khiển Cho Trò Chơi Mario

Chào mừng bạn quay trở lại! Bây giờ chúng ta đã có một phiên bản chạy được của **GameRunner** cho trò chơi **Mario**. Để làm cho trò chơi thú vị hơn, chúng ta sẽ thêm các nút điều khiển **lên**, **xuống**, **trái**, và **phải** cho trò chơi.

## Các Bước Thêm Nút Điều Khiển

### 1. Thêm Phương Thức Điều Khiển Trong Lớp `MarioGame`

Chúng ta sẽ tạo ra các phương thức tương ứng với các hành động khi nhấn các nút điều khiển trong trò chơi **Mario**.

Trong lớp `MarioGame`, thêm các phương thức sau:

```java
public class MarioGame {
    
    public void up() {
        System.out.println("Jump");
    }

    public void down() {
        System.out.println("Go into a hole");
    }

    public void left() {
        System.out.println("Move back");
    }

    public void right() {
        System.out.println("Accelerate");
    }
}
```

Các phương thức này mô phỏng các hành động mà Mario sẽ thực hiện khi người chơi nhấn các nút tương ứng:

- **up()**: Mario nhảy lên.
- **down()**: Mario chui vào hố.
- **left()**: Mario di chuyển ngược lại.
- **right()**: Mario tăng tốc.

### 2. Cập Nhật Phương Thức `run` Trong `GameRunner`

Bây giờ, trong lớp `GameRunner`, chúng ta sẽ gọi các phương thức điều khiển của `MarioGame` khi chạy trò chơi. Cập nhật phương thức `run` để thực hiện điều này:

```java
public class GameRunner {
    private MarioGame game;

    public GameRunner(MarioGame game) {
        this.game = game;
    }

    public void run() {
        System.out.println("Running game: " + game);
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Phương thức `run` bây giờ sẽ gọi các hành động **nhảy**, **chui vào hố**, **đi ngược**, và **tăng tốc** của Mario khi trò chơi được chạy.

### 3. Chạy Lại Ứng Dụng

Bây giờ chúng ta đã thêm các hành động vào trò chơi, hãy chạy lại ứng dụng để xem kết quả:

1. Nhấp chuột phải vào lớp `AppGamingBasicJava`.
2. Chọn **Run As** -> **Java Application**.
3. Xem kết quả trên **Console**.

Bạn sẽ thấy kết quả tương tự như sau:

```
Running game: com.in28minutes.learnspringframework.game.MarioGame@somehashcode
Jump
Go into a hole
Move back
Accelerate
```

Các hành động đã được thực hiện đúng cách khi các nút điều khiển được nhấn.

## Kết Luận

Chúng ta đã thêm thành công các nút điều khiển cho trò chơi **Mario** và chạy các hành động tương ứng khi trò chơi được chạy qua `GameRunner`. Tuy nhiên, ở phiên bản hiện tại, chúng ta đang gọi các hành động trong trò chơi một cách **tightly coupled** (liên kết chặt), nghĩa là `GameRunner` chỉ chạy được trò chơi **Mario**. Điều này sẽ gây khó khăn khi chúng ta muốn thay đổi trò chơi khác hoặc thêm nhiều trò chơi vào.

Ở bước tiếp theo, chúng ta sẽ tìm hiểu về khái niệm **tight coupling** và cách làm thế nào để tạo ra một hệ thống **loose coupling** (liên kết lỏng) bằng cách sử dụng các giao diện (interfaces).
