# Iteration 2: Tạo Loose Coupling Với Interfaces

## 1. Giới Thiệu Về Loose Coupling Và Interfaces

Trong bước này, chúng ta sẽ đưa **loose coupling** vào hệ thống bằng cách sử dụng **interfaces** trong Java. Chúng ta muốn tạo ra một lớp giao diện chung có tên là **`GamingConsole`**, và các trò chơi như **MarioGame**, **SuperContraGame** sẽ thực thi (implement) giao diện này.

Mục tiêu là làm cho **GameRunner** có thể chạy bất kỳ trò chơi nào mà không cần thay đổi mã nguồn của nó, bằng cách phụ thuộc vào giao diện **GamingConsole** thay vì các lớp trò chơi cụ thể.

## 2. Các Bước Thực Hiện

### Bước 1: Tạo Giao Diện `GamingConsole`

1. Nhấp chuột phải vào gói `com.in28minutes.learnspringframework.game`.
2. Chọn **New** -> **Interface**.
3. Đặt tên giao diện là **`GamingConsole`**.
4. Trong giao diện này, định nghĩa các hành động mà trò chơi có thể thực hiện:

```java
public interface GamingConsole {
    void up();
    void down();
    void left();
    void right();
}
```

### Bước 2: Thực Thi Giao Diện Trong `MarioGame` và `SuperContraGame`

#### **MarioGame**:

Chúng ta sẽ thay đổi lớp **MarioGame** để thực thi giao diện **GamingConsole**:

```java
public class MarioGame implements GamingConsole {
    @Override
    public void up() {
        System.out.println("Jump");
    }

    @Override
    public void down() {
        System.out.println("Go into a hole");
    }

    @Override
    public void left() {
        System.out.println("Move back");
    }

    @Override
    public void right() {
        System.out.println("Accelerate");
    }
}
```

#### **SuperContraGame**:

Tương tự, chúng ta sẽ làm điều này cho **SuperContraGame**:

```java
public class SuperContraGame implements GamingConsole {
    @Override
    public void up() {
        System.out.println("Up");
    }

    @Override
    public void down() {
        System.out.println("Sit down");
    }

    @Override
    public void left() {
        System.out.println("Go back");
    }

    @Override
    public void right() {
        System.out.println("Shoot a bullet");
    }
}
```

### Bước 3: Thay Đổi `GameRunner` Để Sử Dụng `GamingConsole`

Thay vì phụ thuộc vào các lớp trò chơi cụ thể như **MarioGame** hay **SuperContraGame**, chúng ta sẽ làm cho **GameRunner** phụ thuộc vào giao diện **GamingConsole**:

```java
public class GameRunner {
    private GamingConsole game;

    public GameRunner(GamingConsole game) {
        this.game = game;
    }

    public void run() {
        game.up();
        game.down();
        game.left();
        game.right();
    }
}
```

Bây giờ, **GameRunner** chỉ cần biết rằng nó đang chạy một trò chơi nào đó, miễn là trò chơi đó thực thi giao diện **GamingConsole**.

### Bước 4: Chạy Và Kiểm Tra Ứng Dụng

Trong lớp **AppGamingBasicJava**, chúng ta có thể dễ dàng chuyển đổi giữa các trò chơi mà không cần thay đổi mã của **GameRunner**:

```java
public class AppGamingBasicJava {
    public static void main(String[] args) {
        // Chạy trò chơi Mario
        var marioGame = new MarioGame();
        var gameRunner = new GameRunner(marioGame);
        gameRunner.run();

        // Chạy trò chơi Super Contra
        var superContraGame = new SuperContraGame();
        var gameRunner2 = new GameRunner(superContraGame);
        gameRunner2.run();
    }
}
```

### Kết Quả

- Khi bạn chạy chương trình, **GameRunner** sẽ có thể chạy cả **MarioGame** và **SuperContraGame** một cách linh hoạt mà không cần thay đổi bất kỳ mã nguồn nào của **GameRunner**.
- Điều này minh họa rõ ràng lợi ích của **loose coupling**: **GameRunner** không phụ thuộc vào chi tiết cụ thể của từng trò chơi mà chỉ phụ thuộc vào giao diện **GamingConsole**.

## 3. Lợi Ích Của Loose Coupling Với Interfaces

### 1. **Giảm Phụ Thuộc Cụ Thể**:
   Bây giờ, **GameRunner** không phụ thuộc vào các lớp cụ thể như **MarioGame** hay **SuperContraGame**, mà chỉ phụ thuộc vào giao diện **GamingConsole**.

### 2. **Dễ Dàng Mở Rộng**:
   Bạn có thể dễ dàng thêm trò chơi mới như **Pac-Man** bằng cách tạo lớp **PacMan** và thực thi giao diện **GamingConsole** mà không cần thay đổi mã của **GameRunner**.

### 3. **Bảo Trì Dễ Dàng**:
   Khi mã nguồn ít phụ thuộc vào nhau, việc sửa đổi và bảo trì sẽ trở nên dễ dàng hơn, giúp tránh các lỗi tiềm ẩn khi thay đổi một phần của hệ thống.

## 4. Kết Luận

Trong bước này, chúng ta đã chuyển từ mã **tightly coupled** sang **loose coupling** bằng cách sử dụng **interfaces** trong Java. **GameRunner** giờ đây có thể tương tác với bất kỳ trò chơi nào thực thi giao diện **GamingConsole** mà không cần thay đổi mã nguồn của chính nó.
