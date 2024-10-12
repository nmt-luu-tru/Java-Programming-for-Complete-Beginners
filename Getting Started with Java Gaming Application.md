# Hướng Dẫn Tạo Game Runner Class Cho Trò Chơi Mario

## Mục tiêu

Trong bước này, chúng ta sẽ tạo một **game runner class** để chạy trò chơi **Mario**. Bạn sẽ viết mã Java để mô phỏng quá trình chạy game bằng cách sử dụng một lớp `GameRunner` và trò chơi `Mario`. Chúng ta sẽ bắt đầu bằng việc thiết lập lớp Mario và sử dụng lớp GameRunner để chạy trò chơi.

## Các Bước Thực Hiện

### 1. Tạo Lớp `AppGamingBasicJava`

1. Mở Eclipse IDE.
2. Trong gói `com.in28minutes.learnspringframework`, nhấp chuột phải và chọn **New** -> **Class**.
3. Đặt tên cho lớp là `AppGamingBasicJava`.
4. Chọn tùy chọn tạo phương thức `public static void main(String[] args)` để có thể khởi chạy chương trình.
5. Nhấp **Finish** để hoàn thành.

### 2. Tạo Lớp `GameRunner` Và `MarioGame`

Trong lớp `AppGamingBasicJava`, bạn sẽ khởi tạo đối tượng `GameRunner` và `MarioGame`. Đây là mã cần viết trong lớp `AppGamingBasicJava`:

```java
public class AppGamingBasicJava {
    public static void main(String[] args) {
        // Tạo đối tượng MarioGame
        MarioGame marioGame = new MarioGame();

        // Tạo đối tượng GameRunner và truyền MarioGame vào
        GameRunner gameRunner = new GameRunner(marioGame);

        // Chạy game
        gameRunner.run();
    }
}
```

Bây giờ bạn sẽ thấy lỗi biên dịch, vì chưa tạo lớp `MarioGame` và `GameRunner`. Chúng ta sẽ giải quyết những lỗi này bằng cách tạo các lớp đó.

### 3. Tạo Lớp `MarioGame`

1. Trở lại Eclipse, nhấn **Ctrl + 1** hoặc **Cmd + 1** tại lỗi `MarioGame` và chọn **Create Class 'MarioGame'**.
2. Đặt lớp này trong gói `com.in28minutes.learnspringframework.game`.
3. Nhấn **Finish**.

Bạn vừa tạo thành công lớp `MarioGame`. Trong lớp này, bạn có thể thêm các phương thức cho các nút di chuyển của trò chơi trong các bước sau.

### 4. Tạo Lớp `GameRunner`

1. Tại lỗi `GameRunner`, nhấn **Ctrl + 1** hoặc **Cmd + 1** và chọn **Create Class 'GameRunner'**.
2. Đặt lớp này cũng trong gói `com.in28minutes.learnspringframework.game`.
3. Nhấn **Finish**.

### 5. Viết Constructor Và Phương Thức `run` Trong `GameRunner`

Bây giờ, trong lớp `GameRunner`, chúng ta sẽ viết constructor để nhận đối tượng `MarioGame` và phương thức `run()` để chạy trò chơi:

```java
public class GameRunner {
    private MarioGame game;

    // Constructor nhận MarioGame
    public GameRunner(MarioGame game) {
        this.game = game;
    }

    // Phương thức run để chạy trò chơi
    public void run() {
        System.out.println("Running game: " + game);
    }
}
```

### 6. Kiểm Tra Và Chạy Ứng Dụng

Quay lại lớp `AppGamingBasicJava`, bạn sẽ thấy không còn lỗi biên dịch nào. Bây giờ, hãy chạy chương trình:

1. Nhấp chuột phải vào lớp `AppGamingBasicJava`.
2. Chọn **Run As** -> **Java Application**.
3. Xem kết quả trên **Console**. Bạn sẽ thấy thông báo tương tự như sau:

```
Running game: com.in28minutes.learnspringframework.game.MarioGame@somehashcode
```
