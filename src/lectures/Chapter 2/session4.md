# **Equality / Comparison in TypeScript** ⚖️

Việc so sánh giữa các giá trị và đối tượng trong TypeScript rất quan trọng để đảm bảo mã của bạn hoạt động đúng như mong muốn. TypeScript kế thừa hầu hết các quy tắc so sánh từ JavaScript, nhưng cũng có một số sự khác biệt cần lưu ý. 

Cùng bắt đầu tìm hiểu cách TypeScript xử lý các phép toán so sánh và các lưu ý khi làm việc với chúng nhé! 🚀

---

## **1. Nhắc lại về `==` và `===` bên JavaScript** 🔄

#### **Toán tử `==` (Equality - So sánh giá trị)**

- **`==`** so sánh giá trị của hai đối tượng nhưng có thể chuyển đổi kiểu dữ liệu (type coercion) nếu cần.
- Khi sử dụng **`==`**, JavaScript tự động chuyển đổi kiểu dữ liệu nếu các kiểu không tương thích.

#### **Toán tử `===` (Strict Equality - So sánh giá trị và kiểu)**

- **`===`** so sánh cả giá trị và kiểu dữ liệu của hai đối tượng. Không có chuyển đổi kiểu dữ liệu (type coercion).
- Đây là toán tử **an toàn hơn** và được khuyến nghị sử dụng để tránh các lỗi tiềm ẩn do chuyển đổi kiểu không mong muốn.

#### **Ví dụ về `==` và `===`:**

```javascript
console.log(1 == '1');  // true, vì '1' được chuyển đổi thành số
console.log(1 === '1'); // false, vì kiểu dữ liệu khác nhau (số và chuỗi)
```

- **`==`** sẽ trả về **`true`** vì JavaScript tự động chuyển đổi chuỗi `'1'` thành kiểu số.
- **`===`** trả về **`false`** vì `1` là kiểu số và `'1'` là kiểu chuỗi.

---

## **2. So sánh trong TypeScript?** 💻

#### **Sự khác biệt chính trong TypeScript**:

- TypeScript thừa hưởng tất cả các quy tắc so sánh từ JavaScript, tuy nhiên, TypeScript có hệ thống kiểu tĩnh, điều này giúp kiểm tra các kiểu dữ liệu trong quá trình biên dịch.
- **`===`** luôn được khuyến khích sử dụng vì nó đảm bảo bạn so sánh cả giá trị và kiểu dữ liệu, giúp tránh lỗi do chuyển đổi kiểu.

#### **Ví dụ trong TypeScript:**

```typescript
let num: number = 10;
let str: string = '10';

console.log(num == str);  // true, vì TypeScript không báo lỗi trong so sánh này
console.log(num === str); // false, vì num là số và str là chuỗi
```

- TypeScript không cho phép so sánh kiểu không tương thích nếu kiểu dữ liệu không khớp trong trường hợp sử dụng `===`. Nhưng nếu sử dụng `==`, TypeScript sẽ không báo lỗi.

---

## **3. So sánh Object trong TypeScript** 🧑‍💻

Khi bạn so sánh **object** (đối tượng), **array** (mảng) hoặc **function** (hàm) trong **JavaScript** và **TypeScript**, toán tử **`==`** và **`===`** không so sánh nội dung của chúng mà chỉ so sánh **tham chiếu** (reference).

#### **So sánh tham chiếu của object:**

Trong JavaScript và TypeScript, mỗi **object** (bao gồm **array** và **function**) là một tham chiếu, và khi bạn so sánh hai đối tượng, bạn thực sự đang so sánh địa chỉ bộ nhớ mà đối tượng đó tham chiếu đến.

#### **Ví dụ về so sánh object:**

```typescript
let obj1 = { name: "Alice" };
let obj2 = { name: "Alice" };
let obj3 = obj1;

console.log(obj1 === obj2); // false, vì chúng là các đối tượng khác nhau mặc dù có cùng giá trị
console.log(obj1 === obj3); // true, vì obj1 và obj3 trỏ tới cùng một đối tượng
```

#### **Giải thích**:
- **`obj1 === obj2`** trả về **`false`** vì dù cả hai đối tượng có cùng giá trị nhưng chúng không phải là cùng một đối tượng trong bộ nhớ.
- **`obj1 === obj3`** trả về **`true`** vì **`obj3`** chỉ là một biến tham chiếu đến **`obj1`**, vì vậy chúng trỏ tới cùng một địa chỉ bộ nhớ.

---

### **4. So sánh Array trong TypeScript** 🧳

So sánh mảng trong JavaScript và TypeScript cũng giống như so sánh object. Toán tử **`===`** và **`==`** chỉ so sánh **tham chiếu** của mảng, không phải nội dung bên trong mảng.

#### **Ví dụ về so sánh mảng:**

```typescript
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
let arr3 = arr1;

console.log(arr1 === arr2); // false, vì arr1 và arr2 là hai mảng khác nhau trong bộ nhớ
console.log(arr1 === arr3); // true, vì arr1 và arr3 trỏ tới cùng một mảng
```

#### **Giải thích**:
- **`arr1 === arr2`** trả về **`false`** vì chúng là hai mảng khác nhau, mặc dù nội dung bên trong giống nhau.
- **`arr1 === arr3`** trả về **`true`** vì cả hai biến đều tham chiếu tới cùng một mảng.

---

## **5. `null` vs `undefined` trong TypeScript** 🚫

Trong JavaScript và TypeScript, **`null`** và **`undefined`** đều đại diện cho "không có giá trị", nhưng chúng có những điểm khác biệt quan trọng về ngữ nghĩa và kiểu dữ liệu.

| **Giá trị**   | **Mô tả**                                           |
|---------------|-----------------------------------------------------|
| **`null`**    | Đại diện cho một **giá trị trống** hoặc **không có đối tượng**. ❌ |
| **`undefined`**| Đại diện cho một biến được khai báo nhưng chưa có giá trị. ⚠️ |

#### **So sánh `null` và `undefined`:**

```typescript
let a: null = null;
let b: undefined = undefined;

console.log(a == b);   // true, vì cả hai đều "không có giá trị"
console.log(a === b);  // false, vì chúng có kiểu khác nhau
```

#### **Giải thích**:
- **`null == undefined`** trả về **`true`** vì trong JavaScript và TypeScript, **`null`** và **`undefined`** đều đại diện cho "không có giá trị" khi so sánh bằng **`==`**.
- **`null === undefined`** trả về **`false`** vì chúng có kiểu khác nhau: **`null`** có kiểu là **`object`**, còn **`undefined`** có kiểu là **`undefined`**.

#### **Ví dụ khác với `null` và `undefined`:**

```typescript
let variable1: null = null;
let variable2: undefined;

console.log(variable1 == variable2); // true, vì cả hai đều không có giá trị
console.log(variable1 === variable2); // false, vì kiểu của chúng khác nhau
```

---

## **📝 Tóm tắt**

- **`==`**: So sánh giá trị và có thể thực hiện **type coercion** (chuyển đổi kiểu dữ liệu). 🔄
- **`===`**: So sánh cả giá trị và kiểu dữ liệu, không có chuyển đổi kiểu, được khuyến khích sử dụng. ✅
- **So sánh Object và Array**: So sánh **tham chiếu** (reference), không phải nội dung. 📦
- **`null`** và **`undefined`**: Đại diện cho "không có giá trị", nhưng có sự khác biệt về kiểu dữ liệu và ngữ nghĩa. 🚫

---

### **📚 Lời khuyên**

- **Luôn sử dụng `===` thay vì `==`** để tránh lỗi do chuyển đổi kiểu không mong muốn. ✅
- **So sánh nội dung của object hoặc array**: Nếu bạn cần so sánh nội dung, hãy sử dụng phương pháp như **`JSON.stringify()`** hoặc thư viện bên ngoài như **Lodash**. 🔍
- **Cẩn thận với `null` và `undefined`**, đảm bảo bạn hiểu rõ sự khác biệt và cách sử dụng chúng trong mã nguồn của mình. ⚠️

