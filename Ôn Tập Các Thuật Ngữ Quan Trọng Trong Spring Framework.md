### Ôn Tập Các Thuật Ngữ Quan Trọng Trong Spring Framework

Trong bước này, chúng ta sẽ xem lại một số thuật ngữ quan trọng thường được sử dụng trong **Spring Framework**. Đây là những khái niệm cơ bản và cốt lõi của Spring mà chúng ta đã sử dụng trong các bước trước.

#### 1. **@Component**
Khi bạn thêm **@Component** vào một lớp, **Spring Framework** sẽ quản lý một instance của lớp đó. 
- **@Component** là một trong những annotation quan trọng nhất trong **Spring**.
- Khi bạn khai báo **@Component**, và nếu lớp đó nằm trong phạm vi của **component scan**, Spring sẽ tạo ra một **Spring Bean** và quản lý nó.
- Ví dụ: Chúng ta đã sử dụng **@Component** trên các lớp như **GameRunner**, **MarioGame**, **YourBusinessClass**, và các phụ thuộc như **Dependency1** và **Dependency2**.

#### 2. **Dependency**
Một **dependency** là một thành phần mà một lớp khác cần để hoạt động. 
- Ví dụ: **GameRunner** cần một implementation của **GamingConsole**, có thể là **MarioGame**, **SuperContra**, hoặc **PacMan**.
- **MarioGame** là một dependency của **GameRunner**.

#### 3. **Component Scan**
Spring cần biết nơi để tìm kiếm các **components** (bean) mà nó sẽ quản lý. 
- Bạn có thể chỉ định nơi Spring tìm kiếm **components** bằng cách sử dụng annotation **@ComponentScan**.
- **@ComponentScan** cho phép bạn chỉ định package cần quét. Nếu không chỉ định, Spring sẽ quét package hiện tại và các sub-packages.

#### 4. **Dependency Injection**
**Dependency Injection (DI)** là quá trình mà **Spring** tự động xác định và tiêm các phụ thuộc vào các **beans**.
- Khi chạy ứng dụng, Spring sẽ tìm kiếm các **components**, xác định phụ thuộc của chúng, và tiêm các đối tượng cần thiết vào.
- DI giúp quản lý mối quan hệ giữa các đối tượng dễ dàng và linh hoạt hơn.

#### 5. **Inversion of Control (IoC)**
**Inversion of Control (IoC)** là quá trình mà Spring quản lý vòng đời và việc tạo đối tượng thay vì lập trình viên phải tự tay thực hiện.
- Ban đầu, lập trình viên viết mã để tạo đối tượng và quản lý phụ thuộc. Nhưng với Spring, bạn chỉ cần định nghĩa **@Component** và **@ComponentScan**, còn Spring sẽ lo việc tạo và quản lý đối tượng.
- Đây là sự **đảo ngược** quyền kiểm soát từ lập trình viên sang Spring Framework, do đó gọi là **Inversion of Control**.

#### 6. **Spring Beans**
- **Spring Bean** là bất kỳ đối tượng nào được Spring Framework quản lý.
- Các **Spring Beans** được tạo ra và quản lý thông qua **IoC Container**.

#### 7. **IoC Container (Inversion of Control Container)**
**IoC Container** là thành phần của **Spring Framework** chịu trách nhiệm quản lý vòng đời của các **Spring Beans** và tiêm phụ thuộc. 
- Có hai loại **IoC Container**:
  - **ApplicationContext**: Cung cấp nhiều tính năng phức tạp như quản lý các **beans**, hỗ trợ sự kiện, và tích hợp quốc tế hóa.
  - **BeanFactory**: Cung cấp tính năng đơn giản hơn và ít được sử dụng trong các ứng dụng hiện đại.

#### 8. **Autowiring**
**Autowiring** là quá trình tự động tiêm các phụ thuộc vào **Spring Bean**.
- Khi Spring phát hiện rằng một lớp cần phụ thuộc, nó sẽ tự động tiêm các đối tượng thích hợp thông qua **constructor**, **setter**, hoặc **field injection**.

Ví dụ:
- **GameRunner** yêu cầu một **GamingConsole**, khi Spring phát hiện điều này thông qua **constructor** của **GameRunner**, nó sẽ tự động tìm và tiêm một **GamingConsole** vào (ví dụ: **MarioGame** hoặc **PacMan**).

### Tổng Kết
- **@Component**: Định nghĩa một lớp là **Spring Bean** và được Spring quản lý.
- **Dependency Injection (DI)**: Spring tự động tiêm các phụ thuộc cho các bean.
- **Inversion of Control (IoC)**: Spring quản lý việc tạo và vòng đời của các đối tượng thay vì lập trình viên.
- **Autowiring**: Quá trình Spring tự động tiêm các phụ thuộc cần thiết vào các bean.
- **ApplicationContext**: IoC Container được sử dụng nhiều nhất trong Spring Framework để quản lý bean.

Các khái niệm này có mối quan hệ chặt chẽ với nhau và là nền tảng để hiểu rõ cách **Spring Framework** hoạt động. Hãy chắc chắn rằng bạn hiểu rõ những thuật ngữ này khi làm việc với Spring. 

Hẹn gặp bạn ở bước tiếp theo!
