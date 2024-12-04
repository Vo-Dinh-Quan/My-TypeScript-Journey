### **Generics trong TypeScript** 🛠️

**Generics** là một tính năng mạnh mẽ của TypeScript giúp bạn viết các hàm, lớp, hoặc giao diện có thể làm việc với nhiều loại dữ liệu khác nhau mà không cần phải xác định cụ thể kiểu dữ liệu trước. Generics giúp bạn viết mã tái sử dụng được, vừa an toàn về kiểu dữ liệu mà lại linh hoạt.

Generics cho phép bạn tạo ra một kiểu dữ liệu hoặc hàm "mở rộng" để chấp nhận nhiều kiểu khác nhau, mà không làm mất đi tính chính xác về kiểu của dữ liệu mà bạn đang làm việc với.

---

### **1. Generics là gì? 🤔**

Generics cho phép bạn chỉ định một "chỗ trống" trong kiểu dữ liệu mà bạn có thể "điền vào" sau này. Tính năng này giúp đảm bảo rằng các kiểu dữ liệu trong chương trình của bạn có thể được xác định một cách chính xác và linh hoạt.

**Cú pháp cơ bản**:

```typescript
function identity<T>(value: T): T {
  return value;
}
```

Trong ví dụ trên, `T` là một **type parameter** (tham số kiểu), nó có thể là bất kỳ kiểu nào mà bạn chỉ định khi gọi hàm. Khi gọi hàm, TypeScript sẽ tự động suy luận kiểu của tham số từ đối số bạn truyền vào, hoặc bạn có thể chỉ định rõ kiểu tham số khi gọi hàm.

**Ví dụ sử dụng hàm generic**:

```typescript
function identity<T>(value: T): T {
  return value;
}

let number = identity(42);  // number có kiểu 'number'
let text = identity("Hello, world!");  // text có kiểu 'string'
```

### **2. Generics với Array 📚**

Generics rất hữu ích khi làm việc với các kiểu mảng hoặc danh sách. Bạn có thể sử dụng chúng để tạo các hàm hoặc lớp có thể xử lý bất kỳ kiểu dữ liệu nào trong mảng, mà vẫn giữ nguyên tính chính xác của kiểu.

**Ví dụ**:

```typescript
function logArray<T>(arr: T[]): void {
  arr.forEach(item => console.log(item));
}

logArray([1, 2, 3]); // Array of numbers
logArray(["apple", "banana", "cherry"]); // Array of strings
```

Ở đây, `T[]` có thể là một mảng chứa bất kỳ kiểu dữ liệu nào.

### **3. Generics với Interface 🔗**

Generics cũng có thể được sử dụng trong các interface hoặc loại đối tượng, giúp bạn tạo ra các kiểu dữ liệu linh hoạt mà vẫn đảm bảo tính an toàn về kiểu.

**Ví dụ**:

```typescript
interface Box<T> {
  value: T;
}

let box1: Box<number> = { value: 42 };
let box2: Box<string> = { value: "Hello" };
```

Ở đây, `Box<T>` là một interface có thể chấp nhận bất kỳ kiểu dữ liệu nào cho `value`. Bạn có thể xác định kiểu dữ liệu của `value` khi tạo các đối tượng.

---

### **4. `keyof` Operator 🧑‍💻**

**`keyof`** là một operator trong TypeScript cho phép bạn lấy ra tập hợp tất cả các khóa (keys) của một kiểu đối tượng. Nó trả về một type đại diện cho các tên thuộc tính của đối tượng, giúp bạn làm việc linh hoạt với các đối tượng và các giá trị của chúng.

**Cú pháp**:

```typescript
type Keys = keyof T;
```

**Ví dụ**:

```typescript
interface Person {
  name: string;
  age: number;
}

type PersonKeys = keyof Person;  // "name" | "age"
```

Ở ví dụ trên, `PersonKeys` sẽ có kiểu `"name" | "age"`, đại diện cho các khóa của `Person`.

**Sử dụng `keyof` trong hàm**:

```typescript
function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person = { name: "Alice", age: 25 };
let name = getValue(person, "name");  // string
let age = getValue(person, "age");    // number
```

Ở đây, `K extends keyof T` đảm bảo rằng `key` chỉ có thể là một trong những khóa hợp lệ của đối tượng `T`.

---

### **5. `typeof` Operator 🛠️**

**`typeof`** là một operator trong TypeScript giúp bạn lấy kiểu dữ liệu của một đối tượng hoặc biến. Trong TypeScript, bạn có thể sử dụng `typeof` để "truy vấn" kiểu dữ liệu của một đối tượng hoặc biến tại thời điểm biên dịch.

**Cú pháp**:

```typescript
let x = "Hello";
let y: typeof x;  // y có kiểu 'string'
```

**Ví dụ**:

```typescript
let obj = { name: "Alice", age: 25 };

type ObjType = typeof obj;  // { name: string; age: number; }
```

Trong ví dụ trên, `ObjType` sẽ có kiểu `{ name: string; age: number; }`, và bạn có thể sử dụng kiểu này trong các hàm hoặc các đối tượng khác.

### **6. Mapped Types 🔁**

**Mapped types** là một loại type đặc biệt trong TypeScript cho phép bạn tạo ra các kiểu dữ liệu mới từ một kiểu dữ liệu đã có. Bạn có thể sử dụng chúng để tạo ra các kiểu đối tượng với các thuộc tính mới dựa trên một kiểu đã có.

**Cú pháp**:

```typescript
type MappedType<T> = {
  [P in keyof T]: T[P];
}
```

**Ví dụ**:

```typescript
interface Person {
  name: string;
  age: number;
}

type ReadOnlyPerson = {
  readonly [P in keyof Person]: Person[P];
};

let person: ReadOnlyPerson = { name: "Alice", age: 25 };
person.name = "Bob";  // Error: cannot assign to 'name' because it is a read-only property
```

Ở đây, `ReadOnlyPerson` là một mapped type, trong đó tất cả các thuộc tính của `Person` trở thành **readonly**.

### **7. Generics và Mapped Types 🛠️**

Generics cũng có thể được kết hợp với mapped types để tạo ra các kiểu dữ liệu linh hoạt hơn.

**Ví dụ**:

```typescript
function makeReadonly<T>(obj: T): { readonly [K in keyof T]: T[K] } {
  let result = {} as { readonly [K in keyof T]: T[K] };
  for (let key in obj) {
    result[key] = obj[key];
  }
  return result;
}

const person = { name: "Alice", age: 25 };
const readonlyPerson = makeReadonly(person);

readonlyPerson.name = "Bob";  // Error: cannot assign to 'name' because it is a read-only property
```

Ở đây, hàm `makeReadonly` nhận vào một đối tượng và trả về một đối tượng mới, trong đó tất cả các thuộc tính trở thành **readonly**.

---

### **Tóm Tắt 📝**

1. **Generics** giúp bạn viết các hàm và lớp linh hoạt mà vẫn đảm bảo tính an toàn về kiểu.
2. **`keyof`** operator lấy ra tất cả các khóa (keys) của một đối tượng.
3. **`typeof`** operator giúp bạn truy vấn kiểu dữ liệu của một đối tượng hoặc biến.
4. **Mapped Types** cho phép bạn tạo kiểu dữ liệu mới từ kiểu dữ liệu đã có bằng cách áp dụng các phép biến đổi (ví dụ: `readonly`, `optional`).

---

### **Tài Liệu Tham Khảo 📚**

- [TypeScript Handbook - Generics](https://www.typescriptlang.org/docs/handbook/generics.html)
- [TypeScript Handbook - keyof](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html)
- [TypeScript Handbook - typeof](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html)
- [TypeScript Handbook - Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)

---

Hy vọng bài giảng này giúp bạn hiểu rõ hơn về **Generics**, **keyof**, **typeof**, và **Mapped Types** trong TypeScript!