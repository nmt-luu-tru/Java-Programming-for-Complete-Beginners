### Tạo Interface Game và Triển Khai Lớp GameImpl

Trong video này, chúng ta sẽ tạo **interface Game** và lớp **GameImpl**. Lớp **GameImpl** sẽ triển khai interface **Game** và sẽ chứa các trường như **numberGenerator**, **guessCount**, **number**, **smallest**, **biggest**, **remainingGuesses**, và **validNumberRange**. Chúng ta cũng sẽ triển khai các phương thức tương ứng.

#### Bước 1: Tạo Interface Game

1. **Tạo Interface Game**:
   - Chúng ta sẽ định nghĩa các phương thức cần thiết cho trò chơi.

```java
public interface Game {
    int getNumber();
    int getGuess();
    void setGuess(int guess);
    int getSmallest();
    int getBiggest();
    int getRemainingGuesses();
    void reset();
    void check();
    boolean isValidNumberRange();
    boolean isGameWon();
    boolean isGameLost();
}
```

#### Bước 2: Tạo Lớp GameImpl

1. **Tạo lớp `GameImpl`**:
   - Lớp này sẽ triển khai tất cả các phương thức từ interface **Game**. Sau đây là một số bước chi tiết.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class GameImpl implements Game {
    private static final Logger log = LoggerFactory.getLogger(GameImpl.class);

    // Các trường
    private NumberGenerator numberGenerator;
    private int guessCount = 10;
    private int number;
    private int guess;
    private int smallest;
    private int biggest;
    private int remainingGuesses;
    private boolean validNumberRange = true;

    // Phương thức reset sẽ được gọi đầu tiên
    @Override
    public void reset() {
        smallest = 0;
        guess = 0;
        remainingGuesses = guessCount;
        biggest = numberGenerator.getMaxNumber();
        number = numberGenerator.next();
        log.debug("The number is {}", number);
    }

    // Triển khai các phương thức getter và setter
    @Override
    public int getNumber() {
        return number;
    }

    @Override
    public int getGuess() {
        return guess;
    }

    @Override
    public void setGuess(int guess) {
        this.guess = guess;
    }

    @Override
    public int getSmallest() {
        return smallest;
    }

    @Override
    public int getBiggest() {
        return biggest;
    }

    @Override
    public int getRemainingGuesses() {
        return remainingGuesses;
    }

    @Override
    public boolean isValidNumberRange() {
        return validNumberRange;
    }

    @Override
    public boolean isGameWon() {
        return guess == number;
    }

    @Override
    public boolean isGameLost() {
        return !isGameWon() && remainingGuesses <= 0;
    }

    // Kiểm tra giá trị guess và điều chỉnh phạm vi đoán
    @Override
    public void check() {
        checkValidNumberRange();

        if (validNumberRange) {
            if (guess > number) {
                biggest = guess - 1;
            } else if (guess < number) {
                smallest = guess + 1;
            }
            remainingGuesses--;
        }
    }

    // Phương thức riêng kiểm tra xem guess có nằm trong phạm vi không
    private void checkValidNumberRange() {
        validNumberRange = (guess >= smallest) && (guess <= biggest);
    }
}
```

### Giải Thích

- **Các trường (`fields`)**: 
    - `numberGenerator` dùng để sinh số ngẫu nhiên mà người chơi cần đoán.
    - `guessCount` đại diện cho số lần đoán tối đa mà người chơi có thể sử dụng.
    - `smallest` và `biggest` đại diện cho phạm vi hiện tại mà người chơi cần đoán.
    - `remainingGuesses` giữ số lần đoán còn lại.

- **Phương thức `reset`**: 
    - Phương thức này sẽ được gọi khi bắt đầu trò chơi và thiết lập các giá trị mặc định cho trò chơi. 
    - Số ngẫu nhiên cần đoán được sinh từ `numberGenerator.next()`.
    - `smallest` và `biggest` được đặt về 0 và giá trị lớn nhất từ `numberGenerator`.

- **Phương thức `check`**: 
    - Phương thức này kiểm tra giá trị đoán của người chơi và điều chỉnh phạm vi nếu cần.
    - Nếu `guess` lớn hơn số cần đoán, `biggest` sẽ được điều chỉnh.
    - Nếu `guess` nhỏ hơn, `smallest` sẽ được điều chỉnh.
    - `remainingGuesses` giảm dần sau mỗi lần đoán.

- **Các phương thức khác**: 
    - Các phương thức getter trả về các giá trị hiện tại của trò chơi như `getGuess()`, `getSmallest()`, `getBiggest()`, và `getRemainingGuesses()`.
    - `isGameWon()` kiểm tra xem người chơi có đoán đúng không.
    - `isGameLost()` kiểm tra xem người chơi có hết lượt đoán không.

### Bước Tiếp Theo

Trong video tiếp theo, chúng ta sẽ kết nối lớp **NumberGenerator** và **Game** với nhau thông qua Spring IoC container.
