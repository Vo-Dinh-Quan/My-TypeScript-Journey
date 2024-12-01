### **Kiểu Dữ Liệu trong TypeScript**

TypeScript là một siêu ngôn ngữ của JavaScript, giúp người lập trình dễ dàng phát triển ứng dụng với kiểm tra kiểu dữ liệu (type checking). Điều này giúp tăng cường độ an toàn của mã và giảm thiểu lỗi khi chạy ứng dụng. Trong bài giảng này, chúng ta sẽ đi qua 4 khái niệm quan trọng về kiểu dữ liệu trong TypeScript:

1. **Explicit Types (Khai báo kiểu dữ liệu)**
2. **Infered Types (Kiểu dữ liệu suy luận)**
3. **Erased Types (Kiểu bị xóa sau khi biên dịch)**
4. **Downleveling (Hạ cấp mã)**

---

### **1. Explicit Types (Khai báo kiểu dữ liệu)** 📝

Khi bạn khai báo một biến trong TypeScript, bạn có thể chỉ định kiểu dữ liệu rõ ràng bằng cách sử dụng **explicit types**. Điều này giúp bạn kiểm soát chính xác kiểu dữ liệu mà biến có thể nhận, đảm bảo rằng không có lỗi kiểu dữ liệu trong quá trình biên dịch.

#### **Cách khai báo kiểu dữ liệu:**

Trong TypeScript, kiểu dữ liệu được khai báo bằng cách sử dụng dấu hai chấm (`:`) ngay sau tên biến và trước khi gán giá trị cho biến. Ví dụ:

```typescript
let count: number = 123;  // Kiểu number
let studentName: string = 'Alice';  // Kiểu string
let isActive: boolean = true;  // Kiểu boolean
const numberList: number[] = [1, 2, 3];  // Mảng kiểu number[]
```

#### **Một số kiểu dữ liệu cơ bản trong TypeScript:**
- **number**: Dùng cho số (bao gồm cả số nguyên và số thập phân).
- **string**: Dùng cho chuỗi ký tự.
- **boolean**: Dùng cho giá trị logic `true` hoặc `false`.
- **array**: Mảng có thể chứa nhiều phần tử của cùng một kiểu dữ liệu.
- **tuple**: Mảng có các phần tử với kiểu dữ liệu khác nhau.
- **any**: Kiểu dữ liệu linh hoạt nhất, có thể chứa bất kỳ giá trị nào.
- **void**: Được sử dụng khi hàm không trả về giá trị.
- **null và undefined**: Dùng để biểu thị giá trị không xác định.

#### **Lợi ích của Explicit Types:**
- **Rõ ràng và dễ bảo trì**: Khi bạn khai báo kiểu dữ liệu cho biến, mã của bạn sẽ dễ đọc và hiểu hơn. Các lập trình viên khác sẽ dễ dàng nắm bắt được mục đích và cách thức hoạt động của mã.
- **Giảm lỗi trong quá trình phát triển**: TypeScript sẽ giúp bạn phát hiện các lỗi liên quan đến kiểu dữ liệu ngay từ khi viết mã thay vì phải chờ mã chạy.

**Ví dụ:**
```typescript
let username: string = "Thuận";  // Kiểu string
let age: number = 30;  // Kiểu number
let isActive: boolean = true;  // Kiểu boolean
```

**Lưu ý**: Nếu bạn cố gắng gán giá trị sai kiểu, TypeScript sẽ báo lỗi:
```typescript
username = 123;  // Lỗi: Type 'number' is not assignable to type 'string'.
```

---

### **2. Infered Types (Kiểu dữ liệu suy luận)** 🤖

**Infered types** là một tính năng mạnh mẽ của TypeScript. Khi bạn không khai báo kiểu dữ liệu cho một biến, TypeScript sẽ tự động **suy luận** kiểu dữ liệu dựa trên giá trị mà bạn gán cho biến. Điều này giúp bạn tiết kiệm thời gian mà vẫn đảm bảo được tính an toàn kiểu dữ liệu.

#### **Cách TypeScript suy luận kiểu dữ liệu:**
TypeScript sẽ dựa vào giá trị gán cho biến để suy luận kiểu dữ liệu. Nếu bạn gán một giá trị kiểu `string`, TypeScript sẽ suy luận kiểu của biến là `string`. Nếu bạn gán giá trị kiểu `number`, kiểu sẽ được suy luận là `number`.

**Ví dụ:**
```typescript
let count = 123;  // TypeScript suy luận kiểu number
let studentName = 'Alice';  // TypeScript suy luận kiểu string
let isActive = true;  // TypeScript suy luận kiểu boolean
```

Ở đây, TypeScript sẽ tự động suy luận các kiểu dữ liệu cho các biến `count`, `studentName`, và `isActive` mà không cần phải khai báo kiểu rõ ràng. Khi gán giá trị `123` cho `count`, TypeScript sẽ biết kiểu của nó là `number`. Tương tự, với `studentName = 'Alice'`, kiểu của `studentName` sẽ là `string`, và `isActive = true` sẽ có kiểu `boolean`.

#### **Lợi ích của Infered Types:**
- **Tiết kiệm thời gian**: Bạn không cần phải khai báo kiểu dữ liệu nếu TypeScript có thể suy luận đúng từ giá trị gán.
- **Giảm mã lặp lại**: Trường hợp các giá trị rõ ràng, bạn không cần phải khai báo lại kiểu dữ liệu mà TypeScript có thể suy luận.

**Ví dụ về sử dụng `Infered Types` với mảng:**
```typescript
const numberList = [1, 2, 3];  // TypeScript suy luận kiểu number[]
const names = ['Alice', 'Bob'];  // TypeScript suy luận kiểu string[]
```

**Nhược điểm**:
- **Thiếu rõ ràng**: Nếu giá trị khởi tạo không rõ ràng, có thể dẫn đến việc suy luận kiểu sai.

---

### **3. Erased Types (Kiểu bị xóa sau khi biên dịch)** 🧹

**Erased types** là một khái niệm quan trọng trong TypeScript. Khi bạn biên dịch mã TypeScript thành JavaScript, **tất cả các kiểu dữ liệu** mà bạn khai báo trong TypeScript sẽ bị **xóa**. Điều này có nghĩa là các khai báo kiểu không tồn tại trong mã JavaScript cuối cùng, vì JavaScript không có cơ chế kiểm tra kiểu dữ liệu như TypeScript.

#### **Trước khi biên dịch (TypeScript):**
```typescript
const greeting: string = `hello ${1 + 1}`;
console.log(greeting);

(() => {
  interface Student {
    id: number;
    name: string;
    age: number;
  }
  const student: Student = {
    id: 1,
    name: 'Alice',
    age: 18,
  };
  const { id, name, age } = student;
  console.log(id, name, age);
})();
```

#### **Sau khi biên dịch thành JavaScript (với target="ES5"):**
```javascript
"use strict";
var greeting = "hello " + (1 + 1);
console.log(greeting);

(function () {
  var student = {
    id: 1,
    name: 'Alice',
    age: 18,
  };
  var id = student.id, name = student.name, age = student.age;
  console.log(id, name, age);
})();
```

#### **Lý do kiểu bị xóa**:
- TypeScript chỉ là một công cụ hỗ trợ phát triển, và kiểu dữ liệu trong TypeScript không có ý nghĩa trong môi trường JavaScript. Khi TypeScript biên dịch thành JavaScript, tất cả các **type annotations** sẽ bị xóa đi vì JavaScript không có khái niệm kiểu dữ liệu tĩnh.

---

### **4. Downleveling (Hạ cấp mã)** 🕹️

**Downleveling** là quá trình TypeScript biên dịch mã TypeScript xuống mã JavaScript sao cho mã đó có thể chạy trên các trình duyệt hoặc môi trường JavaScript cũ hơn. Điều này rất quan trọng khi bạn muốn mã của mình chạy trên các trình duyệt không hỗ trợ các tính năng mới của ECMAScript (ví dụ như các trình duyệt cũ).

#### **Lý do Downleveling**:
- **Tương thích ngược (Backward compatibility)**: TypeScript giúp bạn sử dụng các tính năng mới của ECMAScript nhưng vẫn có thể chạy trên các trình duyệt cũ hơn, thông qua quá trình biên dịch xuống JavaScript cũ hơn.

#### **Ví dụ về Downleveling với ES6 Class:**
TypeScript sử dụng **class**:
```typescript
class Student {
  constructor(public name: string, public age: number) {}
}
```

Biên dịch thành JavaScript với `target = "ES5"`:
```javascript
"use strict";
var Student = (function () {
  function Student(name, age) {
    this.name = name;
    this.age = age;
  }
  return Student;
})();
```

#### **Các tùy chọn target trong TypeScript:**
- **ES5**: Mã JavaScript sẽ được biên dịch về các tính năng của ECMAScript 5, giúp chạy trên các trình duyệt cũ.
- **ES6/ES2015**: Sử dụng các tính năng mới của ECMAScript 6 như arrow functions,

 classes, và template literals.
- **ESNext**: Biên dịch mã với các tính năng mới nhất của ECMAScript.

---

### **Tóm tắt**

- **Explicit Types** giúp bạn khai báo rõ ràng kiểu dữ liệu cho biến, giảm lỗi và tăng tính bảo trì.
- **Infered Types** cho phép TypeScript tự động suy luận kiểu dữ liệu, giúp mã ngắn gọn và dễ đọc.
- **Erased Types** là khái niệm rằng các kiểu dữ liệu trong TypeScript sẽ bị xóa khi biên dịch thành JavaScript.
- **Downleveling** đảm bảo mã TypeScript sẽ tương thích với các trình duyệt cũ hơn thông qua việc biên dịch về mã JavaScript cũ.

---

### **Liên kết tham khảo**

- [TypeScript Type Compatibility](https://basarat.gitbook.io/typescript/type-system/type-compatibility)
- [TypeScript Type Inference](https://basarat.gitbook.io/typescript/type-system/type-inference)
- [Explicit Types Documentation](https://www.typescriptlang.org/docs/handbook/2/basic-types.html#explicit-types)
- [Type Inference Documentation](https://www.typescriptlang.org/docs/handbook/type-inference.html)

---
