# **Variables: `const` and `let` in TypeScript** 📜

Trong TypeScript (cũng như JavaScript), **`const`** và **`let`** là hai cách khai báo biến phổ biến. Sự khác biệt chính giữa chúng là **`const`** dùng để khai báo những biến mà giá trị không thay đổi, trong khi **`let`** dùng khi giá trị của biến có thể thay đổi. Việc hiểu rõ khi nào sử dụng từng loại khai báo này sẽ giúp bạn viết mã rõ ràng, dễ hiểu và dễ bảo trì hơn. Hãy cùng tìm hiểu chi tiết về **`const`** và **`let`**, cũng như một số quy tắc về việc đặt tên biến.

---

## **1. When to use `const` 🛑**

**`const`** là từ khóa dùng để khai báo **biến hằng** — tức là những biến có giá trị **không thể thay đổi** trong suốt quá trình chạy chương trình. Việc sử dụng `const` là rất quan trọng trong các tình huống khi bạn muốn đảm bảo rằng một giá trị không bị thay đổi ngoài ý muốn. Mặc dù vậy, **`const`** không có nghĩa là bạn không thể thay đổi giá trị của đối tượng hoặc mảng, mà chỉ nghĩa là bạn không thể thay đổi **tham chiếu** của đối tượng hoặc mảng đó.

#### **Khi nào nên dùng `const`**:
- **Giá trị không thay đổi**: Khi bạn biết rằng giá trị của biến sẽ không thay đổi trong suốt vòng đời của chương trình.
- **Hằng số**: Các giá trị mà không bao giờ thay đổi, ví dụ như `PI`, `MAX_LENGTH`, `API_URL`.
- **Tham chiếu không thay đổi**: Khi bạn muốn đảm bảo rằng đối tượng hoặc mảng không được thay đổi tham chiếu trong suốt quá trình thực thi.

#### **Ví dụ với `const`:**

```typescript
const pi = 3.14159;  // Hằng số Pi, không thể thay đổi

// Không thể thay đổi giá trị của biến pi
// pi = 3.14;  // Lỗi: Assignment to constant variable.
```

**Lưu ý**: Nếu bạn khai báo một đối tượng hoặc mảng bằng `const`, thì bạn không thể thay đổi **tham chiếu** của nó, nhưng bạn vẫn có thể thay đổi **nội dung** bên trong.

```typescript
const arr = [1, 2, 3];
arr.push(4);  // Được phép, thay đổi nội dung của mảng
console.log(arr);  // [1, 2, 3, 4]

// Nhưng bạn không thể thay đổi tham chiếu của mảng:
// arr = [5, 6, 7];  // Lỗi: Assignment to constant variable.
```

#### **Tóm lại**:
- **Dùng `const`** khi bạn biết biến không thay đổi giá trị sau khi khởi tạo, và khi bạn muốn đảm bảo rằng tham chiếu của đối tượng/ mảng không bị thay đổi.

---

## **2. When to use `let` 🖊️**

**`let`** là từ khóa dùng để khai báo các biến có thể **thay đổi giá trị** trong suốt quá trình chạy chương trình. `let` có phạm vi **block-level**, nghĩa là nó chỉ tồn tại trong phạm vi của khối mã mà nó được khai báo.

#### **Khi nào nên dùng `let`**:
- **Giá trị thay đổi**: Khi bạn cần một biến có thể thay đổi giá trị trong suốt vòng đời của chương trình.
- **Sử dụng trong vòng lặp**: Khi bạn cần cập nhật giá trị của một biến trong vòng lặp.
- **Khi giá trị biến thay đổi theo điều kiện hoặc người dùng nhập**: Ví dụ như lưu trữ số lượng, điểm số, hay các giá trị nhập từ người dùng.

#### **Ví dụ với `let`:**

```typescript
let counter = 0;
counter = counter + 1;  // Được phép, thay đổi giá trị của counter
console.log(counter);  // 1

let message = "Hello";
message = "World";  // Được phép thay đổi giá trị
console.log(message);  // World
```

**Lưu ý**: Với `let`, bạn có thể thay đổi giá trị của biến trong quá trình thực thi. 

#### **Tóm lại**:
- **Dùng `let`** khi bạn chắc chắn rằng giá trị của biến sẽ thay đổi trong suốt quá trình thực thi.

---

## **3. Naming Convention 📐**

Quy tắc về đặt tên biến rất quan trọng trong lập trình, giúp mã dễ đọc và dễ bảo trì. TypeScript (cũng như JavaScript) khuyến khích sử dụng các quy tắc đặt tên nhất quán để đảm bảo mã nguồn rõ ràng và có thể hiểu được ngay lập tức.

#### **Quy ước đặt tên trong TypeScript**:
1. **CamelCase**:
   - Dùng cho các **biến**, **hàm**, và **thuộc tính đối tượng**. Tên biến bắt đầu bằng chữ thường và các từ tiếp theo viết hoa chữ cái đầu. Ví dụ: `userName`, `getUserInfo`, `isAvailable`.
   
2. **PascalCase**:
   - Dùng cho **tên lớp** và **kiểu dữ liệu**. Tên lớp bắt đầu bằng chữ cái viết hoa và các từ sau viết hoa chữ cái đầu. Ví dụ: `Person`, `EmployeeData`.

3. **UPPERCASE**:
   - Dùng cho **hằng số** hoặc các giá trị không thay đổi. Tên hằng số thường viết tất cả chữ in hoa, nếu có nhiều từ thì dùng dấu gạch dưới giữa các từ. Ví dụ: `MAX_LENGTH`, `PI`, `API_KEY`.

#### **Ví dụ về naming convention**:

```typescript
const MAX_AGE = 100;  // Hằng số, sử dụng ALL_UPPERCASE
let userName = "JohnDoe";  // Biến, sử dụng camelCase
let userAge = 30;  // Biến, sử dụng camelCase

class Employee {  // Lớp, sử dụng PascalCase
  private employeeId: number;
  
  constructor(employeeId: number) {
    this.employeeId = employeeId;
  }
}
```

#### **Các lưu ý khi đặt tên biến**:
- **Đặt tên rõ ràng, dễ hiểu**: Nên đặt tên sao cho người khác có thể dễ dàng hiểu được mục đích của biến mà không cần phải xem xét nhiều.
- **Tránh các tên không rõ ràng**: Ví dụ như `temp`, `data`, `item` nếu không rõ ràng trong ngữ cảnh sử dụng.
- **Sử dụng các từ khóa mô tả**: Các tên như `isAvailable`, `userEmail`, `productList` giúp người đọc hiểu ngay mục đích của biến.

---

## **4. Các Lý Do Cần Sử Dụng `const` và `let` Đúng Cách**

1. **Tăng cường tính ổn định của mã**: Việc sử dụng `const` giúp đảm bảo rằng các giá trị không thay đổi ngoài ý muốn, làm giảm khả năng xảy ra lỗi trong mã nguồn. Điều này rất quan trọng trong các ứng dụng phức tạp.
  
2. **Giảm thiểu lỗi không đáng có**: Sử dụng `let` và `const` một cách hợp lý giúp dễ dàng phát hiện lỗi và tránh những tình huống như vô tình thay đổi giá trị của biến mà không biết.

3. **Dễ bảo trì mã**: Các quy ước đặt tên rõ ràng giúp bạn dễ dàng theo dõi, duy trì mã của mình và chia sẻ với những người khác trong nhóm phát triển.

---

### **📚 Tài Liệu Tham Khảo**

1. **MDN Web Docs - JavaScript Variables**:  
   [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)  
   [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

2. **TypeScript Handbook**:
   [https://www.typescriptlang.org/docs/](https://www.typescriptlang.org/docs/)

3. **Code with the Best Practices**:
   - [https://basarat.gitbook.io/typescript/](https://basarat.gitbook.io/typescript/)
   - [https://refactoring.guru/](https://refactoring.guru/)

---

### **📝 Tóm Tắt**

- **`const`**: Sử dụng khi giá trị không thay đổi.
- **`let`**: Sử dụng khi giá trị có thể thay đổi.
- **Naming convention**:
  - **camelCase** cho biến, hàm và thuộc tính.
  - **PascalCase** cho lớp và kiểu dữ liệu.
  - **UPPERCASE** cho hằng số.

Việc chọn lựa **`const`** hay **`let`** phù hợp sẽ giúp mã của bạn trở nên rõ ràng và an toàn hơn, đồng thời giúp bạn tránh được các lỗi không mong muốn trong quá trình phát triển ứng dụng.