# Tìm Hiểu Về Tight Coupling Và Loose Coupling Trong Java

## 1. Tight Coupling Là Gì?

**Tight coupling** (liên kết chặt) là khi các lớp hoặc các thành phần của phần mềm phụ thuộc mạnh mẽ vào nhau. Điều này có nghĩa là khi bạn thay đổi một phần của hệ thống, bạn cần thay đổi các phần khác liên quan để mọi thứ hoạt động bình thường. 

### Ví Dụ: Tight Coupling Trong GameRunner

Trong ví dụ của chúng ta, **GameRunner** được thiết kế để chạy trò chơi **Mario**. Mã hiện tại của chúng ta như sau:

```java
MarioGame marioGame = new MarioGame();
GameRunner gameRunner = new GameRunner(marioGame);
gameRunner.run();
```

Nếu bây giờ bạn muốn chạy trò chơi **Super Contra** thay vì **Mario**, bạn phải thay đổi cả **GameRunner** để hỗ trợ trò chơi mới:

```java
SuperContraGame superContraGame = new SuperContraGame();
GameRunner gameRunner = new GameRunner(superContraGame);
gameRunner.run();
```

Tuy nhiên, khi làm điều này, bạn sẽ thấy rằng **GameRunner** được "tightly coupled" với trò chơi **MarioGame**, tức là **GameRunner** chỉ có thể làm việc với **MarioGame**, và bạn phải thay đổi mã nếu muốn nó làm việc với **SuperContraGame**.

### Ví Dụ Cụ Thể Về Tight Coupling

Nếu bạn thay đổi loại trò chơi, bạn phải sửa đổi mã trong **GameRunner**. Ví dụ:

```java
// Thay đổi GameRunner để sử dụng SuperContraGame
private SuperContraGame game;

public GameRunner(SuperContraGame game) {
    this.game = game;
}

public void run() {
    game.up();
    game.down();
    game.left();
    game.right();
}
```

Mỗi khi bạn thêm hoặc thay đổi trò chơi, bạn phải cập nhật cả **GameRunner**. Đây là một ví dụ điển hình của tight coupling – bất kỳ thay đổi nào cũng đòi hỏi sự thay đổi trong nhiều nơi trong mã nguồn, làm tăng rủi ro lỗi và giảm tính linh hoạt.

### Tại Sao Tight Coupling Là Vấn Đề?

Tight coupling gây ra nhiều vấn đề khi phát triển phần mềm:

- **Khó khăn trong việc mở rộng**: Khi bạn muốn thêm chức năng mới (ví dụ, một trò chơi mới), bạn phải thay đổi mã nguồn trong nhiều nơi.
- **Khó bảo trì**: Mỗi lần thay đổi một phần của hệ thống, bạn phải kiểm tra lại các phần khác để đảm bảo rằng chúng không bị ảnh hưởng.
- **Giảm tính linh hoạt**: Bạn không thể dễ dàng thay đổi hoặc thêm các thành phần mà không làm gián đoạn toàn bộ hệ thống.


## 3. Kết Luận

- **Tight Coupling**: Là khi các lớp phụ thuộc mạnh vào nhau, gây khó khăn khi thay đổi và mở rộng.
- **Loose Coupling**: Giúp tăng tính linh hoạt, dễ dàng bảo trì và mở rộng hệ thống bằng cách giảm sự phụ thuộc giữa các thành phần.
- **Interfaces**: Là công cụ mạnh mẽ trong Java giúp đạt được loose coupling, cho phép các lớp tương tác thông qua giao diện chung thay vì phụ thuộc trực tiếp vào nhau.

Ở bước tiếp theo, chúng ta sẽ tiếp tục khám phá cách Spring Framework hỗ trợ **loose coupling** thông qua các khái niệm như **Dependency Injection**.
