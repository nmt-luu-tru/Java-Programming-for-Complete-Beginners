### CDI (Contexts and Dependency Injection) trong Jakarta EE và Spring Framework

Trong bước này, chúng ta sẽ tìm hiểu về **Jakarta Contexts and Dependency Injection (CDI)**. CDI là một **specification** của **Jakarta EE** nhằm quản lý vòng đời của các đối tượng và thực hiện **dependency injection** (tiêm phụ thuộc). CDI và các annotations của nó có chức năng tương tự như các annotations trong **Spring Framework**, và Spring cũng hỗ trợ CDI, cho phép sử dụng các annotations như **@Inject** và **@Named**.

### 1. **CDI và Spring**
- **CDI** là một **specification**, tức là nó chỉ định một tập hợp các **API** nhưng không có triển khai cụ thể. 
- **Spring Framework** cũng hỗ trợ CDI và có thể sử dụng các annotations của CDI như **@Inject** và **@Named** thay vì **@Autowired** và **@Component** của Spring.

### 2. **Cách Thêm CDI Vào Dự Án**
Để sử dụng CDI trong dự án Spring, bạn cần thêm dependency **jakarta.inject** vào file **POM.xml**.

**Ví dụ:**
```xml
<dependency>
    <groupId>jakarta.inject</groupId>
    <artifactId>jakarta.inject-api</artifactId>
    <version>2.0.1</version>
</dependency>
```

Sau khi thêm dependency, Spring sẽ tự động hỗ trợ các annotations của CDI.

### 3. **Ví Dụ Về CDI trong Spring**

Chúng ta sẽ xem xét một ví dụ trong đó sử dụng các annotations **@Inject** và **@Named** từ CDI thay thế cho **@Autowired** và **@Component** trong Spring.

**BusinessService**:
```java
import jakarta.inject.Inject;
import jakarta.inject.Named;

@Named
public class BusinessService {
    
    private DataService dataService;
    
    @Inject
    public void setDataService(DataService dataService) {
        this.dataService = dataService;
    }
    
    public DataService getDataService() {
        return dataService;
    }
}
```

**DataService**:
```java
import jakarta.inject.Named;

@Named
public class DataService {
    // Các phương thức của DataService
}
```

**CDIContextLauncherApplication**:
```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class CDIContextLauncherApplication {

    public static void main(String[] args) {
        try (var context = new AnnotationConfigApplicationContext(CDIContextLauncherApplication.class)) {
            
            // Lấy BusinessService bean từ Spring Context
            BusinessService businessService = context.getBean(BusinessService.class);
            
            // In ra DataService để kiểm tra việc tiêm phụ thuộc
            System.out.println("DataService is: " + businessService.getDataService());
        }
    }
}
```

### 4. **So Sánh @Inject và @Autowired**
- **@Inject**: Đến từ **CDI**, có chức năng tương tự như **@Autowired** trong Spring. Dùng để tiêm phụ thuộc.
- **@Named**: Được sử dụng thay thế cho **@Component** của Spring. Nó đánh dấu một class là một bean và để Spring quản lý.

**Ví dụ so sánh:**

- Với Spring:
  ```java
  @Component
  public class DataService {
      // Các phương thức của DataService
  }
  ```
  ```java
  @Autowired
  private DataService dataService;
  ```

- Với CDI:
  ```java
  @Named
  public class DataService {
      // Các phương thức của DataService
  }
  ```
  ```java
  @Inject
  private DataService dataService;
  ```

### 5. **Kết Luận**
- **CDI** là một tiêu chuẩn trong **Jakarta EE** và Spring Framework hỗ trợ các annotations của CDI như **@Inject** và **@Named**. Chúng là các thay thế cho **@Autowired** và **@Component** trong Spring.
- **@Inject** dùng để tiêm phụ thuộc, tương tự như **@Autowired**.
- **@Named** đánh dấu một class là bean, tương tự như **@Component**.

CDI và Spring Framework có thể hoạt động song song, và hiểu về CDI sẽ giúp bạn làm việc với các dự án sử dụng Jakarta EE hoặc Spring Framework dễ dàng hơn.

Hẹn gặp lại bạn ở bước tiếp theo!
