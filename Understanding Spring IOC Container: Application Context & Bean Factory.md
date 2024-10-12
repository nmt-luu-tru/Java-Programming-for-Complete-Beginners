### Spring Container là gì?

**Spring Container** (còn gọi là **Spring Context** hoặc **IOC Container**) chịu trách nhiệm quản lý **Spring Beans** và vòng đời của chúng. Spring Container tạo và quản lý các bean dựa trên cấu hình do người dùng cung cấp, chẳng hạn như các lớp Java và các file cấu hình.

#### Cách hoạt động của Spring Container

- **Đầu vào**:
  - Các lớp Java (như `Person`, `Address`, v.v.)
  - Các file cấu hình (như `HelloWorldConfiguration`), trong đó định nghĩa các bean.

- **Đầu ra**:
  - Một hệ thống chạy được quản lý bởi **Spring Context**. Khi ứng dụng chạy, hệ thống này sẽ quản lý tất cả các bean và các phụ thuộc của chúng bên trong JVM.

**Spring Container** đảm nhiệm việc tạo ra, cấu hình và quản lý các bean, cũng như mối quan hệ giữa chúng. Nói cách khác, nó xây dựng và vận hành ứng dụng dựa trên các bean và cấu hình được cung cấp.

#### Các loại Spring Container

1. **BeanFactory**:
   - Là **Spring Container** cơ bản và nhẹ.
   - Quản lý các bean nhưng không có các tính năng nâng cao của doanh nghiệp.
   - Thích hợp cho các môi trường có hạn chế về bộ nhớ như các ứng dụng IoT.

2. **ApplicationContext**:
   - Là **Spring Container** nâng cao với các tính năng mở rộng dành cho doanh nghiệp như:
     - **Hỗ trợ quốc tế hóa** (i18n)
     - Tích hợp với **Spring AOP** (Lập trình Hướng khía cạnh)
     - **Hỗ trợ ứng dụng web**
   - Thường được sử dụng trong hầu hết các ứng dụng doanh nghiệp, dịch vụ web, REST API và microservices.

#### Những điểm chính:
- **Spring Container** = **Spring Context** = **IOC Container**.
- **ApplicationContext** mạnh mẽ hơn và thường được sử dụng trong các ứng dụng doanh nghiệp, đặc biệt là phát triển web.

Trong bước này, chúng ta đã có cái nhìn tổng quan về cách **Spring Container** hoạt động, vai trò của nó trong ứng dụng, và sự khác biệt giữa **BeanFactory** và **ApplicationContext**. Chúng ta sẽ tìm hiểu sâu hơn về các khái niệm này trong những bài học tiếp theo.
