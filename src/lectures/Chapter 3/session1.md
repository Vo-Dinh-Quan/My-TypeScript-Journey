# **1. Type System Overview 🎯**

TypeScript là một ngôn ngữ lập trình dựa trên JavaScript, bổ sung một hệ thống kiểu mạnh mẽ để giúp bạn phát triển ứng dụng dễ dàng hơn, với ít lỗi hơn. Trong khi JavaScript là một ngôn ngữ không có hệ thống kiểu (dynamically typed), TypeScript cung cấp một lớp kiểm tra kiểu tĩnh (static typing), giúp kiểm tra lỗi khi biên dịch thay vì khi ứng dụng đang chạy. Điều này làm cho mã nguồn của bạn trở nên an toàn hơn và dễ bảo trì hơn, đặc biệt là trong các dự án lớn.

#### **Tại sao hệ thống kiểu lại quan trọng? 🤔**

- **Giảm thiểu lỗi**: Kiểm tra kiểu giúp phát hiện lỗi ngay từ khi biên dịch, tránh được các lỗi khó phát hiện trong quá trình chạy ứng dụng.
- **Tăng cường khả năng tự động hoàn thành (autocompletion)**: IDE (Integrated Development Environment) có thể cung cấp hỗ trợ mã tốt hơn với TypeScript vì hệ thống kiểu giúp nó hiểu được các kiểu dữ liệu cụ thể.
- **Dễ dàng bảo trì**: Khi dự án ngày càng lớn, việc có một hệ thống kiểu rõ ràng giúp các nhà phát triển mới tham gia dễ dàng hiểu được mã nguồn.

TypeScript không chỉ giới hạn ở việc kiểm tra các kiểu dữ liệu cơ bản mà còn hỗ trợ những cấu trúc dữ liệu phức tạp và các tính năng mạnh mẽ khác như generics, enums, và các loại đặc biệt.

---

## **Các Thành Phần Chính của Hệ Thống Kiểu trong TypeScript**

### 1. **Primitive Types (Kiểu Dữ Liệu Cơ Bản) 🛠️**
Các kiểu dữ liệu cơ bản trong TypeScript là những kiểu dữ liệu không thể chia nhỏ được nữa. Chúng bao gồm:
- `number`: Kiểu số (số nguyên và số thực).
- `string`: Kiểu chuỗi.
- `boolean`: Kiểu giá trị đúng/sai (true/false).
- `null`: Kiểu null đại diện cho một giá trị không tồn tại.
- `undefined`: Kiểu undefined đại diện cho một giá trị chưa được khởi tạo.
- `symbol`: Kiểu biểu tượng, thường dùng trong các trường hợp đặc biệt để tránh sự trùng lặp.
- `bigint`: Kiểu số lớn dùng để biểu diễn các số nguyên vượt quá giới hạn của `number`.

**Ví dụ**:

```typescript
let age: number = 25;
let name: string = "Alice";
let isActive: boolean = true;
let uniqueSymbol: symbol = Symbol("id");
let largeNumber: bigint = 1234567890123456789012345678901234567890n;
```

---

### 2. **Array Types (Kiểu Mảng) 🧮**

Mảng trong TypeScript có thể có kiểu dữ liệu đồng nhất (ví dụ, tất cả là số hoặc tất cả là chuỗi). Cú pháp khai báo mảng có thể sử dụng `[]` hoặc `Array<Type>`.

**Ví dụ**:

```typescript
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["apple", "banana", "cherry"];
```

Bạn cũng có thể sử dụng tuple (mảng có các phần tử có kiểu dữ liệu khác nhau ở các vị trí cố định).

```typescript
let tuple: [string, number] = ["Alice", 25];
```

---

### 3. **Object Types (Kiểu Đối Tượng) 📦**

Trong TypeScript, bạn có thể định nghĩa đối tượng với các thuộc tính có kiểu dữ liệu cụ thể. Để làm việc với đối tượng, bạn có thể sử dụng **Type Alias** hoặc **Interface**.

**Ví dụ**:

```typescript
type Person = {
  name: string;
  age: number;
};

let person: Person = {
  name: "Alice",
  age: 25,
};
```

Hoặc sử dụng **Interface**:

```typescript
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: "Alice",
  age: 25,
};
```

### 4. **Function Types (Kiểu Hàm) 🧑‍💻**

Trong TypeScript, bạn có thể định nghĩa kiểu cho tham số và giá trị trả về của một hàm.

**Ví dụ**:

```typescript
function add(x: number, y: number): number {
  return x + y;
}

let greet: (name: string) => string = function(name) {
  return `Hello, ${name}!`;
};
```

- `number` là kiểu dữ liệu cho tham số và kiểu trả về.
- `void` là kiểu cho những hàm không có giá trị trả về (hàm "void").

**Ví dụ về hàm không trả về giá trị**:

```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

### 5. **Generics (Kiểu Tổng Quát) 🌍**

Generics giúp bạn định nghĩa các kiểu dữ liệu tổng quát mà không cần biết trước kiểu dữ liệu cụ thể. Điều này giúp loại bỏ sự lặp lại trong mã và cung cấp tính linh hoạt.

**Ví dụ**:

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let result1 = identity(5);  // result1 có kiểu number
let result2 = identity("Hello");  // result2 có kiểu string
```

Generics có thể được áp dụng trong **Classes**, **Interfaces**, và **Functions**.

```typescript
class Box<T> {
  value: T;
  
  constructor(value: T) {
    this.value = value;
  }
}

const numberBox = new Box(123);
const stringBox = new Box("Hello");
```

---

### 6. **Enums (Liệt Kê) 🏷️**

**Enum** là một kiểu đặc biệt trong TypeScript, cho phép bạn định nghĩa một tập hợp các giá trị có tên, giúp mã dễ đọc và dễ bảo trì hơn.

**Ví dụ**:

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}

let move = Direction.Up;
console.log(move);  // "UP"
```

---

### 7. **Union Types (Kiểu Liên Hợp) 🏗️**

Union types cho phép một biến có thể là một trong nhiều kiểu dữ liệu khác nhau. Điều này giúp tăng tính linh hoạt mà vẫn giữ được tính an toàn kiểu.

**Ví dụ**:

```typescript
let value: string | number;
value = "Hello";
value = 42;  // Cả 2 kiểu đều hợp lệ
```

---

### 8. **Intersection Types (Kiểu Giao Thoa) 🔗**

Intersection types cho phép bạn kết hợp nhiều kiểu dữ liệu vào một kiểu duy nhất.

**Ví dụ**:

```typescript
interface Person {
  name: string;
  age: number;
}

interface Address {
  street: string;
  city: string;
}

type PersonWithAddress = Person & Address;

let personWithAddress: PersonWithAddress = {
  name: "Alice",
  age: 25,
  street: "123 Main St",
  city: "Wonderland",
};
```

---

### **Tóm Tắt 📝**

- **Primitive Types**: Sử dụng để định nghĩa các kiểu cơ bản như `number`, `string`, `boolean`, v.v.
- **Array Types**: Định nghĩa các kiểu mảng, hỗ trợ kiểu dữ liệu đồng nhất và tuple.
- **Object Types**: Định nghĩa kiểu đối tượng với các thuộc tính có kiểu dữ liệu cụ thể.
- **Function Types**: Định nghĩa kiểu cho hàm, bao gồm các tham số và kiểu trả về.
- **Generics**: Cung cấp tính linh hoạt cho các hàm, lớp và interface.
- **Enums**: Định nghĩa một tập hợp các giá trị có tên để mã dễ đọc hơn.
- **Union Types**: Cho phép một biến có thể nhận nhiều kiểu dữ liệu khác nhau.
- **Intersection Types**: Kết hợp các kiểu dữ liệu lại với nhau.

Hệ thống kiểu trong TypeScript không chỉ giúp phát hiện lỗi sớm mà còn giúp mã nguồn trở nên dễ đọc và dễ bảo trì. Nó cung cấp rất nhiều công cụ mạnh mẽ để làm việc với dữ liệu và cấu trúc phức tạp, từ đó giúp bạn phát triển các ứng dụng một cách dễ dàng và hiệu quả.

---

### **Tài Liệu Tham Khảo 📚**
- [TypeScript Handbook - Type System](https://www.typescriptlang.org/docs/handbook/2/types.html)
- [Generics in TypeScript](https://www.typescriptlang.org/docs/handbook/generics.html)
- [Enums in TypeScript](https://www.typescriptlang.org/docs/handbook/enums.html)
- [Utility Types in TypeScript](https://www.typescriptlang.org/docs/handbook/utility-types.html)