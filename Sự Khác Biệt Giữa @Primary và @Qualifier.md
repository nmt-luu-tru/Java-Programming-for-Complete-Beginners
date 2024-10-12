### Sự Khác Biệt Giữa @Primary và @Qualifier

Trong bước này, chúng ta sẽ đi sâu hơn vào sự khác biệt giữa **@Primary** và **@Qualifier**, và khi nào nên sử dụng từng chú thích này. Hãy cùng tìm hiểu thông qua một ví dụ về các thuật toán sắp xếp.

### Tình Huống Giả Định

Giả sử bạn có một **interface** tên là **SortingAlgorithm** và bạn đã triển khai các thuật toán sắp xếp như **QuickSort**, **BubbleSort**, và **RadixSort**. Bạn cũng có hai lớp **ComplexAlgorithm** và **AnotherComplexAlgorithm**, cả hai đều cần sử dụng **SortingAlgorithm**.

Chúng ta muốn sử dụng **@Autowired** để Spring tự động tiêm một **SortingAlgorithm** vào các lớp này, nhưng câu hỏi đặt ra là: chúng ta nên sử dụng **@Primary** hay **@Qualifier** để điều khiển quá trình tiêm (inject)?

### Khi Nào Nên Sử Dụng @Primary?

**@Primary** được sử dụng khi bạn có nhiều bean triển khai cùng một interface, và bạn muốn Spring ưu tiên một bean nhất định khi không có chỉ định cụ thể nào.

Ví dụ, nếu bạn có 5 thuật toán sắp xếp khác nhau và muốn Spring sử dụng **QuickSort** làm mặc định, bạn có thể thêm **@Primary** vào **QuickSort**:

```java
import org.springframework.stereotype.Component;
import org.springframework.context.annotation.Primary;

@Component
@Primary
public class QuickSort implements SortingAlgorithm {
    // Implementation of QuickSort
}
```

Trong trường hợp này, khi **ComplexAlgorithm** không chỉ định rõ thuật toán nào, Spring sẽ tự động tiêm **QuickSort** vì nó có **@Primary**.

### Khi Nào Nên Sử Dụng @Qualifier?

**@Qualifier** được sử dụng khi bạn muốn chỉ định rõ ràng một bean cụ thể sẽ được tiêm vào. Ví dụ, trong **AnotherComplexAlgorithm**, bạn muốn sử dụng **RadixSort** thay vì **QuickSort** hoặc **BubbleSort**, thì bạn sử dụng **@Qualifier**:

1. **Gắn @Qualifier cho RadixSort**:

```java
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.annotation.Qualifier;

@Component
@Qualifier("RadixSortQualifier")
public class RadixSort implements SortingAlgorithm {
    // Implementation of RadixSort
}
```

2. **Chỉ định @Qualifier trong AnotherComplexAlgorithm**:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class AnotherComplexAlgorithm {

    private final SortingAlgorithm sortingAlgorithm;

    @Autowired
    public AnotherComplexAlgorithm(@Qualifier("RadixSortQualifier") SortingAlgorithm sortingAlgorithm) {
        this.sortingAlgorithm = sortingAlgorithm;
    }

    // Use RadixSort in this algorithm
}
```

Trong trường hợp này, **AnotherComplexAlgorithm** sẽ luôn sử dụng **RadixSort**, bất kể có bao nhiêu thuật toán sắp xếp khác được tiêm vào Spring.

### @Primary và @Qualifier Trong Thực Tiễn

1. **ComplexAlgorithm** sử dụng **@Autowired** mà không chỉ định cụ thể thuật toán sắp xếp, vì vậy Spring sẽ tiêm thuật toán sắp xếp có **@Primary**:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class ComplexAlgorithm {

    private final SortingAlgorithm sortingAlgorithm;

    @Autowired
    public ComplexAlgorithm(SortingAlgorithm sortingAlgorithm) {
        this.sortingAlgorithm = sortingAlgorithm;
    }

    // Use the default sorting algorithm (e.g., QuickSort if marked as @Primary)
}
```

2. **AnotherComplexAlgorithm** sử dụng **@Qualifier** để chỉ định rõ ràng **RadixSort**, bất kể thuật toán nào có **@Primary**:

```java
@Component
public class AnotherComplexAlgorithm {

    private final SortingAlgorithm sortingAlgorithm;

    @Autowired
    public AnotherComplexAlgorithm(@Qualifier("RadixSortQualifier") SortingAlgorithm sortingAlgorithm) {
        this.sortingAlgorithm = sortingAlgorithm;
    }

    // Use RadixSort in this algorithm
}
```

### Lưu Ý Quan Trọng

1. **Ưu tiên của @Qualifier cao hơn @Primary**: Nếu một bean có **@Primary**, nhưng bạn chỉ định **@Qualifier** ở nơi khác, Spring sẽ tuân theo **@Qualifier** thay vì **@Primary**.

2. **Sử dụng tên bean làm @Qualifier**: Nếu bạn không sử dụng **@Qualifier** để chỉ định cụ thể, Spring có thể tự động sử dụng tên của bean (theo kiểu camel case) làm **qualifier**. Ví dụ, nếu bạn có một bean tên là **RadixSort**, Spring sẽ tự động đặt tên bean là **radixSort** và bạn có thể sử dụng:

```java
@Autowired
@Qualifier("radixSort")
private SortingAlgorithm sortingAlgorithm;
```

Điều này giúp bạn tránh phải khai báo thủ công **@Qualifier** cho từng bean.

### Kết Luận

- **Sử dụng @Primary** khi bạn muốn Spring tự động chọn một bean mặc định khi có nhiều lựa chọn.
- **Sử dụng @Qualifier** khi bạn cần kiểm soát rõ ràng và chỉ định cụ thể một bean sẽ được tiêm vào.
- Luôn nhớ rằng **@Qualifier** sẽ có ưu tiên cao hơn **@Primary**.

Hy vọng qua ví dụ về các thuật toán sắp xếp này, bạn đã hiểu rõ hơn về cách sử dụng **@Primary** và **@Qualifier** trong Spring. Hãy áp dụng và thử nghiệm để nắm vững cách Spring quản lý các bean và phụ thuộc trong ứng dụng của bạn!
