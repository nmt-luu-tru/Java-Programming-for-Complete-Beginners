### Triển khai logic cho MessageGenerator

#### Mục tiêu:
Trong video này, chúng ta sẽ hoàn thành việc triển khai logic cho các phương thức `getMainMessage()` và `getResultMessage()` trong lớp **MessageGeneratorImpl**. Những phương thức này sẽ hiển thị các thông báo dựa trên tiến trình của trò chơi.

#### **Bước 1: Triển khai `getMainMessage()`**

Phương thức `getMainMessage()` sẽ trả về thông điệp mô tả khoảng giá trị của số cần đoán. Dưới đây là cách triển khai:

```java
@Override
public String getMainMessage() {
    return "Number is between " + game.getSmallest() + " and " + game.getBiggest() + ". Can you guess it?";
}
```

Ở đây, chúng ta sử dụng các phương thức `getSmallest()` và `getBiggest()` từ đối tượng **Game** để lấy khoảng giá trị của số bí mật và hiển thị thông điệp "Can you guess it?" để thách thức người chơi đoán số.

---

#### **Bước 2: Triển khai `getResultMessage()`**

Phương thức này sẽ trả về thông điệp dựa trên giá trị mà người chơi đã đoán. Chúng ta sẽ kiểm tra nếu người chơi đoán đúng, đoán sai, hoặc đoán không hợp lệ.

```java
@Override
public String getResultMessage() {
    if (game.isGameWon()) {
        return "You guessed it! The number was " + game.getNumber();
    } else if (game.isGameLost()) {
        return "You lost. The number was " + game.getNumber();
    } else if (!game.isValidNumberRange()) {
        return "Invalid number range!";
    } else if (game.getRemainingGuesses() == guessCount) {
        return "What is your first guess?";
    } else {
        String direction = (game.getGuess() < game.getNumber()) ? "Higher" : "Lower";
        return direction + "! You have " + game.getRemainingGuesses() + " guesses left.";
    }
}
```

#### **Giải thích logic:**
- **Kiểm tra thắng/thua:** Nếu người chơi đoán đúng, sẽ hiện thông điệp "You guessed it! The number was ..." và nếu thua, sẽ hiện "You lost. The number was ...".
- **Kiểm tra số đoán không hợp lệ:** Nếu số đoán không nằm trong khoảng hợp lệ, hiển thị "Invalid number range!".
- **Kiểm tra nếu đó là lần đoán đầu tiên:** Nếu số lần đoán còn lại bằng với giá trị khởi tạo `guessCount`, hiển thị "What is your first guess?".
- **So sánh giá trị đoán với số bí mật:** Nếu số đoán nhỏ hơn số bí mật, hiển thị "Higher", ngược lại hiển thị "Lower", kèm theo số lần đoán còn lại.

---

### **Kiểm tra ứng dụng**

Sau khi đã triển khai logic cho hai phương thức, chúng ta chạy lại ứng dụng để kiểm tra kết quả. Khi chạy, chương trình sẽ hiển thị các thông điệp phù hợp với tiến trình của trò chơi.

Ví dụ:
- Nếu người chơi đoán đúng: "You guessed it! The number was 42."
- Nếu người chơi thua: "You lost. The number was 42."
- Nếu đoán sai: "Higher! You have 9 guesses left."

---

### **Tóm tắt**

Chúng ta đã hoàn thành việc triển khai logic cho phương thức `getMainMessage()` và `getResultMessage()`, giúp trò chơi phản hồi dựa trên hành động của người chơi. Trong video tiếp theo, chúng ta sẽ tạo một module console để chạy trò chơi từ dòng lệnh, và sau đó sẽ phát triển phiên bản web của trò chơi khi chúng ta giới thiệu Spring MVC.
