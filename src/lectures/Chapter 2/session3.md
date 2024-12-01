# **Strictness - Tìm hiểu về strict flag trong TypeScript 🛡️**

Trong **TypeScript**, **strict flag** là một tính năng quan trọng giúp tăng cường kiểm tra kiểu dữ liệu, đảm bảo rằng mã nguồn của bạn không có các lỗi không mong muốn khi chạy. Khi bật chế độ strict, TypeScript sẽ phát hiện sớm các lỗi có thể xảy ra, giúp việc lập trình trở nên an toàn và chính xác hơn. Hãy cùng tìm hiểu chi tiết về **strict flag** và các tùy chọn liên quan đến nó.

---

## **AGENDA** 🎓
1. **Strict flag là gì?**  
2. **Option: noImplicitAny**  
3. **Option: strictNullChecks**  
4. **Option: alwaysStrict**  
5. **Other options**  
6. **Summary**  

---

## **1. Strict flag là gì? 🔒**

**Strict flag** trong TypeScript là một tính năng cực kỳ quan trọng, giúp đảm bảo mã nguồn của bạn được kiểm tra nghiêm ngặt và tránh các lỗi không mong muốn trong quá trình biên dịch. Khi bạn bật **`strict=true`**, tất cả các tùy chọn kiểm tra nghiêm ngặt sẽ được kích hoạt, đồng thời giúp bạn tránh được các lỗi tiềm ẩn có thể xảy ra khi mã chạy.

Trong TypeScript, **strict mode** là một cách để bật tất cả các tùy chọn kiểm tra nghiêm ngặt, làm cho quá trình phát triển trở nên an toàn hơn. Những lỗi liên quan đến kiểu dữ liệu như `null` hoặc `undefined`, kiểu dữ liệu mơ hồ (`any`), và nhiều vấn đề khác sẽ được TypeScript kiểm tra và cảnh báo ngay khi biên dịch, giúp bạn phát hiện sớm và xử lý chúng trước khi mã được chạy trong môi trường thực tế.

Mặc dù **mặc định** trong TypeScript là **tất cả các tùy chọn strict** đều được đặt là `false`, nhưng **khuyến khích sử dụng `strict=true`** để đảm bảo mã nguồn của bạn được kiểm tra đầy đủ và an toàn hơn.

---

#### **Ví dụ về cấu hình `strict=true` trong `tsconfig.json`:**

Khi bạn bật `strict=true`, tất cả các tùy chọn kiểm tra nghiêm ngặt của TypeScript sẽ được tự động kích hoạt. Tuy nhiên, bạn cũng có thể điều chỉnh cấu hình riêng cho từng tùy chọn nếu muốn tùy chỉnh.

##### **Cấu hình `tsconfig.json` với `strict=true`:**
```json
{
  "compilerOptions": {
    "strict": true,  // Bật tất cả các tùy chọn strict
    "noImplicitAny": true,  // Cấm kiểu any ngầm định
    "strictNullChecks": true,  // Kiểm tra null và undefined nghiêm ngặt
    "strictFunctionTypes": true,  // Kiểm tra nghiêm ngặt kiểu hàm
    "strictBindCallApply": true,  // Kiểm tra bind/call/apply đúng kiểu
    "strictPropertyInitialization": true,  // Kiểm tra khởi tạo thuộc tính trong class
    "noImplicitThis": true,  // Kiểm tra kiểu this
    "alwaysStrict": true  // Đảm bảo mã được biên dịch dưới chế độ strict
  }
}
```

#### **Giải thích chi tiết các tùy chọn strict trong cấu hình trên:**

1. **`strict`**: Bật tất cả các tùy chọn kiểm tra nghiêm ngặt của TypeScript. Khi bật `strict=true`, các tùy chọn như `noImplicitAny`, `strictNullChecks`, v.v... sẽ được bật mặc định. Đây là cách dễ dàng để bảo vệ mã nguồn của bạn khỏi các lỗi tiềm ẩn.
   
2. **`noImplicitAny`**: Khi bật `noImplicitAny=true`, TypeScript sẽ yêu cầu bạn phải khai báo kiểu rõ ràng cho các biến. Nếu TypeScript không thể suy luận được kiểu, nó sẽ báo lỗi thay vì sử dụng kiểu `any`. Điều này giúp loại bỏ sự không chắc chắn trong việc xác định kiểu dữ liệu.

3. **`strictNullChecks`**: Kích hoạt `strictNullChecks=true` sẽ giúp kiểm tra xem giá trị có thể là `null` hoặc `undefined` hay không. Nếu bạn cố gắng sử dụng các giá trị này mà không xử lý đúng, TypeScript sẽ báo lỗi. Đây là một tùy chọn cực kỳ hữu ích để tránh các lỗi runtime khi làm việc với `null` hoặc `undefined`.

4. **`strictFunctionTypes`**: Kích hoạt `strictFunctionTypes=true` sẽ đảm bảo rằng các tham số của hàm được kiểm tra nghiêm ngặt, bao gồm việc so sánh kiểu tham số khi truyền vào các hàm hoặc phương thức.

5. **`strictBindCallApply`**: Khi bật `strictBindCallApply=true`, TypeScript sẽ đảm bảo rằng các phương thức `bind()`, `call()`, và `apply()` được gọi với các đối số đúng kiểu. Điều này giúp tránh các lỗi do việc sử dụng không đúng kiểu dữ liệu với các phương thức này.

6. **`strictPropertyInitialization`**: Bật `strictPropertyInitialization=true` đảm bảo rằng tất cả các thuộc tính trong lớp phải được khởi tạo trong constructor, tránh các lỗi khi truy cập các thuộc tính chưa được khởi tạo.

7. **`noImplicitThis`**: Tùy chọn này giúp kiểm tra kiểu dữ liệu của `this`. Nếu không có kiểu rõ ràng cho `this`, TypeScript sẽ báo lỗi, giúp bạn tránh được các vấn đề khi sử dụng `this` mà không xác định rõ kiểu.

8. **`alwaysStrict`**: Khi bật `alwaysStrict=true`, TypeScript sẽ đảm bảo rằng tất cả các tệp `.ts` được biên dịch dưới chế độ `strict mode`. Điều này có nghĩa là các mã JavaScript sẽ tự động được bao bọc trong `"use strict";`, giúp tránh các lỗi liên quan đến phạm vi biến và các vấn đề không mong muốn khi chạy mã.

---

#### **Ưu tiên cấu hình strict**

Khi bạn bật `strict=true`, TypeScript sẽ tự động bật tất cả các tùy chọn kiểm tra nghiêm ngặt. Tuy nhiên, nếu bạn muốn tắt hoặc điều chỉnh một số tùy chọn, bạn có thể cấu hình riêng cho từng tùy chọn trong `tsconfig.json`.

- **Ưu tiên cấu hình strict**: Khi bạn cấu hình `strict=true`, các tùy chọn như `noImplicitAny`, `strictNullChecks`, v.v... sẽ được bật mặc định. Nhưng nếu bạn cấu hình trực tiếp cho từng tùy chọn, các cấu hình đó sẽ có ưu tiên cao hơn và sẽ ghi đè lên các thiết lập từ `strict`.

#### **Ví dụ về việc ghi đè cấu hình:**

```json
{
  "compilerOptions": {
    "strict": true,  // Bật tất cả các tùy chọn strict
    "noImplicitAny": false,  // Tắt tùy chọn noImplicitAny
    "strictNullChecks": true  // Giữ lại strictNullChecks
  }
}
```

Trong trường hợp này, `strict=true` sẽ bật tất cả các tùy chọn strict, nhưng cấu hình `noImplicitAny=false` sẽ tắt tùy chọn `noImplicitAny`, còn `strictNullChecks=true` vẫn được bật. Điều này cho phép bạn có sự linh hoạt trong việc tùy chỉnh cấu hình của mình.

---

#### **Tại sao nên sử dụng strict flag?**

1. **Phát hiện lỗi sớm**: Việc bật `strict=true` giúp bạn phát hiện các lỗi về kiểu dữ liệu, `null`/`undefined`, và các vấn đề tiềm ẩn khác ngay khi biên dịch, giúp giảm thiểu lỗi trong runtime.
2. **An toàn hơn khi phát triển**: Đảm bảo rằng các lỗi không mong muốn không xảy ra trong mã của bạn, đặc biệt khi làm việc với các dự án lớn hoặc mã nguồn phức tạp.
3. **Chất lượng mã cao hơn**: Việc tuân thủ nghiêm ngặt các quy tắc kiểm tra giúp mã của bạn dễ bảo trì, dễ đọc và ít bị lỗi hơn.

---

## **2. Option: noImplicitAny 🚫**

Trong **TypeScript**, khi bạn khai báo một biến mà không chỉ định rõ kiểu dữ liệu, TypeScript sẽ tự động gán cho biến đó kiểu `any`. Kiểu `any` có thể chứa bất kỳ giá trị nào, và không có sự kiểm tra kiểu dữ liệu. Điều này có thể dẫn đến các lỗi khó phát hiện khi mã chạy.

Tùy chọn **`noImplicitAny`** trong TypeScript giúp hạn chế điều này bằng cách yêu cầu bạn phải chỉ định kiểu rõ ràng cho tất cả các biến, tham số và giá trị trả về. Nếu bạn không khai báo kiểu và TypeScript không thể suy luận kiểu của một biến, TypeScript sẽ báo lỗi và yêu cầu bạn khai báo kiểu dữ liệu.

---

#### **🔒 Giải thích chi tiết về `noImplicitAny`**

- **`noImplicitAny=true`**: TypeScript sẽ không tự động suy luận kiểu `any` cho bất kỳ biến nào. Nếu TypeScript không thể xác định kiểu của một biến, tham số, hoặc giá trị trả về, nó sẽ báo lỗi và yêu cầu bạn khai báo kiểu dữ liệu.
  
- **`noImplicitAny=false`** (mặc định): TypeScript sẽ cho phép kiểu `any` được suy luận khi không có kiểu rõ ràng, nghĩa là bạn có thể để TypeScript tự động gán kiểu cho biến mà không gặp lỗi.

---

#### **⚙️ Cấu hình `noImplicitAny` trong `tsconfig.json`**

Để bật hoặc tắt tùy chọn `noImplicitAny`, bạn cần cấu hình trong tệp `tsconfig.json`. Đây là nơi chứa các cài đặt của TypeScript cho dự án của bạn.

##### **🔼 Cấu hình bật `noImplicitAny`**:
```json
{
  "compilerOptions": {
    "noImplicitAny": true  // Bật chế độ yêu cầu khai báo kiểu dữ liệu rõ ràng
  }
}
```

##### **🔽 Cấu hình tắt `noImplicitAny`** (mặc định):
```json
{
  "compilerOptions": {
    "noImplicitAny": false  // Tắt chế độ kiểm tra kiểu dữ liệu
  }
}
```

---

#### **📝 Ví dụ minh họa:**

##### **1. Không khai báo kiểu và bật `noImplicitAny=true`**:

```typescript
function add(a, b) {
  return a + b;
}

console.log(add(1, 2)); // 3
```

Trong ví dụ trên, hàm `add` không khai báo kiểu cho các tham số `a` và `b`. Khi bạn bật **`noImplicitAny=true`**, TypeScript sẽ báo lỗi vì không thể xác định kiểu của các tham số:

```
Parameter 'a' implicitly has an 'any' type.
Parameter 'b' implicitly has an 'any' type.
```

**🚨 Giải pháp**: Bạn phải khai báo rõ kiểu của các tham số trong hàm.

```typescript
function add(a: number, b: number): number {
  return a + b;
}

console.log(add(1, 2)); // 3
```

---

##### **2. Sử dụng biến không khai báo kiểu**:

```typescript
let num;
num = 10;
num = 'Hello';  // Vẫn hợp lệ trong JavaScript, nhưng TypeScript sẽ báo lỗi khi bật `noImplicitAny`
```

Khi bạn không khai báo kiểu cho biến `num`, TypeScript không thể xác định kiểu của nó và sẽ báo lỗi:

```
Variable 'num' implicitly has an 'any' type.
```

**🛠 Giải pháp**: Bạn cần khai báo rõ kiểu dữ liệu của biến:

```typescript
let num: number;
num = 10;
num = 'Hello';  // Lỗi, vì 'num' phải là kiểu number
```

---

##### **3. Sử dụng kiểu `any` một cách hợp lý**:

Nếu bạn thực sự muốn cho phép một biến có kiểu `any`, bạn có thể khai báo kiểu `any` một cách rõ ràng:

```typescript
let value: any;
value = 10;
value = 'Hello';
value = true;
```

Dù bạn có thể sử dụng kiểu `any`, việc để **`noImplicitAny=true`** sẽ giúp bạn tránh việc sử dụng `any` không kiểm soát và giúp mã của bạn an toàn hơn.

---

#### **⚠️ Khi nào nên tắt `noImplicitAny`?**

Mặc dù khuyến khích bật **`noImplicitAny`**, trong một số trường hợp, bạn có thể cần phải tắt nó. Ví dụ:

1. **Khi sử dụng thư viện bên ngoài**: Một số thư viện JavaScript không có tệp kiểu (type definitions), điều này có thể khiến TypeScript không thể suy luận kiểu chính xác. Trong trường hợp này, bạn có thể tắt **`noImplicitAny`** tạm thời hoặc sử dụng kiểu `any` để tránh báo lỗi.

2. **Khi bạn làm việc với mã cũ hoặc mã không có kiểu**: Nếu bạn đang di chuyển một dự án JavaScript lớn sang TypeScript và không muốn gặp quá nhiều lỗi khi biên dịch, bạn có thể tắt **`noImplicitAny`** trong giai đoạn đầu và bật lại khi bạn đã dần hoàn thiện việc khai báo kiểu cho toàn bộ mã nguồn.

---

#### **📚 Kết luận**

- **`noImplicitAny`** giúp đảm bảo rằng mọi biến, tham số, hoặc giá trị trả về đều có kiểu rõ ràng, giảm thiểu rủi ro và giúp mã dễ bảo trì hơn.
- Việc bật **`noImplicitAny=true`** là một trong những thói quen tốt khi làm việc với TypeScript, giúp phát hiện lỗi sớm và bảo vệ mã nguồn khỏi các vấn đề tiềm ẩn.
- Trong một số tình huống, bạn có thể cần tắt tùy chọn này tạm thời, nhưng tốt nhất vẫn nên tuân thủ kiểm tra kiểu nghiêm ngặt.

---

## **3. Option: strictNullChecks ❌**

Trong **TypeScript**, `null` và `undefined` là những giá trị đặc biệt và có thể gây ra lỗi nếu không được xử lý đúng cách. Tùy chọn **`strictNullChecks`** giúp kiểm soát việc sử dụng các giá trị này, đảm bảo rằng bạn không vô tình gọi phương thức hoặc truy cập thuộc tính của một giá trị `null` hoặc `undefined`.

Khi **`strictNullChecks`** được bật, TypeScript sẽ yêu cầu bạn phải xử lý các giá trị `null` và `undefined` một cách rõ ràng, thay vì để chúng tự do gây ra lỗi tại runtime. Điều này giúp giảm thiểu các lỗi tiềm ẩn và làm cho mã của bạn an toàn hơn.

---

#### **🔒 Giải thích chi tiết về `strictNullChecks`**

- **`strictNullChecks=true`**: Khi bật tùy chọn này, **`null`** và **`undefined`** sẽ không được coi là kiểu dữ liệu hợp lệ cho các loại dữ liệu khác, trừ khi bạn khai báo rõ ràng. Điều này nghĩa là bạn phải kiểm tra hoặc xử lý chúng trước khi sử dụng.
  
- **`strictNullChecks=false`** (mặc định): TypeScript sẽ coi **`null`** và **`undefined`** là giá trị hợp lệ cho bất kỳ kiểu dữ liệu nào, điều này có thể dẫn đến lỗi không mong muốn khi chạy mã.

---

#### **⚙️ Cấu hình `strictNullChecks` trong `tsconfig.json`**

Để bật hoặc tắt tùy chọn **`strictNullChecks`**, bạn cần cấu hình trong tệp `tsconfig.json`. Đây là nơi chứa các cài đặt của TypeScript cho dự án của bạn.

#### **🔼 Cấu hình bật `strictNullChecks`**:
```json
{
  "compilerOptions": {
    "strictNullChecks": true  // Bật kiểm tra null và undefined nghiêm ngặt
  }
}
```

#### **🔽 Cấu hình tắt `strictNullChecks`** (mặc định):
```json
{
  "compilerOptions": {
    "strictNullChecks": false  // Tắt kiểm tra null và undefined
  }
}
```

---

#### **📝 Ví dụ minh họa:**

##### **1. Không bật `strictNullChecks` (mặc định)**:

```typescript
let str: string;
str = null;  // Không lỗi khi không bật strictNullChecks
str = undefined;  // Cũng không lỗi
```

Khi không bật **`strictNullChecks`**, bạn có thể gán `null` hoặc `undefined` cho các biến kiểu `string` mà không gặp lỗi, điều này có thể dẫn đến lỗi khi chạy mã.

---

##### **2. Bật `strictNullChecks=true`**:

```typescript
let str: string;
str = null;  // Lỗi: Type 'null' is not assignable to type 'string'
str = undefined;  // Lỗi: Type 'undefined' is not assignable to type 'string'
```

Khi bật **`strictNullChecks=true`**, TypeScript sẽ không cho phép gán `null` hoặc `undefined` cho các biến kiểu `string`, giúp tránh những lỗi tiềm ẩn. Bạn cần xử lý các giá trị này một cách rõ ràng.

---

##### **3. Kiểm tra `null` hoặc `undefined`**:

```typescript
let str: string | null = null;
if (str !== null) {
  console.log(str.length);  // OK, vì chúng ta đã kiểm tra null
} else {
  console.log("str is null");
}

let num: number | undefined = undefined;
if (num !== undefined) {
  console.log(num.toFixed(2));  // OK, vì chúng ta đã kiểm tra undefined
} else {
  console.log("num is undefined");
}
```

Khi **`strictNullChecks`** được bật, bạn cần kiểm tra rõ ràng các giá trị **`null`** hoặc **`undefined`** trước khi sử dụng chúng. Điều này giúp bảo vệ mã của bạn khỏi các lỗi khi chạy.

---

##### **4. Các kiểu dữ liệu với `strictNullChecks`**:

Khi bật **`strictNullChecks`**, **`null`** và **`undefined`** không còn là một phần của các kiểu dữ liệu cơ bản nữa, trừ khi bạn khai báo rõ ràng. Ví dụ:

```typescript
let a: string = null;  // Lỗi, vì 'null' không phải là kiểu 'string'
let b: string | null = null;  // OK, vì chúng ta đã khai báo kiểu 'string | null'
```

---

#### **⚠️ Khi nào cần tắt `strictNullChecks`?**

Mặc dù **`strictNullChecks`** giúp mã của bạn an toàn hơn, nhưng trong một số trường hợp bạn có thể cần phải tắt nó:

1. **Sử dụng với mã JavaScript cũ**: Nếu bạn đang di chuyển một dự án JavaScript sang TypeScript và không muốn phải xử lý tất cả các giá trị `null` và `undefined`, bạn có thể tắt tùy chọn này tạm thời.

2. **Làm việc với thư viện bên ngoài không có khai báo kiểu**: Nếu bạn đang làm việc với thư viện mà không có khai báo kiểu (type definitions), có thể cần tắt **`strictNullChecks`** để tránh gặp phải các vấn đề khi biên dịch.

---

#### **📚 Kết luận**

- **`strictNullChecks`** giúp kiểm soát việc sử dụng **`null`** và **`undefined`** trong TypeScript, giúp mã của bạn trở nên an toàn hơn và giảm thiểu các lỗi không mong muốn.
- Khi bật **`strictNullChecks=true`**, bạn sẽ phải xử lý các giá trị `null` và `undefined` rõ ràng trước khi sử dụng chúng.
- Mặc dù bật **`strictNullChecks`** là một thói quen tốt, trong một số trường hợp bạn có thể cần phải tắt tùy chọn này, đặc biệt là khi làm việc với mã cũ hoặc thư viện không có khai báo kiểu.

Hãy sử dụng **`strictNullChecks`** để bảo vệ mã của bạn khỏi các lỗi tiềm ẩn và giúp TypeScript trở thành công cụ mạnh mẽ hơn trong việc kiểm tra kiểu dữ liệu! 🚀

---

### **4. Option: alwaysStrict ⚙️**

Khi **`alwaysStrict=true`**, TypeScript sẽ tự động kích hoạt chế độ strict cho tất cả các tệp mã nguồn TypeScript của bạn. Điều này đảm bảo rằng tất cả mã của bạn được biên dịch dưới chế độ strict, bất kể cấu hình cụ thể của từng tệp.

#### **Cấu hình alwaysStrict**:
```json
{
  "compilerOptions": {
    "alwaysStrict": true  // Đảm bảo mã được biên dịch dưới chế độ strict
  }
}
```

- Mã JavaScript được biên dịch từ TypeScript sẽ tự động bao gồm `"use strict";` ở đầu file.

---

## **5. Other Options 🔧**

Ngoài các tùy chọn đã đề cập, TypeScript còn cung cấp một số tùy chọn khác trong cấu hình **strict flag** để kiểm tra mã nguồn của bạn:

| **Option**                     | **Mô tả**                                                  |
|---------------------------------|------------------------------------------------------------|
| **strictBindCallApply**         | Đảm bảo `bind`, `call`, và `apply` được gọi với các đối số đúng kiểu. |
| **strictFunctionTypes**         | Kiểm tra kiểu của các tham số hàm nghiêm ngặt (không áp dụng cho method). |
| **strictPropertyInitialization**| Kiểm tra rằng tất cả các thuộc tính trong lớp đều được khởi tạo trong constructor. |
| **noImplicitThis**              | Đảm bảo rằng `this` không có kiểu `any`.                   |
| **useUnknownInCatchVariables**  | Đảm bảo rằng các biến trong `catch` có kiểu là `unknown` (v4.4 trở lên). |

Tham khảo thêm tại [TypeScript Strict Configuration](https://www.typescriptlang.org/tsconfig#strict).

---

## **6. Tóm tắt 🔑**

- **strict flag** giúp kiểm tra kiểu dữ liệu nghiêm ngặt, giúp phát hiện lỗi sớm.
- **noImplicitAny** ngăn việc sử dụng kiểu `any` ngầm định.
- **strictNullChecks** giúp tránh lỗi liên quan đến `null` và `undefined`.
- **alwaysStrict** kích hoạt chế độ strict cho tất cả các tệp.
- Các tùy chọn khác giúp kiểm tra các hàm, thuộc tính lớp và các trường hợp `this`.

---

### **Liên kết tham khảo 🌐**

- [TypeScript Strict Configuration](https://www.typescriptlang.org/tsconfig#strict)
- [Basarat's TypeScript Book](https://basarat.gitbook.io/typescript/intro/noimplicitany)

