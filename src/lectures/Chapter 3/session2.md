# **Type Alias vs Interface 🔥**

Cả **Type Alias** và **Interface** trong TypeScript đều cho phép bạn định nghĩa các kiểu dữ liệu cho các đối tượng, hàm, hoặc các loại dữ liệu khác. Tuy nhiên, chúng có sự khác biệt về cách sử dụng, khả năng mở rộng, và các tính năng hỗ trợ. Hãy cùng khám phá chi tiết về sự khác biệt giữa **Type Alias** và **Interface** trong TypeScript.

---

## **1. Type Alias là gì? 🏷️**

**Type Alias** là cách để gán một tên cho một kiểu dữ liệu phức tạp trong TypeScript. Type Alias có thể sử dụng với tất cả các kiểu dữ liệu trong TypeScript, bao gồm các kiểu cơ bản (primitive types), các kiểu dữ liệu kết hợp (union, intersection), và các kiểu phức tạp khác như **tuple** và **mapped types**.

**Cú pháp**:
```typescript
type TypeName = TypeDefinition;
```

**Ví dụ**:

```typescript
// Alias cho kiểu union
type StringOrNumber = string | number;
let value: StringOrNumber;

value = "Hello";  // Ok
value = 42;       // Ok
value = true;     // Error

// Alias cho kiểu tuple
type Point = [number, number];
let point: Point = [10, 20];

// Alias cho kiểu intersection
type Employee = { name: string } & { department: string };
let employee: Employee = { name: "Alice", department: "HR" };

```

### **Ưu điểm**:
- **Flexibility**: **Type Alias** có thể sử dụng với nhiều loại kiểu dữ liệu khác nhau, bao gồm **union**, **intersection**, **tuples**, **mapped types**, và **literal types**.
- **Kết hợp nhiều kiểu dữ liệu**: Bạn có thể dễ dàng kết hợp nhiều kiểu dữ liệu lại với nhau thông qua **union** và **intersection**.

---

## **2. Interface là gì? 🧩**

**Interface** là một cấu trúc trong TypeScript để định nghĩa các kiểu đối tượng. **Interface** giúp định nghĩa một bộ các thuộc tính và phương thức mà một đối tượng phải có. Bạn có thể sử dụng **Interface** để khai báo các kiểu dữ liệu phức tạp cho các đối tượng, và có thể mở rộng các **Interface** khác.

**Cú pháp**:
```typescript
interface InterfaceName {
  property: type;
  method(): returnType;
}
```

**Ví dụ**:

```typescript
interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  department: string;
}
```

### **Ưu điểm**:
- **Kế thừa (Extends)**: **Interface** có thể mở rộng và kế thừa các **Interface** khác thông qua từ khóa `extends`, điều này rất hữu ích khi bạn cần mở rộng một kiểu dữ liệu mà không phải thay đổi cấu trúc ban đầu.
- **Tính tương thích**: Các **Interface** có thể được **merge** lại với nhau (hợp nhất) nếu chúng có cùng tên, giúp việc mở rộng trở nên dễ dàng hơn.
- **Hỗ trợ Class**: **Interface** có thể được sử dụng với **class**. Một class có thể **implement** một hoặc nhiều **interface**.

---

## 3. So Sánh **Type Alias** và **Interface** ⚖️

| **Tính năng**                  | **Type Alias**                                  | **Interface**                                  |
|---------------------------------|-------------------------------------------------|------------------------------------------------|
| **Định nghĩa kiểu dữ liệu**     | Hỗ trợ tất cả các kiểu dữ liệu như `primitive`, `union`, `intersection`, `tuple`, `mapped types`,... | Thường được sử dụng để định nghĩa các kiểu đối tượng và có thể kế thừa các interface khác. |
| **Kế thừa (Extends)**           | Không hỗ trợ kế thừa trực tiếp, nhưng có thể kết hợp các kiểu với **intersection** (`&`) | Hỗ trợ kế thừa với từ khóa `extends`. |
| **Tính tương thích (Merging)**  | Không hỗ trợ **merging** | **Interface** có thể hợp nhất (merge) nhiều định nghĩa cùng tên. |
| **Sử dụng với Class**           | Không thể implement **Type Alias** trong class | **Interface** có thể được implement trong class. |
| **Định nghĩa hàm**              | Có thể định nghĩa kiểu cho hàm hoặc các cấu trúc phức tạp | Có thể định nghĩa kiểu cho hàm, tuy nhiên, không linh hoạt như **Type Alias**. |
| **Đặt tên**                     | Có thể sử dụng tên kiểu dữ liệu phức tạp như `union`, `intersection`, `tuple`,... | Thường được sử dụng cho các đối tượng và không linh hoạt như **Type Alias**. |

---

## **4. Union Type vs Intersection Type** 🔗

### **Union Type (Kiểu Liên Hợp)**

- **Type Alias** có thể được sử dụng để định nghĩa **union types**, cho phép biến có thể là một trong nhiều kiểu dữ liệu khác nhau.

**Ví dụ**:

```typescript
type StringOrNumber = string | number;
let value: StringOrNumber;

value = "Hello";  // Ok
value = 42;       // Ok
value = true;     // Error
```

- **Interface** không thể định nghĩa **union types** trực tiếp.

### **Intersection Type (Kiểu Giao Thoa)**

- **Type Alias** có thể được sử dụng để kết hợp nhiều kiểu dữ liệu lại với nhau bằng **intersection types**.

**Ví dụ**:

```typescript
type Person = { name: string; };
type Employee = Person & { department: string; };

let employee: Employee = {
  name: "Alice",
  department: "HR"
};
```

- **Interface** cũng có thể sử dụng **intersection types** để kết hợp nhiều interface lại với nhau.

**Ví dụ**:

```typescript
interface Person { name: string; }
interface Employee { department: string; }

interface EmployeeDetails extends Person, Employee {}

let employee: EmployeeDetails = {
  name: "Alice",
  department: "HR"
};
```

---

## **5. Nên Dùng `Interface` Hay `Type Alias`? 🤔**

### **Khi nào nên dùng Interface?**
- **Interface** thường được ưa chuộng khi bạn cần định nghĩa các đối tượng và muốn khả năng kế thừa, mở rộng hoặc kết hợp nhiều **interface** lại với nhau.
- Nếu bạn làm việc với **class** và cần **implement** một hoặc nhiều **interface**, thì **Interface** là lựa chọn tốt hơn.
- **Interface** dễ dàng **merge** với các **interface** cùng tên, giúp việc quản lý và mở rộng mã dễ dàng hơn.

### **Khi nào nên dùng Type Alias?**
- **Type Alias** được sử dụng khi bạn cần định nghĩa các kiểu phức tạp như **union types**, **intersection types**, **tuple types**, hoặc **literal types**.
- Khi bạn cần kết hợp nhiều kiểu dữ liệu lại với nhau (ví dụ: sử dụng **intersection types**), **Type Alias** là lựa chọn tối ưu.
- **Type Alias** cho phép bạn khai báo nhiều kiểu dữ liệu khác nhau trong một cấu trúc duy nhất.

---

## **6. Tóm Tắt 📝**

- **Interface**: Tốt cho việc định nghĩa các kiểu đối tượng, kế thừa và mở rộng các kiểu khác. Hỗ trợ làm việc với **class**.
- **Type Alias**: Thích hợp để kết hợp các kiểu dữ liệu phức tạp như **union types**, **intersection types**, **tuple**, và **literal types**. Hỗ trợ linh hoạt hơn trong việc định nghĩa các kiểu dữ liệu tổng quát.
- **Interface** và **Type Alias** có thể thay thế nhau trong nhiều trường hợp, nhưng mỗi cái có những điểm mạnh riêng tuỳ thuộc vào mục đích sử dụng.

---

### **Tài Liệu Tham Khảo 📚**

- [TypeScript Handbook - Type Aliases](https://www.typescriptlang.org/docs/handbook/2/objects.html#type-aliases)
- [TypeScript Handbook - Interfaces](https://www.typescriptlang.org/docs/handbook/2/objects.html#interfaces)
- [TypeScript Type System](https://www.typescriptlang.org/docs/handbook/2/types.html)