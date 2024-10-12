### Cấu Hình XML trong Spring Framework

Trong bước này, chúng ta sẽ tìm hiểu về cấu hình **XML** trong **Spring Framework**. Đây là phương pháp cũ hơn để cấu hình Spring trước khi các cấu hình **Java** và **annotation** được giới thiệu. Mặc dù hiện nay **Java configuration** và **annotations** được sử dụng phổ biến hơn, nhưng việc hiểu cấu hình XML vẫn rất quan trọng, đặc biệt khi bạn làm việc với các dự án cũ.

### 1. **Cấu Hình XML So Với Java Configuration**

Khi làm việc với Spring Framework, hiện tại ta có thể sử dụng **Java configuration** bằng cách sử dụng các annotations như **@Configuration** và **@ComponentScan** để khai báo các bean và định nghĩa cấu hình. Tuy nhiên, trong quá khứ, tất cả các cấu hình này được thực hiện thông qua **XML files**.

### 2. **Tạo Tệp Cấu Hình XML**

Để sử dụng cấu hình XML, ta cần tạo một file XML mới để định nghĩa các bean.

#### Bước 1: Tạo tệp XML trong thư mục `src/main/resources`
- Tạo một tệp XML tên là `contextConfiguration.xml` trong thư mục `src/main/resources`.
- Trong tệp này, ta định nghĩa các bean bằng cách sử dụng cú pháp XML.

**Ví dụ cấu hình một chuỗi (String) và một số nguyên (Integer):**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <!-- Định nghĩa bean chuỗi -->
    <bean id="name" class="java.lang.String">
        <constructor-arg value="Ranga"/>
    </bean>
    
    <!-- Định nghĩa bean số nguyên -->
    <bean id="age" class="java.lang.Integer">
        <constructor-arg value="35"/>
    </bean>

</beans>
```

#### Bước 2: Khởi chạy Spring Context từ XML
- Để khởi chạy Spring context từ file XML, ta sử dụng **ClassPathXmlApplicationContext** thay vì **AnnotationConfigApplicationContext**.

**Ví dụ:**
```java
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class XmlConfigurationContextLauncherApplication {
    public static void main(String[] args) {
        try (var context = new ClassPathXmlApplicationContext("contextConfiguration.xml")) {
            System.out.println(context.getBean("name"));
            System.out.println(context.getBean("age"));
        }
    }
}
```
Kết quả sẽ in ra giá trị `"Ranga"` và `35`.

### 3. **Sử Dụng Component Scan Trong XML**

Cũng giống như khi sử dụng **@ComponentScan** trong Java configuration, trong XML ta có thể quét các packages để tự động phát hiện các bean với **context:component-scan**.

**Ví dụ về component scan trong XML:**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- Component Scan cho package cụ thể -->
    <context:component-scan base-package="com.in28minutes.learnspringframework.game" />

</beans>
```

### 4. **Injection Trong XML: Constructor Injection**

Chúng ta có thể sử dụng **constructor injection** trong XML để tiêm các phụ thuộc vào các bean.

**Ví dụ:**

```xml
<bean id="pacmanGame" class="com.in28minutes.learnspringframework.game.PacmanGame"/>
<bean id="gameRunner" class="com.in28minutes.learnspringframework.game.GameRunner">
    <constructor-arg ref="pacmanGame"/>
</bean>
```

Trong đó, bean `gameRunner` sẽ nhận phụ thuộc từ bean `pacmanGame` thông qua **constructor injection**.

### 5. **Tại Sao Hiểu XML Configuration Quan Trọng**

Mặc dù cấu hình XML không còn được sử dụng rộng rãi trong các dự án mới, nhưng nhiều dự án cũ vẫn sử dụng phương pháp này. Hiểu cách cấu hình và quản lý các bean thông qua XML giúp bạn làm việc với các hệ thống kế thừa dễ dàng hơn.

### 6. **Kết Luận**

- **Java configuration** với annotations như **@Configuration** và **@Component** là phương pháp hiện đại và dễ sử dụng hơn so với XML.
- **XML configuration** vẫn hữu ích, đặc biệt khi bạn cần tương thích với các dự án cũ.
- Trong XML, bạn có thể định nghĩa các bean, tiêm phụ thuộc và sử dụng **component scan** giống như trong cấu hình Java.

Hy vọng bạn đã có một cái nhìn rõ ràng hơn về cách cấu hình Spring thông qua XML. Hẹn gặp lại bạn ở bước tiếp theo!
