# **Destructuring trong TypeScript 🧩**

**Destructuring** là một cú pháp mạnh mẽ trong JavaScript và TypeScript cho phép bạn truy xuất giá trị từ mảng hoặc đối tượng và gán chúng vào các biến một cách dễ dàng. Destructuring giúp làm mã ngắn gọn, dễ hiểu, và giảm thiểu việc phải viết mã lặp đi lặp lại.

Trong bài giảng này, chúng ta sẽ đi vào chi tiết từng phần về **Object Destructuring**, **Array Destructuring**, sự khác biệt giữa **Rest Operator** và **Spread Operator**, cùng với một số ví dụ nâng cao.

---

## **1. Object Destructuring 🔑**

**Object Destructuring** cho phép bạn trích xuất các thuộc tính từ đối tượng và gán chúng vào các biến với tên tương ứng.

#### **Cú pháp cơ bản**:

```typescript
const person = { name: "John", age: 30, city: "New York" };

// Destructuring đối tượng
const { name, age, city } = person;

console.log(name);  // John
console.log(age);   // 30
console.log(city);  // New York
```

#### **Gán tên khác cho các biến**:

Nếu bạn muốn sử dụng tên khác cho các biến, bạn có thể thay đổi tên của các thuộc tính trong khi destructuring bằng cách sử dụng dấu `:`.

```typescript
const person = { name: "John", age: 30, city: "New York" };

// Gán tên khác cho các biến
const { name: firstName, age: yearsOld, city: location } = person;

console.log(firstName); // John
console.log(yearsOld);  // 30
console.log(location);  // New York
```

#### **Cung cấp giá trị mặc định**:

Nếu thuộc tính không tồn tại trong đối tượng, bạn có thể cung cấp giá trị mặc định cho nó.

```typescript
const person = { name: "John", age: 30 };

// Destructuring với giá trị mặc định
const { name, age, city = "Unknown" } = person;

console.log(city); // Unknown
```

#### **Destructuring với kiểu dữ liệu tùy chỉnh (Type Aliases)**

Trong TypeScript, bạn có thể sử dụng **type aliases** để định nghĩa kiểu dữ liệu và kết hợp với **object destructuring**.

```typescript
type Person = {
  name: string;
  age: number;
  city?: string;  // city có thể là undefined
};

const person: Person = { name: "John", age: 30 };

// Destructuring với kiểu dữ liệu tùy chỉnh
const { name, age, city = "Unknown" }: Person = person;

console.log(city); // Unknown
```

---

## **2. Array Destructuring 📚**

**Array Destructuring** giúp bạn trích xuất các giá trị từ mảng và gán chúng vào các biến một cách dễ dàng.

#### **Cú pháp cơ bản**:

```typescript
const numbers = [1, 2, 3, 4, 5];

// Destructuring mảng
const [first, second, third] = numbers;

console.log(first);  // 1
console.log(second); // 2
console.log(third);  // 3
```

#### **Sử dụng Rest Operator trong mảng**:

**Rest Operator** (`...`) cho phép bạn thu thập phần còn lại của mảng sau khi đã destructuring các phần tử đầu tiên.

```typescript
const numbers = [1, 2, 3, 4, 5];

// Destructuring và lấy phần còn lại của mảng
const [first, second, ...rest] = numbers;

console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]
```

#### **Destructuring với các giá trị bỏ qua**:

Bạn có thể bỏ qua các phần tử trong mảng bằng cách sử dụng dấu phẩy mà không cần phải gán giá trị cho chúng.

```typescript
const numbers = [1, 2, 3, 4, 5];

// Bỏ qua phần tử thứ ba
const [first, , third] = numbers;

console.log(first);  // 1
console.log(third);  // 3
```

#### **Destructuring trong function arguments**:

Một ứng dụng phổ biến của **array destructuring** là khi truyền mảng vào hàm. Bạn có thể destructure trực tiếp trong tham số của hàm.

```typescript
function sum([a, b]: [number, number]) {
  return a + b;
}

const result = sum([5, 10]);
console.log(result); // 15
```

---

## **3. Rest vs Spread Operator ⚡**

**Rest Operator** và **Spread Operator** đều sử dụng cú pháp `...`, nhưng có sự khác biệt về mục đích sử dụng:

- **Rest Operator** được sử dụng để thu thập các phần tử còn lại của mảng hoặc đối tượng.
- **Spread Operator** được sử dụng để sao chép tất cả các phần tử của mảng hoặc đối tượng vào một đối tượng hoặc mảng mới.

#### **Rest Operator** trong Destructuring

**Rest Operator** dùng để thu thập phần còn lại của mảng hoặc đối tượng sau khi đã destructuring.

```typescript
const numbers = [1, 2, 3, 4, 5];

// Sử dụng Rest để lấy phần còn lại của mảng
const [first, second, ...rest] = numbers;

console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]
```

#### **Spread Operator** trong Destructuring

**Spread Operator** được sử dụng để sao chép các phần tử của mảng hoặc đối tượng vào một mảng hoặc đối tượng khác.

##### **Ví dụ với đối tượng**:

```typescript
const person = { name: "John", age: 30 };

// Spread vào đối tượng mới
const updatedPerson = { ...person, city: "New York" };

console.log(updatedPerson); // { name: 'John', age: 30, city: 'New York' }
```

##### **Ví dụ với mảng**:

```typescript
const numbers = [1, 2, 3];

// Spread trong mảng
const moreNumbers = [...numbers, 4, 5];

console.log(moreNumbers); // [1, 2, 3, 4, 5]
```

---

### **4. Ứng dụng thực tế của Destructuring 📌**

#### **4.1. Truy xuất thông tin từ API Response**

Khi bạn nhận được dữ liệu từ API, bạn có thể dùng destructuring để truy xuất các phần tử cần thiết từ đối tượng trả về.

```typescript
interface ApiResponse {
  status: string;
  data: any;
  error?: string;
}

const response: ApiResponse = {
  status: "success",
  data: { id: 1, name: "John" },
};

// Destructuring đối tượng trả về từ API
const { status, data } = response;
console.log(status); // success
console.log(data);   // { id: 1, name: "John" }
```

#### **4.2. Destructuring trong Function Arguments**

Khi một hàm nhận vào một đối tượng hoặc mảng phức tạp, bạn có thể sử dụng destructuring trực tiếp trong các tham số hàm để làm mã ngắn gọn và dễ hiểu.

```typescript
interface Person {
  name: string;
  age: number;
  city: string;
}

function greetPerson({ name, city }: Person) {
  console.log(`Hello, ${name} from ${city}!`);
}

const person = { name: "John", age: 30, city: "New York" };
greetPerson(person); // Hello, John from New York!
```

#### **4.3. Destructuring trong Nested Objects**

Khi đối tượng có cấu trúc lồng nhau, bạn cũng có thể sử dụng destructuring để trích xuất dữ liệu một cách dễ dàng.

```typescript
const person = { name: "John", address: { city: "New York", zip: "10001" } };

// Destructuring với nested objects
const { name, address: { city, zip } } = person;

console.log(name);  // John
console.log(city);  // New York
console.log(zip);   // 10001
```

---

### **5. Những điểm cần lưu ý**

- **Destructuring giúp giảm thiểu mã lặp lại**: Bạn không cần phải truy xuất từng thuộc tính của đối tượng một cách thủ công.
- **Đảm bảo tính tương thích**: Destructuring hoạt động tốt nhất với các đối tượng và mảng có cấu trúc cố định.
- **Destructuring có thể được sử dụng trong các kiểu dữ liệu tùy chỉnh** (Type Aliases, Interfaces).

---

### **Tài Liệu Tham Khảo 📚**

- [MDN Web Docs - Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [JavaScript Destructuring

 Tutorial](https://javascript.info/destructuring-assignment)
- [TypeScript Official Documentation](https://www.typescriptlang.org/docs/)

---

### **Tóm Tắt 📝**

- **Object Destructuring** giúp bạn truy xuất các thuộc tính của đối tượng và gán chúng vào biến.
- **Array Destructuring** giúp bạn truy xuất các phần tử từ mảng và gán chúng vào các biến.
- **Rest Operator** dùng để thu thập phần còn lại của đối tượng hoặc mảng.
- **Spread Operator** dùng để sao chép các phần tử từ một đối tượng hoặc mảng vào đối tượng hoặc mảng mới.

Hy vọng bài giảng chi tiết này sẽ giúp bạn hiểu rõ hơn về **Destructuring** và cách sử dụng nó trong TypeScript.