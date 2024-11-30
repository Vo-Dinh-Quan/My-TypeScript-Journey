Để cài đặt các package bằng **Yarn**:

1. **Khởi tạo dự án (nếu chưa có `package.json`)**:

    ```bash
    yarn init -y
    ```

2. **Cài đặt TypeScript**:

    ```bash
    yarn add typescript --dev
    ```

3. **Cài đặt `ts-node` để chạy TypeScript trực tiếp**:

    ```bash
    yarn add ts-node --dev
    ```

4. **Cài đặt thư viện khác (ví dụ: Express)**:

    ```bash
    yarn add express
    ```

5. **Cài đặt type definitions (nếu cần)**:
   Ví dụ, để cài đặt type definitions cho Express:

    ```bash
    yarn add @types/express --dev
    ```

6. **Cài đặt các package khác như `typescript-eslint`**:
    ```bash
    yarn add typescript-eslint --dev
    ```
7. **Kiểm tra version Typescript**:
    Cài typescript local thì thêm câu lệnh npx, global thì không cần
    ````bash
    npx tsc -v
    ```

**Lưu ý**: Tất cả các câu lệnh trên sử dụng `yarn add` thay vì `npm install` và thêm `--dev` để cài đặt các package vào `devDependencies` khi cần.


8. **Cấu hình Prettier extension**:
- tạo ra file .prettierrc rồi lên prettier.io để config