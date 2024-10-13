### Giải quyết thử thách: Tạo module Maven mới cho console

#### Mục tiêu:
- Tạo một **module Maven** mới có tên là **console**.
- Thêm **core project** làm dependency.
- Di chuyển **main class** sang module **console** mới.
- Chạy **main class** từ module **console** và đảm bảo rằng dự án hoạt động tương tự như trước.

#### **Bước 1: Tạo module Maven mới**
1. **Tạo module mới**: Trong IntelliJ, click chuột phải vào tên project ở bảng bên trái -> **New** -> **Module**.
2. Chọn **Maven**, đặt tên module là **console**.
3. Hệ thống sẽ tự động thừa kế **group ID** và **version** từ project cha, vì vậy không cần phải nhập lại.
4. **Click "Finish"** để hoàn tất việc tạo module.

#### **Bước 2: Thêm phụ thuộc vào core module**
1. **Mở file `pom.xml`** của module **console** vừa tạo.
2. Thêm dependency vào **core module**:

```xml
<dependencies>
    <dependency>
        <groupId>Academy.learnprogramming</groupId>
        <artifactId>core</artifactId>
        <version>${project.version}</version>
    </dependency>
</dependencies>
```

Ở đây, chúng ta sử dụng `${project.version}` để đảm bảo rằng phiên bản của **core module** sẽ luôn đồng nhất với phiên bản của project chính.

#### **Bước 3: Di chuyển lớp `Main`**
1. Tạo package mới trong module **console**: **Academy.learnprogramming.console**.
2. Di chuyển file **Main.java** từ module **core** sang package mới vừa tạo trong module **console**.
3. Khi di chuyển, bạn có thể nhận được một số lỗi biên dịch liên quan đến các thư viện (như SLF4J và Spring). Điều này xảy ra vì các dependency của module **core** chưa được thêm vào module **console**.

#### **Bước 4: Thêm các dependency cần thiết**
Vì các thư viện như **SLF4J** và **Spring** đã được khai báo trong module **core**, nên chúng ta không cần khai báo lại trong module **console**. Các dependency này sẽ được tự động thêm vào nhờ **transitive dependencies** từ **core**.

#### **Bước 5: Kiểm tra và sửa lỗi biên dịch**
Nếu IntelliJ không tự động tối ưu các import, bạn có thể cần:
1. Nhấn **Alt + Enter** để tự động sửa các import còn thiếu.
2. Hoặc vào **Code -> Optimize Imports** để tự động sửa.

#### **Bước 6: Chạy chương trình**
- Sau khi di chuyển lớp **Main** và sửa các lỗi biên dịch, hãy chạy lại chương trình từ module **console** để đảm bảo rằng mọi thứ hoạt động như mong đợi.
- Khi chạy chương trình, bạn sẽ thấy thông báo như: **"What is your first guess?"** xuất hiện trong console.

#### **Tóm tắt**
- Trong thử thách này, chúng ta đã tạo một module Maven mới có tên **console**, thêm dependency vào module **core**, di chuyển lớp **Main** sang module mới, và đảm bảo rằng dự án vẫn hoạt động tốt.
- Quá trình này cũng giúp bạn làm quen với cách cấu hình và sử dụng **transitive dependencies** trong Maven.

Trong video tiếp theo, chúng ta sẽ tiếp tục tìm hiểu về **application events** và cách xử lý các sự kiện trong Spring container.
