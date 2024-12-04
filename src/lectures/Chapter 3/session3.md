# **Điều Cần Lưu Ý Khi Làm Việc Với Function Trong TypeScript 📜**

---

## **1. Default Function Return Type 🔄**

Trong TypeScript, **default function return type** được xác định khi bạn không khai báo rõ kiểu trả về (return type) trong hàm. TypeScript sẽ tự động suy luận kiểu trả về từ giá trị được trả lại.

- Nếu hàm không trả về gì (chỉ thực hiện hành động mà không trả về giá trị gì), TypeScript sẽ gán kiểu trả về là `void`.
- Nếu hàm trả về một giá trị, TypeScript sẽ suy luận kiểu trả về dựa trên giá trị thực tế.

**Ví dụ**:

```typescript
// Hàm trả về kiểu number
function add(a: number, b: number) {
  return a + b;  // TypeScript tự động suy luận kiểu trả về là number
}

console.log(add(2, 3));  // Output: 5
```

**Tóm tắt**:
- Khi bạn không chỉ định kiểu trả về trong TypeScript, TypeScript sẽ tự động suy luận kiểu trả về của hàm.
- Đối với các hàm không trả về giá trị, kiểu trả về mặc định là `void`.

---

#### **2. Explicit Return Type 🖋️**

**Explicit return type** có nghĩa là bạn khai báo rõ ràng kiểu trả về cho hàm. Điều này giúp TypeScript hiểu rõ loại giá trị mà hàm sẽ trả về và đảm bảo rằng bạn không có lỗi khi trả về giá trị sai kiểu.

**Cú pháp**:

```typescript
function add(a: number, b: number): number {
  return a + b;  // Kiểu trả về là number
}
```

**Ví dụ**:

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

console.log(greet('Alice')); // Output: "Hello, Alice"
```

**Tại sao cần Explicit Return Type?**
- Giúp mã dễ bảo trì hơn.
- Phòng tránh các lỗi khi trả về giá trị sai kiểu.
- Cung cấp thông tin rõ ràng về kiểu trả về của hàm cho người khác khi làm việc với mã.

---

#### **3. Optional and Default Parameters 🎚️**

**Optional parameters** là các tham số có thể không được truyền vào khi gọi hàm, và khi đó TypeScript sẽ gán giá trị `undefined` cho tham số đó.

**Cú pháp**:
- Sử dụng dấu `?` để đánh dấu tham số là optional.
  
**Default parameters** là các tham số có giá trị mặc định nếu không có giá trị nào được truyền vào khi gọi hàm.

**Cú pháp**:
- Sử dụng dấu `=` để chỉ định giá trị mặc định cho tham số.

**Ví dụ**:

```typescript
// Optional parameter
function greet(name: string, age?: number): string {
  if (age) {
    return `${name} is ${age} years old.`;
  }
  return `${name} has no age information.`;
}

// Default parameter
function multiply(a: number, b: number = 2): number {
  return a * b;
}

console.log(greet('Alice'));                // "Alice has no age information."
console.log(greet('Bob', 30));             // "Bob is 30 years old."
console.log(multiply(5));                 // 10
console.log(multiply(5, 3));              // 15
```

**Tóm tắt**:
- Tham số **optional** cho phép tham số có thể bị bỏ qua.
- Tham số **default** cho phép bạn chỉ định giá trị mặc định cho tham số nếu không có giá trị nào được truyền vào.

---

#### **4. Function Overload 🧑‍💻**

**Function Overloading** là tính năng trong TypeScript cho phép bạn khai báo nhiều phiên bản của cùng một hàm, với các tham số và kiểu trả về khác nhau. Điều này cho phép một hàm có thể xử lý nhiều kiểu dữ liệu đầu vào khác nhau.

**Cú pháp**:
- Sử dụng các khai báo overload trước khi khai báo thân hàm.

**Ví dụ**:

```typescript
// Khai báo overload
function greet(name: string): string;
function greet(name: string, age: number): string;

// Thực thi hàm với logic cụ thể
function greet(name: string, age?: number): string {
  if (age) {
    return `${name} is ${age} years old.`;
  }
  return `Hello, ${name}!`;
}

console.log(greet('Alice'));             // Output: "Hello, Alice!"
console.log(greet('Bob', 30));          // Output: "Bob is 30 years old."
```

**Lưu ý**:
- Các khai báo overload cần phải có sự nhất quán giữa các tham số và kiểu trả về.
- TypeScript không cho phép thực thi logic trong các khai báo overload, chỉ có thể thực thi trong phần thân hàm.

---

#### **5. Destructuring Parameters 📦**

**Destructuring parameters** là một kỹ thuật trong JavaScript/TypeScript giúp bạn dễ dàng lấy giá trị từ các đối tượng hoặc mảng làm tham số của hàm.

**Cú pháp**:
- Dùng cú pháp destructuring để truyền tham số vào hàm.

**Ví dụ**:

```typescript
interface Person {
  name: string;
  age: number;
}

// Destructuring trong function parameters
function greet({ name, age }: Person): string {
  return `${name} is ${age} years old.`;
}

const person = { name: 'Alice', age: 30 };
console.log(greet(person));  // Output: "Alice is 30 years old."
```

- **Destructuring Array**:

```typescript
function sum([a, b]: [number, number]): number {
  return a + b;
}

console.log(sum([1, 2]));  // Output: 3
```

**Tóm tắt**:
- **Destructuring parameters** giúp bạn dễ dàng thao tác với các đối tượng và mảng khi truyền vào hàm.
- Thích hợp khi bạn cần làm việc với các đối tượng hoặc mảng phức tạp.

---

### **Bảng Type Compatibility 📊**

Dưới đây là bảng mô tả các kiểu dữ liệu trong TypeScript và đặc điểm của từng loại. Việc hiểu rõ bảng này sẽ giúp bạn làm việc với các kiểu dữ liệu trong TypeScript một cách hiệu quả hơn.

| **Type**              | **Description**                                           |
|-----------------------|-----------------------------------------------------------|
| `string`              | Kiểu chuỗi, dùng để lưu trữ các ký tự.                   |
| `number`              | Kiểu số, bao gồm cả số nguyên và số thập phân.            |
| `boolean`             | Kiểu boolean, chỉ có hai giá trị: `true` hoặc `false`.    |
| `null`                | Kiểu giá trị không khả dụng, không thể sử dụng.           |
| `undefined`           | Kiểu chưa được khởi tạo, biến chưa có giá trị.            |
| `any`                 | Kiểu linh hoạt, không kiểm tra kiểu dữ liệu.              |
| `unknown`             | Kiểu an toàn, không thể làm gì với biến `unknown` trừ khi bạn xác minh kiểu của nó. |
| `void`                | Kiểu hàm không trả về giá trị.                            |
| `never`               | Kiểu không bao giờ trả về giá trị, dùng cho các hàm throw error hoặc hàm infinite loop. |

---

### **Tóm Tắt 📝**

1. **Default function return type**: TypeScript tự động suy luận kiểu trả về nếu không được khai báo rõ ràng.
2. **Explicit return type**: Giúp bạn khai báo rõ ràng kiểu trả về của hàm, giúp mã dễ bảo trì và tránh lỗi.
3. **Optional and default parameters**: Bạn có thể sử dụng tham số tùy chọn (`?`) và tham số mặc định (`=`) trong TypeScript để dễ dàng xử lý các giá trị không xác định.
4. **Function Overload**: TypeScript hỗ trợ khai báo nhiều phiên bản của hàm với các tham số và kiểu trả về khác nhau.
5. **Destructuring parameters**: Kỹ thuật giúp bạn dễ dàng làm việc với đối tượng và mảng trong hàm.

---

### **Tài Liệu Tham Khảo 📚**

- [TypeScript Handbook - Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html)
- [TypeScript Handbook - Type Compatibility](https://www.typescriptlang.org/docs/handbook/2/type-compatibility.html)
- [TypeScript Handbook - Advanced Types](https://www.typescriptlang.org/docs/handbook/2/advanced-types.html)

--- 

Hy vọng bài giảng này sẽ giúp bạn nắm bắt được các lưu ý khi làm việc với functions trong TypeScript!