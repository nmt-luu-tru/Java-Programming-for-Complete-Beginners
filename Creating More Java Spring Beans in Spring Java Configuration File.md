

# Tạo Nhiều Spring Bean Và Giới Thiệu Về Record Trong Java

## 1. Giới Thiệu Về Spring Bean

Trong Spring Framework, **Spring bean** là các đối tượng được Spring quản lý. Khi một đối tượng trở thành một **Spring bean**, Spring sẽ kiểm soát vòng đời của nó, từ việc tạo ra cho đến khi hủy. Điều này giúp loại bỏ sự phức tạp khi phải tự tay quản lý đối tượng và phụ thuộc trong mã nguồn.

Trong bước trước, chúng ta đã tạo một **Spring context** và để Spring quản lý một đối tượng đơn giản (chuỗi **name**). Bây giờ, chúng ta sẽ mở rộng để tạo thêm nhiều **Spring beans**, bao gồm cả các kiểu dữ liệu phức tạp như các **custom class**.

## 2. Giới Thiệu Về Record Trong Java

**Record** là một tính năng mới được giới thiệu từ **JDK 16**. **Record** giúp đơn giản hóa việc tạo các lớp Java thông thường mà thường yêu cầu phải viết rất nhiều mã thừa như getter, setter, `equals()`, `hashCode()`, và `toString()`.

### Ví Dụ: Tạo Một Lớp Truyền Thống (Trước Khi Có Record)

Trước khi có **Record**, để tạo một lớp đơn giản với các thuộc tính như **name** và **age**, chúng ta cần phải viết nhiều mã lặp lại:

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

### Sử Dụng Record Để Tạo Lớp Đơn Giản

Với **Record**, bạn có thể đơn giản hóa điều này bằng cách chỉ định các thuộc tính trong một dòng, và tất cả các phương thức như `getter`, `toString()`, `equals()`, và `hashCode()` sẽ được tự động tạo.

```java
public record Person(String name, int age) {
}
```

Với dòng mã đơn giản này, bạn đã tạo được lớp **Person** với các phương thức như `toString()`, `equals()`, và `hashCode()` được Spring tự động cung cấp.

## 3. Tạo Nhiều Spring Beans

### Bước 1: Thêm Bean Mới - `age` (kiểu `int`)

Chúng ta sẽ bắt đầu bằng việc thêm một **bean** mới đại diện cho tuổi (**age**) vào **HelloWorldConfiguration**. Mã này sẽ quản lý một giá trị nguyên đơn giản.

```java
@Configuration
public class HelloWorldConfiguration {

    @Bean
    public String name() {
        return "Hello, Spring!";
    }

    @Bean
    public int age() {
        return 15; // Quản lý tuổi bởi Spring
    }
}
```

### Bước 2: Lấy Bean `age` Từ Spring Context

Trong lớp **App02HelloWorldSpring**, chúng ta sẽ lấy và in giá trị của **age**:

```java
public class App02HelloWorldSpring {
    public static void main(String[] args) {
        var context = new AnnotationConfigApplicationContext(HelloWorldConfiguration.class);

        // Lấy và in bean 'name'
        String name = context.getBean("name", String.class);
        System.out.println(name);

        // Lấy và in bean 'age'
        int age = context.getBean("age", Integer.class);
        System.out.println(age); // In ra: 15
    }
}
```

Khi chạy chương trình, bạn sẽ thấy kết quả là:

```
Hello, Spring!
15
```

### Bước 3: Tạo Custom Class `Person` Sử Dụng Record

Chúng ta sẽ tạo một **custom class** gọi là **Person** bằng cách sử dụng **Record**, một tính năng mới của JDK 16 giúp loại bỏ sự phức tạp khi tạo getter, setter, và constructor.

```java
public record Person(String name, int age) {
}
```

Với **Record**, chúng ta không cần phải viết thủ công các phương thức getter hay `toString()`. Những phương thức này được tự động tạo ra, giúp mã ngắn gọn hơn.

### Bước 4: Thêm Bean `Person` Trong Lớp Cấu Hình

Chúng ta sẽ tạo một bean **person** trong **HelloWorldConfiguration** để Spring quản lý đối tượng này.

```java
@Configuration
public class HelloWorldConfiguration {

    @Bean
    public String name() {
        return "Hello, Spring!";
    }

    @Bean
    public int age() {
        return 15;
    }

    @Bean
    public Person person() {
        return new Person("Ravi", 20); // Tạo Person mới với tên và tuổi
    }
}
```

### Bước 5: Lấy Bean `Person` Từ Spring Context

Trong **App02HelloWorldSpring**, chúng ta sẽ lấy và in thông tin của **Person**:

```java
public class App02HelloWorldSpring {
    public static void main(String[] args) {
        var context = new AnnotationConfigApplicationContext(HelloWorldConfiguration.class);

        // Lấy và in bean 'person'
        Person person = context.getBean("person", Person.class);
        System.out.println(person); // In ra: Person[name=Ravi, age=20]
    }
}
```

Kết quả khi chạy chương trình:

```
Person[name=Ravi, age=20]
```

### Bước 6: Tạo Và Quản Lý `Address` Bean

Chúng ta sẽ tạo một lớp **Address** sử dụng **Record** và thêm nó vào **Spring context**.

#### Tạo Lớp `Address`:

```java
public record Address(String firstLine, String city) {
}
```

#### Thêm Bean `Address` Trong Lớp Cấu Hình:

```java
@Bean
public Address address() {
    return new Address("Baker Street", "London");
}
```

#### Lấy Và In `Address`:

```java
public class App02HelloWorldSpring {
    public static void main(String[] args) {
        var context = new AnnotationConfigApplicationContext(HelloWorldConfiguration.class);

        // Lấy và in bean 'address'
        Address address = context.getBean("address", Address.class);
        System.out.println(address); // In ra: Address[firstLine=Baker Street, city=London]
    }
}
```

Kết quả:

```
Address[firstLine=Baker Street, city=London]
```

## 4. Kết Luận

Trong bước này, chúng ta đã:

- Tạo nhiều **Spring beans** từ các kiểu dữ liệu khác nhau như **String**, **int**, và **custom class** sử dụng **Record**.
- Giới thiệu tính năng **Record** của Java, giúp đơn giản hóa việc tạo các lớp Java thông thường.
- Hiểu cách Spring Framework quản lý các đối tượng phức tạp như **Person** và **Address**.

**Record** là một tính năng mạnh mẽ trong Java giúp loại bỏ sự thừa thãi khi tạo các lớp đơn giản, và kết hợp với Spring, chúng ta có thể dễ dàng quản lý các đối tượng trong ứng dụng. Trong bước tiếp theo, chúng ta sẽ khám phá thêm các tính năng của Spring để hiểu rõ hơn về cách nó quản lý và tiêm phụ thuộc cho các đối tượng phức tạp.
