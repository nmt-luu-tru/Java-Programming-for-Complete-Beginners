### Hoàn thiện Logic của Trò chơi

Trong video này, chúng ta sẽ hoàn thiện logic của trò chơi và kiểm tra tính năng hoạt động bằng cách chơi thử. Cụ thể, chúng ta cần hoàn thành lớp **ConsoleNumberGuess** với vòng lặp chính cho trò chơi, nơi người chơi sẽ nhập các giá trị dự đoán qua **console**.

#### **Bước 1: Thêm các biến được Auto-wired**
Đầu tiên, chúng ta cần auto-wire các bean **Game** và **MessageGenerator** vào lớp **ConsoleNumberGuess**. Điều này cho phép chúng ta sử dụng chúng để kiểm soát trò chơi và tạo thông điệp cho người chơi.

```java
@Component
public class ConsoleNumberGuess {
    @Autowired
    private Game game;

    @Autowired
    private MessageGenerator messageGenerator;

    private static final Logger log = LoggerFactory.getLogger(ConsoleNumberGuess.class);
    
    @EventListener
    public void start(ContextRefreshedEvent event) {
        log.info("Container ready for use.");

        Scanner scanner = new Scanner(System.in);

        while (true) { // Vòng lặp chính của trò chơi
            System.out.println(messageGenerator.getMainMessage());
            System.out.println(messageGenerator.getResultMessage());

            // Nhập dự đoán từ người chơi
            int guess = scanner.nextInt();
            scanner.nextLine(); // Để xử lý phím Enter
            game.setGuess(guess);
            game.check();

            if (game.isGameWon() || game.isGameLost()) {
                System.out.println(messageGenerator.getResultMessage());
                System.out.println("Play again? y/n");

                String playAgainString = scanner.nextLine();
                if (!playAgainString.equalsIgnoreCase("y")) {
                    break; // Thoát vòng lặp nếu người chơi không muốn tiếp tục
                }

                game.reset(); // Khởi động lại trò chơi
            }
        }
    }
}
```

#### **Bước 2: Giải thích logic trò chơi**
- **Vòng lặp vô hạn (`while true`)**: Vòng lặp này sẽ tiếp tục chạy cho đến khi người chơi thắng hoặc thua trò chơi và quyết định không chơi lại.
- **Nhập giá trị dự đoán**: Sử dụng lớp **Scanner** để đọc giá trị số mà người chơi nhập. Sau đó, gọi phương thức `game.setGuess(guess)` để cập nhật dự đoán và `game.check()` để kiểm tra xem người chơi đã đoán đúng hay sai.
- **Kiểm tra trạng thái trò chơi**: Nếu trò chơi đã thắng hoặc thua, hiển thị kết quả và hỏi người chơi có muốn chơi lại không. Nếu người chơi nhập "y", trò chơi sẽ được reset, nếu không, vòng lặp sẽ kết thúc.

#### **Bước 3: Kiểm tra và chơi thử**
1. Sau khi hoàn tất cài đặt, chúng ta sẽ chạy chương trình và nhập các giá trị để chơi thử.

Ví dụ:
```bash
Number is between 0 and 100. Can you guess it?
50
Number is between 0 and 49. Can you guess it?
25
Number is between 0 and 24. Can you guess it?
12
...
You guessed it! The number was 11. Play again? y/n
```

#### **Bước 4: Khắc phục vấn đề nhỏ**
Trong quá trình chơi thử, có thể bạn sẽ gặp một số vấn đề nhỏ như thông báo về số lượng "guesses left" không chính xác. Điều này có thể được chỉnh sửa bằng cách kiểm tra và sửa đổi thông báo đầu ra trong phương thức `getResultMessage()` của lớp **MessageGeneratorImpl**.

### **Tổng kết**
Chúng ta đã hoàn thiện logic chính của trò chơi với các bước nhập giá trị dự đoán và kiểm tra kết quả. Trò chơi hiện đã có thể chạy và cho phép người chơi chơi lại. Trong video tiếp theo, chúng ta sẽ xem xét các vấn đề còn lại và cải thiện mã nguồn, đồng thời học cách sử dụng **qualifiers** để tiêm hai bean cùng loại vào trong Spring.
