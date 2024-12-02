# **Truthy vs Falsy in TypeScript** ⚖️

Trong TypeScript (và JavaScript), **truthy** và **falsy** là những khái niệm liên quan đến cách mà các giá trị được đánh giá trong điều kiện (condition). Những giá trị **truthy** được coi là **đúng** khi chúng được kiểm tra trong một biểu thức điều kiện, trong khi những giá trị **falsy** được coi là **sai**.

Hãy cùng tìm hiểu chi tiết về **truthy** và **falsy**, cũng như các **use cases** phổ biến trong lập trình với TypeScript.

---

## **1. What is Truthy and Falsy? 🤔**

- **Truthy**: Là những giá trị được đánh giá là **đúng** khi sử dụng trong các biểu thức điều kiện (if, while, v.v). Tất cả các giá trị trong JavaScript và TypeScript đều được coi là truthy ngoại trừ các giá trị falsy.
  
- **Falsy**: Là những giá trị được đánh giá là **sai** trong biểu thức điều kiện. Chỉ có một số giá trị cụ thể được coi là falsy.

#### **Các giá trị Falsy trong JavaScript/TypeScript**:

- `false`: Chính nó.
- `0`: Số không.
- `-0`: Số âm không.
- `""` (Chuỗi rỗng): Một chuỗi không chứa ký tự nào.
- `null`: Một giá trị không xác định.
- `undefined`: Một giá trị chưa được gán.
- `NaN`: Không phải một số.

Tất cả những giá trị trên khi được sử dụng trong các biểu thức điều kiện sẽ được coi là **sai** (falsy).

#### **Các giá trị Truthy**:

- **Tất cả các giá trị khác ngoài những giá trị falsy** đều được coi là **truthy**. Ví dụ:
  - Số khác 0: `1`, `-1`, `3.14`, ...
  - Chuỗi không rỗng: `"Hello"`, `"0"`, `"false"`, ...
  - Các đối tượng: `{}`, `[]`, ...
  - Hàm: `function() {}`

---

## **2. How Truthy and Falsy Work in Conditions 🎯**

Trong TypeScript (và JavaScript), khi bạn kiểm tra một giá trị trong một biểu thức điều kiện, giá trị đó sẽ được **chuyển đổi thành kiểu boolean**. Các giá trị falsy sẽ được coi là `false`, và các giá trị truthy sẽ được coi là `true`.

#### **Ví dụ 1: Kiểm tra điều kiện với các giá trị Truthy và Falsy**

```typescript
let value: any;

// Falsy values
value = false;
if (!value) {
  console.log('Falsy: false');
}

value = 0;
if (!value) {
  console.log('Falsy: 0');
}

value = '';
if (!value) {
  console.log('Falsy: empty string');
}

value = null;
if (!value) {
  console.log('Falsy: null');
}

value = undefined;
if (!value) {
  console.log('Falsy: undefined');
}

value = NaN;
if (!value) {
  console.log('Falsy: NaN');
}

// Truthy values
value = 1;
if (value) {
  console.log('Truthy: 1');
}

value = 'Hello';
if (value) {
  console.log('Truthy: non-empty string');
}

value = {};
if (value) {
  console.log('Truthy: empty object');
}

value = [];
if (value) {
  console.log('Truthy: empty array');
}
```

**Kết quả**:
```
Falsy: false
Falsy: 0
Falsy: empty string
Falsy: null
Falsy: undefined
Falsy: NaN
Truthy: 1
Truthy: non-empty string
Truthy: empty object
Truthy: empty array
```

---

## **3. Use Cases: Khi nào sử dụng Truthy và Falsy? 💡**

#### **3.1. Kiểm tra dữ liệu đầu vào từ người dùng**

Khi lấy dữ liệu từ người dùng, bạn có thể muốn kiểm tra xem người dùng đã nhập gì hay chưa. Nếu họ để trống trường nhập liệu, đó là một giá trị **falsy**, và bạn có thể xử lý nó.

```typescript
let userInput = prompt("Enter your name:");

if (userInput) {
  console.log(`Hello, ${userInput}!`);
} else {
  console.log("You didn't enter your name.");
}
```

Trong ví dụ trên, nếu người dùng nhập vào một chuỗi rỗng (hoặc không nhập gì), `userInput` sẽ có giá trị falsy và câu thông báo "You didn't enter your name." sẽ được in ra.

#### **3.2. Kiểm tra nếu một đối tượng hoặc mảng có phần tử**

Khi làm việc với mảng hoặc đối tượng, bạn có thể kiểm tra xem chúng có dữ liệu hay không. Một mảng rỗng hoặc đối tượng trống sẽ được coi là falsy.

```typescript
let myArray = [];

if (myArray.length) {
  console.log("Array has elements.");
} else {
  console.log("Array is empty.");
}
```

Ở đây, mảng trống sẽ được coi là falsy vì `myArray.length` là `0`, và câu thông báo "Array is empty." sẽ được in ra.

#### **3.3. Kiểm tra các giá trị đầu vào không xác định**

Khi làm việc với các giá trị có thể là `null` hoặc `undefined`, bạn có thể dùng cách kiểm tra truthy/falsy để xác định xem giá trị đó có hợp lệ hay không.

```typescript
let data = fetchDataFromAPI(); // Giả sử hàm này trả về null hoặc một đối tượng.

if (data) {
  console.log("Data fetched successfully.");
} else {
  console.log("Data not found.");
}
```

Nếu `data` là `null` hoặc `undefined`, điều kiện `if (data)` sẽ trả về false, và câu thông báo "Data not found." sẽ được in ra.

---

### **4. Lưu Ý Quan Trọng 📝**

- **Lưu ý về chuỗi rỗng**: Một chuỗi rỗng `""` là falsy, nhưng một chuỗi chứa khoảng trắng `" "` hoặc một chuỗi bất kỳ khác sẽ là truthy.
- **Thận trọng với `0` và `NaN`**: Cả `0` và `NaN` đều là falsy, nhưng chúng có thể dễ gây nhầm lẫn vì trong các bài toán tính toán, chúng có thể có ý nghĩa khác.
- **Boolean Conversion**: Khi bạn cần chắc chắn rằng một giá trị được chuyển đổi thành `true` hoặc `false`, bạn có thể sử dụng `Boolean()` để ép kiểu:

```typescript
let value = 0;
let isTruthy = Boolean(value);  // false

let anotherValue = "Hello";
let isTruthy2 = Boolean(anotherValue);  // true
```

---

### **5. Tài Liệu Tham Khảo 📚**

- **MDN Web Docs - Falsy values**:  
  [https://developer.mozilla.org/en-US/docs/Glossary/Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  
- **JavaScript: Understanding the Weird Parts - Truthy/Falsy**:  
  [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)

---

### **Tóm Tắt**

- **Falsy** là các giá trị trong JavaScript/TypeScript mà khi kiểm tra trong điều kiện, chúng sẽ đánh giá là `false` (ví dụ: `false`, `0`, `""`, `null`, `undefined`, `NaN`).
- **Truthy** là mọi giá trị còn lại không phải falsy, nghĩa là chúng sẽ được coi là `true` trong các điều kiện.
- Sử dụng **truthy** và **falsy** để kiểm tra tính hợp lệ của dữ liệu đầu vào, mảng, đối tượng hoặc các giá trị không xác định.

Hy vọng bài giảng này giúp bạn hiểu rõ hơn về cách sử dụng **truthy** và **falsy** trong TypeScript để viết mã an toàn và hiệu quả hơn!