# Giới Thiệu Về Từ Khóa `var` Trong Java

## 1. Từ Khóa `var` Là Gì?

Trong các bước trước, chúng ta đã sử dụng từ khóa **`var`** để khai báo biến như sau:

```java
var marioGame = new MarioGame();
var gameRunner = new GameRunner(marioGame);
```

Thay vì sử dụng cách khai báo biến truyền thống với kiểu dữ liệu cụ thể, như:

```java
MarioGame marioGame = new MarioGame();
GameRunner gameRunner = new GameRunner(marioGame);
```

Chúng ta sử dụng **`var`** để giảm bớt việc khai báo kiểu dữ liệu một cách rõ ràng. Điều này giúp mã ngắn gọn và dễ đọc hơn.

## 2. `var` Được Giới Thiệu Khi Nào?

**`var`** là một tính năng mới được giới thiệu từ **Java 10**. Để sử dụng **`var`**, bạn cần ít nhất phiên bản **Java 10** trở lên.

## 3. Cách Hoạt Động Của `var`

**`var`** sử dụng **type inference** (suy luận kiểu) để giúp trình biên dịch tự động xác định kiểu của biến dựa trên giá trị mà biến được gán. Điều này có nghĩa là:

- Khi bạn gán giá trị `new MarioGame()`, trình biên dịch sẽ tự động hiểu rằng biến đó có kiểu **`MarioGame`**.
- Khi bạn gán giá trị `new GameRunner(marioGame)`, trình biên dịch sẽ hiểu rằng biến đó có kiểu **`GameRunner`**.

Điều này giúp giảm thiểu việc khai báo kiểu dữ liệu, cho phép bạn viết ít mã hơn mà vẫn đảm bảo mã dễ hiểu.

### Ví Dụ

```java
var marioGame = new MarioGame();  // Tự động hiểu là MarioGame
var gameRunner = new GameRunner(marioGame);  // Tự động hiểu là GameRunner
```

Trong ví dụ trên, **`var`** giúp trình biên dịch tự động suy luận ra kiểu của `marioGame` là `MarioGame` và `gameRunner` là `GameRunner`.

## 4. Lợi Ích Của `var`

- **Giảm thiểu sự lặp lại**: Bạn không cần phải khai báo kiểu dữ liệu ở cả hai bên của biểu thức gán.
- **Tăng tính dễ đọc**: Trong các tình huống sử dụng **generics** hoặc khi khai báo kiểu dữ liệu phức tạp, **`var`** giúp mã trở nên ngắn gọn và dễ hiểu hơn.
- **Giảm thiểu mã dư thừa**: Giúp tránh viết mã "boilerplate" – những đoạn mã dư thừa không cần thiết.

### Ví Dụ Phức Tạp

Khi sử dụng với **generics** hoặc các kiểu dữ liệu phức tạp, **`var`** thực sự giúp mã ngắn gọn hơn:

```java
// Không sử dụng var
List<String> names = new ArrayList<String>();

// Sử dụng var
var names = new ArrayList<String>();
```

Trong ví dụ này, **`var`** giúp tránh việc phải khai báo lại kiểu dữ liệu cho cả bên trái và bên phải của phép gán.

## 5. Giới Hạn Của `var`

Mặc dù **`var`** giúp mã ngắn gọn hơn, nhưng cũng có một số hạn chế cần lưu ý:

- **Chỉ có thể sử dụng khi khai báo và gán giá trị trong cùng một câu lệnh**. Bạn không thể khai báo `var` mà không gán giá trị ban đầu.
- **Không thể sử dụng cho các biến lớp (instance variables) hoặc biến toàn cục** – chỉ sử dụng cho các biến cục bộ trong phương thức.

## Kết Luận

Từ khóa **`var`** là một tính năng mạnh mẽ được giới thiệu từ Java 10 để cải thiện tính dễ đọc của mã và giảm thiểu mã dư thừa. Nó cho phép trình biên dịch tự động suy luận kiểu dữ liệu từ giá trị được gán, giúp bạn tập trung vào logic chương trình mà không cần lo lắng về việc khai báo kiểu quá chi tiết.

Trong khóa học này, chúng ta sẽ tiếp tục sử dụng **`var`** để giữ cho mã đơn giản và dễ hiểu hơn. Hãy thoải mái thử nghiệm và sử dụng **`var`** trong các dự án Java của bạn!
