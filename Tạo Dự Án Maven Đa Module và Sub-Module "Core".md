### Tạo Dự Án Maven Đa Module và Sub-Module "Core"

Trong phần này, chúng ta sẽ học cách tạo một **dự án Maven đa module** và sau đó tạo một sub-module **core**. Để dễ dàng thực hiện các bước này, bạn cần mở dự án **hello Maven** mà chúng ta đã làm ở phần trước của khóa học, vì chúng ta sẽ sao chép và dán một số thành phần từ đó.

#### Bước 1: Tạo dự án mới
- Mở **IntelliJ**, chọn **File** > **New Project**.
- Chọn **Maven** và đảm bảo rằng phiên bản JDK mới nhất đang được chọn (trong ví dụ này là JDK 10).
- Nhập **group ID** là `Academy.learnprogramming` và **artifact ID** là `guess-the-number` (đây là tên cho trò chơi mà chúng ta sẽ phát triển trong phần này).
- Chọn nơi lưu trữ dự án. Bạn có thể lưu nó ở bất kỳ thư mục nào trên máy tính, nhưng hãy nhớ IntelliJ sẽ tự động tạo một thư mục con cho mỗi dự án mới.

#### Bước 2: Chuyển đổi dự án thành dự án đa module
Để tạo một dự án Maven đa module, chúng ta cần:
1. **Tạo dự án cha (parent project)**, nơi không chứa mã nguồn mà chỉ đóng vai trò chứa các sub-module.
2. **Tạo các dự án con (sub-modules)**.

Trước tiên, hãy xóa thư mục `src` vì dự án cha không cần mã nguồn. Nhấp chuột phải vào thư mục `src` và chọn **Delete**.

Sau đó, mở tệp **pom.xml** của dự án cha và thêm thẻ **packaging** để định nghĩa dự án này là một dự án **pom**:
```xml
<packaging>pom</packaging>
```
Thẻ này cho Maven biết rằng dự án cha sẽ chứa các sub-module, và bản thân nó sẽ không có mã nguồn để biên dịch.

#### Bước 3: Tạo sub-module "Core"
Để tạo một sub-module, thực hiện các bước sau:
1. Nhấp chuột phải vào tên dự án trong **Project View** > **New** > **Module**.
2. Chọn **Maven** và nhấn **Next**. Lúc này, bạn chỉ cần nhập **artifact ID** cho sub-module vì **group ID** và **version** sẽ được kế thừa từ dự án cha. Trong trường hợp này, nhập **artifact ID** là `core`.
3. Nhấn **Finish** để hoàn thành quá trình tạo module.

Kết quả sẽ là bạn có một sub-module `core` với thư mục mã nguồn riêng (`src/main/java` và `src/main/resources`).

#### Bước 4: Hiểu cách các module và pom.xml hoạt động
- **Dự án cha (parent pom)**: Dự án cha có tệp `pom.xml` chứa thông tin về các sub-module. Bạn sẽ thấy rằng Maven đã tự động thêm thẻ `<modules>` và liệt kê module `core` bên trong đó.
- **Dự án con (core pom)**: Tệp `pom.xml` của module `core` sẽ kế thừa các thuộc tính từ dự án cha. Bạn sẽ thấy một thẻ `<parent>` trong tệp này, nó chỉ ra rằng module `core` thuộc về dự án cha.

Một điều thú vị là khi bạn nhấn vào các biểu tượng mũi tên trong **IntelliJ** cạnh thẻ **parent** hoặc **modules**, bạn có thể di chuyển dễ dàng giữa tệp `pom.xml` của dự án cha và con.

#### Bước 5: Chạy các lệnh Maven
Để đảm bảo rằng mọi thứ được thiết lập đúng cách, hãy chạy các lệnh Maven để kiểm tra quá trình biên dịch:
1. Mở **Maven Projects** ở bên phải IntelliJ.
2. Chọn root project (dự án gốc, không phải sub-module).
3. Chạy lệnh `clean` và `install` bằng cách gõ `clean install` vào mục **Goals** và nhấn **Execute**.

Kết quả của quá trình này sẽ cho thấy Maven tự động xử lý thứ tự biên dịch các module (dự án cha trước, sau đó đến module `core`).

#### Kết Luận
Chúng ta đã tạo thành công một dự án Maven đa module với một sub-module `core`. Dự án đa module giúp chúng ta dễ dàng quản lý mã nguồn, tách biệt các thành phần logic, và tái sử dụng mã trong tương lai. Ở video tiếp theo, chúng ta sẽ thiết lập các phụ thuộc (dependencies) cho dự án và tiếp tục phát triển thêm các module khác.
