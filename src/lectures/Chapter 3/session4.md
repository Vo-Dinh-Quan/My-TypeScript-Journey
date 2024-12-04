# **Enum in TypeScript** 🎯

Trong TypeScript, **enum** là một kiểu dữ liệu đặc biệt cho phép bạn định nghĩa một tập hợp các hằng số có tên. Enums giúp mã của bạn dễ đọc, dễ hiểu và dễ bảo trì hơn khi làm việc với các giá trị có ý nghĩa đặc biệt hoặc thuộc một tập hợp cố định. Enum có thể là kiểu số (numeric) hoặc chuỗi (string), và chúng giúp mã nguồn của bạn trở nên rõ ràng hơn khi làm việc với các giá trị này.

---

### **1. Number Enum 🔢**

**Number enums** là kiểu enum mặc định trong TypeScript, trong đó các giá trị của các phần tử enum sẽ tự động nhận giá trị kiểu số (number), bắt đầu từ 0 hoặc một số nguyên được chỉ định.

**Cú pháp**:

```typescript
enum EnumName {
  Member1 = 0,
  Member2 = 1,
  Member3 = 2
}
```

**Ví dụ**:

```typescript
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}

console.log(Direction.Up);    // Output: 1
console.log(Direction.Down);  // Output: 2
console.log(Direction.Left);  // Output: 3
console.log(Direction.Right); // Output: 4
```

- Trong ví dụ trên, giá trị của `Direction.Up` là `1`. Các giá trị còn lại (`Direction.Down`, `Direction.Left`, `Direction.Right`) sẽ tự động tăng dần (2, 3, 4).
- Nếu bạn không gán giá trị cho `Up`, TypeScript sẽ mặc định gán giá trị `0` cho `Up` và các thành viên còn lại sẽ tăng dần từ 1.

**Lưu ý**:
- Nếu bạn chỉ định giá trị cho phần tử đầu tiên (như `Up = 1`), thì các phần tử sau sẽ tự động tăng dần từ giá trị đó.
- Nếu không có giá trị nào được gán, enum sẽ bắt đầu từ 0.

---

### **2. String Enum 📝**

**String enums** là một dạng enum trong đó các giá trị của các phần tử là chuỗi, không phải số. Dạng này hữu ích khi bạn cần làm việc với các giá trị chuỗi có ý nghĩa, ví dụ như tên trạng thái, danh mục, loại,...

**Cú pháp**:

```typescript
enum EnumName {
  Member1 = "Value1",
  Member2 = "Value2",
  Member3 = "Value3"
}
```

**Ví dụ**:

```typescript
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE"
}

console.log(Color.Red);    // Output: "RED"
console.log(Color.Green);  // Output: "GREEN"
console.log(Color.Blue);   // Output: "BLUE"
```

- **Lợi ích của String Enums**:
  - Thường được sử dụng khi bạn muốn sử dụng các chuỗi có ý nghĩa rõ ràng.
  - Dễ dàng trong việc debugging vì giá trị của các phần tử enum có thể đọc được trực tiếp từ chuỗi.

**Lưu ý**:
- Các phần tử enum phải có giá trị chuỗi cụ thể (không thể để trống hoặc tự động gán giá trị như trong number enums).
  
---

### **3. When to Use Enum ⚖️**

Bạn nên sử dụng **enum** khi bạn cần làm việc với một tập hợp các giá trị cố định, giúp mã của bạn dễ đọc, dễ bảo trì hơn và tránh các lỗi khi sử dụng các giá trị không hợp lệ.

**Khi nào sử dụng Enum?**:

- **Khi cần một tập hợp các giá trị cố định**: Ví dụ, ngày trong tuần, các loại trạng thái, các lựa chọn từ danh sách, các mã lỗi,...
- **Khi muốn mã rõ ràng hơn**: Sử dụng enum thay vì các giá trị số hoặc chuỗi thô giúp bạn tránh việc sử dụng các giá trị không hợp lệ.
- **Khi cần bảo vệ mã của bạn khỏi các thay đổi không mong muốn**: Enum sẽ giới hạn các giá trị có thể được sử dụng cho một thuộc tính hoặc tham số.

**Ví dụ**:

```typescript
enum Status {
  Pending = "PENDING",
  Approved = "APPROVED",
  Rejected = "REJECTED"
}

function updateStatus(status: Status): void {
  console.log(`The current status is ${status}`);
}

updateStatus(Status.Approved);  // Output: "The current status is APPROVED"
updateStatus(Status.Rejected);  // Output: "The current status is REJECTED"
```

**Lợi ích**:
- Giảm thiểu việc sử dụng các giá trị không hợp lệ như chuỗi hoặc số thô.
- Làm cho mã dễ bảo trì và dễ hiểu hơn.

---

### **4. Bonus: How Enum Compiles to JavaScript ⚡**

Khi TypeScript biên dịch mã của bạn xuống JavaScript, enum sẽ được chuyển đổi thành các đối tượng JavaScript. 

**Ví dụ**:

```typescript
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}

console.log(Direction.Up); // 1
console.log(Direction[2]); // "Down"
```

Biến `Direction` sau khi biên dịch TypeScript sang JavaScript sẽ trở thành một đối tượng như sau:

**JavaScript Output**:

```javascript
var Direction;
(function (Direction) {
    Direction[Direction["Up"] = 1] = "Up";
    Direction[Direction["Down"] = 2] = "Down";
    Direction[Direction["Left"] = 3] = "Left";
    Direction[Direction["Right"] = 4] = "Right";
})(Direction || (Direction = {}));

console.log(Direction.Up); // 1
console.log(Direction[2]); // "Down"
```

**Lưu ý**:
- TypeScript chuyển **Number enums** thành đối tượng bidirectional, nghĩa là bạn có thể truy cập giá trị của enum thông qua chỉ số (e.g., `Direction[2]` trả về "Down").
- **String enums** chỉ là các đối tượng đơn giản, không có tính bidirectional như **Number enums**.

---

### **Tóm Tắt 📝**

1. **Number Enum**: Enum mặc định trong TypeScript, các phần tử có giá trị tự động gán bắt đầu từ 0 hoặc giá trị đã chỉ định.
2. **String Enum**: Enum với giá trị là chuỗi, giúp mã dễ đọc và dễ debug hơn.
3. **Khi nào sử dụng Enum?**: Sử dụng khi bạn cần một tập hợp các giá trị cố định, giúp mã rõ ràng hơn và tránh các lỗi khi sử dụng giá trị không hợp lệ.
4. **Cách Enum Biên Dịch Sang JavaScript**: TypeScript biên dịch **Number enums** thành các đối tượng bidirectional, còn **String enums** là các đối tượng đơn giản.

---

### **Tài Liệu Tham Khảo 📚**

- [TypeScript Handbook - Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [TypeScript - Advanced Types](https://www.typescriptlang.org/docs/handbook/2/advanced-types.html#enums)

---

Hy vọng bài giảng giúp bạn hiểu rõ hơn về enum trong TypeScript và cách áp dụng nó trong dự án của mình!