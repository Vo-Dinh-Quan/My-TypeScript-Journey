# **Giới thiệu về TypeScript trong Frontend**

Trong bài giảng này, chúng ta sẽ tìm hiểu về **TypeScript cơ bản**, với các chủ đề sau:

1. **Static Type Checking**
2. **Types for Tooling**
3. **tsc - TypeScript Compiler**
4. **Emitting with Errors**

Nguồn tài liệu tham khảo từ [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/2/basic-types.html).

---

## **1. Static Type Checking** 🛠️

**TypeScript giúp gì?**
- TypeScript cung cấp khả năng **kiểm tra kiểu dữ liệu tĩnh** ngay trong lúc bạn đang viết mã. Điều này có nghĩa là **lỗi sẽ được phát hiện ngay khi viết mã, thay vì khi chạy ứng dụng** như JavaScript.
  
**Lợi ích của Static Type Checking:**
- **Phát hiện lỗi typos**: Khi bạn viết sai tên biến hoặc gọi hàm không đúng, TypeScript sẽ cảnh báo ngay lập tức. Đây là một vấn đề phổ biến trong JavaScript, nơi các lỗi này chỉ được phát hiện khi chạy mã.
- **Giúp tiết kiệm thời gian debug**: Không cần phải mất thời gian debug các lỗi phát sinh khi chạy ứng dụng vì chúng đã được kiểm tra và thông báo ngay từ khi viết mã.
  
Ví dụ trong TypeScript:
```typescript
let name: string = "Quân";
// Lỗi nếu bạn gán một giá trị không phải kiểu string:
name = 123; // Error: Type 'number' is not assignable to type 'string'.
```

---

## **2. Types for Tooling** 🔧

**Những công cụ hữu ích trong TypeScript:**
- **Auto-completion**: TypeScript giúp cung cấp gợi ý tự động khi bạn gõ mã, điều này giúp tránh được các lỗi về tên biến hay hàm.
- **Suggestions**: Ngoài việc cung cấp auto-completions, TypeScript còn hỗ trợ bạn thông qua các gợi ý về cách sử dụng các API, đối tượng hoặc hàm với kiểu dữ liệu tương thích.
  
**Ví dụ về auto-completion trong TypeScript:**
- Khi bạn khai báo kiểu dữ liệu cho biến hoặc hàm, editor sẽ cung cấp các gợi ý về các phương thức, thuộc tính mà bạn có thể sử dụng, giúp bạn tránh những lỗi phổ biến khi không biết chính xác các hàm hoặc phương thức có sẵn.
  
```typescript
let obj: { name: string, age: number } = { name: "Thuận", age: 42 };
// Khi gọi obj., bạn sẽ thấy tất cả các thuộc tính như "name" và "age" trong gợi ý.
```

---

## **3. tsc - TypeScript Compiler** ⚙️

**Cài đặt TypeScript:**
Để bắt đầu sử dụng TypeScript, bạn cần cài đặt `typescript` thông qua npm:
```bash
npm install -g typescript
```
Sau khi cài đặt xong, bạn có thể sử dụng **tsc (TypeScript Compiler)** để biên dịch các file `.ts` thành `.js`.

**Cách biên dịch TypeScript với tsc:**

- **Biên dịch tất cả các file TypeScript trong thư mục hiện tại:**
```bash
tsc
```

- **Biên dịch một file TypeScript đơn lẻ:**
```bash
tsc index.ts
```

- **Biên dịch tất cả các file `.ts` trong thư mục `src`:**
```bash
tsc src/*.ts
```

- **Biên dịch với cấu hình từ một file `tsconfig.json`:**
```bash
tsc --project tsconfig.production.json
```

- **Chỉ tạo file khai báo (d.ts) từ file JS mà không biên dịch mã nguồn:**
```bash
tsc index.js --declaration --emitDeclarationOnly
```

**Lưu ý**: `tsconfig.json` là file cấu hình giúp bạn thiết lập các tùy chọn biên dịch cho dự án TypeScript.

---

### **4. Emitting with Errors** ⚠️

Trong quá trình biên dịch, bạn có thể gặp phải lỗi. TypeScript cung cấp tùy chọn cấu hình để xử lý lỗi trong quá trình biên dịch:

- **Tùy chọn `--noEmitOnError`:**
  - Nếu bạn bật tùy chọn này (`--noEmitOnError: true`), TypeScript sẽ **không tạo ra file `.js` nếu có lỗi biên dịch**.
  - Nếu bạn đặt `false`, TypeScript vẫn sẽ tạo ra file `.js` mặc dù có lỗi biên dịch.

**Cách sử dụng `--noEmitOnError`:**
```bash
tsc --noEmitOnError
```

Nếu bạn không muốn tạo file `.js` khi có lỗi biên dịch, bạn có thể dùng:
```bash
tsc --noEmitOnError true
```

Còn nếu bạn vẫn muốn tạo file `.js` dù có lỗi:
```bash
tsc --noEmitOnError false
```

---

### **Một số lỗi phổ biến khi dùng JavaScript:**

Các lỗi sau thường xuất hiện khi sử dụng JavaScript:

- **Lỗi không khai báo biến trước khi sử dụng**: JavaScript cho phép bạn sử dụng biến mà không cần khai báo trước, nhưng điều này có thể dẫn đến những lỗi không mong muốn khi bạn không nhận ra biến chưa được khai báo.
- **Lỗi kiểu dữ liệu**: Trong JavaScript, bạn có thể gán giá trị của các kiểu dữ liệu khác nhau cho một biến mà không bị lỗi, nhưng đôi khi điều này dẫn đến các vấn đề không thể đoán trước được.
- **Lỗi khi sử dụng hàm không đúng cách**: JavaScript không kiểm tra loại đối số mà bạn truyền vào hàm, điều này có thể dẫn đến các lỗi khó phát hiện khi chạy chương trình.

**Điểm chung của các lỗi này là: Lỗi chỉ được phát hiện khi chạy chương trình, điều này rất mất thời gian để debug. TypeScript giúp chúng ta tránh điều này bằng cách thông báo lỗi ngay khi viết mã!**

---

### **Tóm tắt**

- **Static Type Checking** giúp bạn phát hiện lỗi ngay khi viết mã.
- **Types for Tooling** cung cấp các công cụ hữu ích như auto-completion, giúp tránh lỗi phổ biến.
- **tsc - TypeScript Compiler** giúp bạn biên dịch TypeScript thành JavaScript với nhiều tùy chọn cấu hình.
- **Emitting with Errors** cho phép bạn kiểm soát việc tạo file `.js` khi có lỗi biên dịch.

Bài học này giúp bạn hiểu rõ hơn về TypeScript và cách sử dụng nó để viết mã hiệu quả và giảm thiểu lỗi trong quá trình phát triển.

---

**Chúc bạn học tốt và tiếp tục khám phá thêm về TypeScript! 🎉**

