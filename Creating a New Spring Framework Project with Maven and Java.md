# Hướng Dẫn Tạo Dự Án Spring

## Bước 1: Tạo Dự Án Spring Từ Spring Initializr

### 1. Truy cập Spring Initializr

Để tạo một dự án Spring nhanh chóng và dễ dàng, bạn có thể truy cập vào trang web [Spring Initializr](https://start.spring.io). Đây là công cụ trực tuyến được cung cấp bởi Spring, giúp bạn thiết lập dự án với cấu hình ban đầu và các thư viện cần thiết chỉ với vài thao tác.

### 2. Cấu hình dự án

Tại trang Spring Initializr, bạn sẽ thấy một giao diện nơi bạn có thể tùy chỉnh cấu hình cho dự án của mình. Hãy làm theo các bước dưới đây để thiết lập dự án:

- **Project Type**: Chọn **Maven Project**. Maven sẽ là công cụ quản lý và xây dựng dự án mà chúng ta sẽ sử dụng.
- **Language**: Chọn **Java** làm ngôn ngữ lập trình.
- **Spring Boot Version**: Chọn phiên bản **Spring Boot 3.0.0 RC1** (Release Candidate 1). Nếu bạn thấy phiên bản ổn định (released version) của Spring Boot 3, ví dụ như **3.0.1** hoặc **3.1.0**, hãy chọn phiên bản đó thay vì sử dụng phiên bản snapshot hoặc RC (Release Candidate).
- **Group**: Nhập `com.in28minutes`.
- **Artifact**: Nhập `learn-spring-framework`.
- **Name**: Nhập tên dự án của bạn, ví dụ `LearnSpringFramework`.
- **Description**: Mô tả ngắn gọn cho dự án, ví dụ `A Spring Framework learning project`.
- **Package Name**: Sẽ tự động được điền dựa trên Group và Artifact đã nhập ở trên, ví dụ: `com.in28minutes.learnspringframework`.
- **Packaging**: Chọn **Jar** (file thực thi dưới dạng .jar).
- **Java Version**: Chọn **Java 17** hoặc phiên bản Java mới nhất mà bạn đang sử dụng.

### 3. Thêm các thư viện cần thiết

Chọn các dependency (thư viện phụ thuộc) mà bạn muốn sử dụng trong dự án. Để bắt đầu, bạn có thể chọn:

- **Spring Web**: Cung cấp các tính năng phát triển ứng dụng web cơ bản.
- **Spring Boot DevTools**: Công cụ hỗ trợ phát triển, giúp tái khởi động ứng dụng tự động khi có thay đổi trong mã nguồn.
- **Spring Data JPA**: Hỗ trợ tương tác với cơ sở dữ liệu.
- **H2 Database**: Cơ sở dữ liệu nhúng cho việc thử nghiệm.

### 4. Tải dự án

Sau khi hoàn tất cấu hình, nhấn nút **Generate** để tải xuống file nén (.zip) chứa dự án của bạn. File sẽ được tải xuống thư mục `Downloads` trên máy tính của bạn.

## Bước 2: Giải Nén Dự Án

Sau khi tải xuống file .zip, hãy thực hiện các bước sau:

1. Giải nén file vào một thư mục trên máy tính của bạn, ví dụ: `C:/SpringProjects/`.
2. Bạn sẽ thấy cấu trúc thư mục dự án được tạo ra như sau:
   - **src/main/java**: Chứa các file mã nguồn Java.
   - **src/main/resources**: Chứa các file cấu hình như `application.properties`.
   - **src/test/java**: Chứa mã nguồn phục vụ việc kiểm thử (test).

## Bước 3: Import Dự Án Vào IDE

### 1. Mở IDE (Eclipse)

Mở Eclipse IDE. Nếu bạn chưa cài đặt Eclipse, hãy tải phiên bản mới nhất từ [eclipse.org](https://www.eclipse.org/downloads/). Đảm bảo bạn sử dụng phiên bản Eclipse cho **Enterprise Java và Web Developers** để tương thích tốt nhất với Spring Boot.

### 2. Thiết lập Workspace

Khi mở Eclipse, bạn sẽ được yêu cầu chọn một **workspace** (thư mục làm việc) cho các dự án của mình. Chọn một thư mục hoặc để mặc định theo cấu hình của Eclipse.

### 3. Import Dự Án

Thực hiện các bước sau để import dự án:

1. Trên thanh menu, chọn **File** -> **Import**.
2. Trong cửa sổ **Import**, gõ “Maven” vào ô tìm kiếm và chọn **Existing Maven Projects**. Nhấn **Next**.
3. Chọn **Browse** để tìm đến thư mục mà bạn đã giải nén dự án Spring ở bước trước (ví dụ: `C:/SpringProjects/learn-spring-framework`).
4. Nhấn **Open**, bạn sẽ thấy file `pom.xml` xuất hiện. Đây là file cấu hình của dự án Maven.
5. Nhấn **Finish** để hoàn tất quá trình import.

### 4. Kiểm tra cấu trúc dự án

Sau khi import thành công, bạn sẽ thấy cấu trúc dự án trong Eclipse như sau:

- **src/main/java**: Chứa các file mã nguồn Java.
- **src/main/resources**: Chứa các file cấu hình.
- **src/test/java**: Chứa các file kiểm thử.

## Bước 4: Khởi Chạy Dự Án

Để khởi chạy dự án, thực hiện các bước sau:

1. Trong Project Explorer (hoặc Package Explorer), nhấp chuột phải vào dự án của bạn.
2. Chọn **Run As** -> **Spring Boot App**.
3. Eclipse sẽ bắt đầu biên dịch và khởi chạy ứng dụng của bạn. Bạn sẽ thấy log thông báo trong console, hiển thị trạng thái khởi động của ứng dụng.

## Lưu Ý Khi Tạo Và Import Dự Án Spring

- **Không Sử Dụng Các Phiên Bản Snapshot**: Phiên bản snapshot là các phiên bản đang được phát triển và chưa ổn định. Không nên sử dụng chúng khi bạn đang học hoặc xây dựng dự án mới.
- **Sử Dụng Phiên Bản Released**: Hãy chọn các phiên bản đã phát hành chính thức như **2.7.5** hoặc **3.0.1**. Các phiên bản này không chứa các nhãn như `RC1`, `M1`, `M2`...
- **Sử Dụng Eclipse Mới Nhất**: Đảm bảo rằng bạn đang sử dụng phiên bản Eclipse IDE mới nhất để tránh các vấn đề tương thích khi import dự án.

## Kết Luận

Trong bước này, chúng ta đã tạo thành công một dự án Spring với cấu hình cơ bản từ Spring Initializr và import dự án vào IDE. Ở bước tiếp theo, chúng ta sẽ bắt đầu khám phá các tính năng của Spring Framework và triển khai các ứng dụng mẫu. Hãy bắt đầu viết mã và khám phá Spring Framework trong các bài học tiếp theo!
