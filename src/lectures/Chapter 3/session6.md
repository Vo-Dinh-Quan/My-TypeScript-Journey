Dưới đây là bài giảng chi tiết về các **Utility Types** trong TypeScript.

---

# **Utility Types trong TypeScript 🛠️**

TypeScript cung cấp một loạt các **Utility Types** để giúp bạn làm việc với các kiểu dữ liệu dễ dàng hơn và linh hoạt hơn. Những utility types này đặc biệt hữu ích khi bạn muốn thay đổi hoặc thao tác với kiểu dữ liệu mà không cần phải khai báo lại từ đầu.

## **Agenda** 📚
1. **Partial** – Đặt tất cả các thuộc tính của Type thành optional
2. **Required** – Đặt tất cả các thuộc tính của Type thành required
3. **Readonly** – Đặt tất cả các thuộc tính của Type thành readonly
4. **Record<Keys, Type>** – Một kiểu có khóa từ Keys và giá trị của kiểu Type
5. **Pick<Type, Keys>** – Chọn một tập hợp Keys từ Type
6. **Omit<Type, Keys>** – Loại bỏ một tập hợp Keys từ Type
7. **ReturnType** – Kiểu trả về của một hàm

---

## **1. Partial** – Đặt tất cả các thuộc tính của Type thành optional 🔄

**Partial** là một utility type cho phép bạn biến tất cả các thuộc tính của một kiểu dữ liệu thành **optional**.

### **Cú pháp**:
```typescript
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

### **Ví dụ**:
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

// Sử dụng Partial để làm tất cả các thuộc tính trở thành optional
type PartialPerson = Partial<Person>;

const person1: PartialPerson = {
  name: 'Alice',
}; // hợp lệ vì tất cả các thuộc tính đều là optional
```

### **Ứng dụng**:
- Sử dụng khi bạn muốn tạo ra một đối tượng mà không cần phải cung cấp tất cả các thuộc tính ban đầu.

---

## **2. Required** – Đặt tất cả các thuộc tính của Type thành required 🔒

**Required** làm tất cả các thuộc tính của kiểu dữ liệu thành **required**, ngược lại với **Partial**.

### **Cú pháp**:
```typescript
type Required<T> = {
  [P in keyof T]-?: T[P];
};
```

### **Ví dụ**:
```typescript
interface Person {
  name: string;
  age?: number;
}

// Sử dụng Required để làm tất cả các thuộc tính trở thành required
type RequiredPerson = Required<Person>;

const person2: RequiredPerson = {
  name: 'Bob',
  age: 30, // bắt buộc phải có age vì nó đã trở thành required
};
```

### **Ứng dụng**:
- Dùng khi bạn muốn đảm bảo rằng tất cả các thuộc tính của kiểu dữ liệu phải được khai báo khi khởi tạo.

---

## **3. Readonly** – Đặt tất cả các thuộc tính của Type thành readonly 🔐

**Readonly** giúp tất cả các thuộc tính của kiểu dữ liệu trở thành **readonly**, nghĩa là bạn không thể thay đổi giá trị của chúng sau khi đã khởi tạo.

### **Cú pháp**:
```typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

### **Ví dụ**:
```typescript
interface Person {
  name: string;
  age: number;
}

// Sử dụng Readonly để biến tất cả các thuộc tính thành readonly
type ReadonlyPerson = Readonly<Person>;

const person3: ReadonlyPerson = {
  name: 'Charlie',
  age: 35,
};

// person3.age = 36; // Error: Cannot assign to 'age' because it is a read-only property.
```

### **Ứng dụng**:
- Dùng khi bạn muốn bảo vệ dữ liệu khỏi bị thay đổi trong quá trình thực thi chương trình.

---

## **4. Record<Keys, Type>** – Một kiểu có khóa từ Keys và giá trị của kiểu Type 🗂️

**Record** là một utility type rất mạnh mẽ, cho phép bạn tạo ra một kiểu mới mà có các **key** từ một tập hợp **Keys** và giá trị có kiểu **Type**.

### **Cú pháp**:
```typescript
type Record<K extends keyof any, T> = {
  [P in K]: T;
};
```

### **Ví dụ**:
```typescript
// Tạo một đối tượng mà keys là một chuỗi và giá trị là một số
type NumberRecord = Record<string, number>;

const scores: NumberRecord = {
  math: 90,
  science: 85,
  history: 88,
};
```

### **Ứng dụng**:
- Sử dụng khi bạn cần một đối tượng có các key động và giá trị là kiểu dữ liệu cụ thể.

---

## **5. Pick<Type, Keys>** – Chọn một tập hợp Keys từ Type ✅

**Pick** cho phép bạn **chọn** một tập hợp các thuộc tính (keys) từ kiểu dữ liệu **Type** ban đầu.

### **Cú pháp**:
```typescript
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```

### **Ví dụ**:
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

// Sử dụng Pick để chỉ lấy một số thuộc tính
type PersonNameAndAge = Pick<Person, 'name' | 'age'>;

const person4: PersonNameAndAge = {
  name: 'David',
  age: 40,
};
```

### **Ứng dụng**:
- Sử dụng khi bạn chỉ muốn lấy một phần nhỏ thuộc tính từ một kiểu dữ liệu lớn hơn.

---

## **6. Omit<Type, Keys>** – Loại bỏ một tập hợp Keys từ Type ❌

**Omit** ngược lại với **Pick**. Nó cho phép bạn **loại bỏ** một tập hợp thuộc tính từ kiểu dữ liệu **Type** ban đầu.

### **Cú pháp**:
```typescript
type Omit<T, K extends keyof T> = {
  [P in Exclude<keyof T, K>]: T[P];
};
```

### **Ví dụ**:
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

// Sử dụng Omit để loại bỏ thuộc tính 'address'
type PersonWithoutAddress = Omit<Person, 'address'>;

const person5: PersonWithoutAddress = {
  name: 'Eve',
  age: 25,
};
```

### **Ứng dụng**:
- Dùng khi bạn muốn loại bỏ một số thuộc tính không cần thiết từ kiểu dữ liệu mà vẫn giữ lại các thuộc tính khác.

---

## **7. ReturnType** – Kiểu trả về của một hàm 🔄

**ReturnType** lấy kiểu trả về của một hàm và tạo ra một kiểu dữ liệu mới tương ứng với kiểu trả về của hàm đó.

### **Cú pháp**:
```typescript
type ReturnType<T extends (...args: any[]) => any> = T extends (...args: any[]) => infer R ? R : never;
```

### **Ví dụ**:
```typescript
function getPerson(): Person {
  return { name: 'George', age: 50, address: '123 Main St' };
}

type PersonReturnType = ReturnType<typeof getPerson>;

const person6: PersonReturnType = {
  name: 'George',
  age: 50,
  address: '123 Main St',
};
```

### **Ứng dụng**:
- Sử dụng khi bạn cần lấy kiểu trả về từ một hàm mà không cần phải khai báo lại kiểu trả về.

---

## **Tóm Tắt** 📝

Các **Utility Types** trong TypeScript giúp bạn thao tác với kiểu dữ liệu dễ dàng hơn và linh hoạt hơn. Dưới đây là các loại utility types mà bạn đã học:
- **Partial**: Biến tất cả các thuộc tính thành optional.
- **Required**: Biến tất cả các thuộc tính thành required.
- **Readonly**: Biến tất cả các thuộc tính thành readonly.
- **Record**: Tạo kiểu mới với key là một tập hợp và giá trị có kiểu xác định.
- **Pick**: Lựa chọn một tập hợp các thuộc tính từ kiểu dữ liệu.
- **Omit**: Loại bỏ một tập hợp các thuộc tính từ kiểu dữ liệu.
- **ReturnType**: Lấy kiểu trả về của một hàm.

---

### **Tài Liệu Tham Khảo 📚**

- [Utility Types trong TypeScript - Official Documentation](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- [TypeScript Handbook - Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)
