## Cấu trúc commit chuẩn

### Thành phần cơ bản của một commit message:

Một cấu trúc commit chuẩn thường gồm 3 phần chính:

* **Type (loại commit):** Mô tả thay đổi (fix, feat, docs)
* **Scope (Phạm vi)**: Phần nào của dự án bị ảnh hưởng (frontend, backend, API, v.v.).
* **Description (Mô tả)**: Mô tả ngắn gọn, rõ ràng về thay đổi.

Cấu trúc cơ bản của một commit message:

```
type(scope): description

[<body: Mô tả chi tiết hơn về các thay đổi>]

[<footer: Thông tin bổ sung, như issue ID, breaking change>]

[]: Các trường tùy chọn
```

Ví dụ:

```
feat(auth): add login with Google OAuth

Implement Google OAuth2 flow for user authentication.
Add new endpoint /auth/google for redirecting to Google login.
Update user model to store Google ID.

Closes #123
```

#123

### Các loại commit phổ biến

| Type         | Ý Nghĩa                                                         | Ví Dụ                                     |
| ------------ | ----------------------------------------------------------------- | ------------------------------------------- |
| `feat`     | Thêm tính năng mới                                            | `feat(cart): add shopping cart checkout`  |
| `fix`      | Sửa lỗi                                                         | `fix(api): handle null response error`    |
| `docs`     | Chỉ thay đổi tài liệu (README, comment code, v.v.)           | `docs(readme): update installation guide` |
| `style`    | Thay đổi định dạng code (không ảnh hưởng logic)          | `style(css): format with prettier`        |
| `refactor` | Tái cấu trúc code (không thêm tính năng, không sửa lỗi) | `refactor(auth): simplify login logic`    |
| `test`     | Thêm hoặc sửa test case                                        | `test(unit): add tests for user model`    |
| `chore`    | Các thay đổi linh tinh (cập nhật dependency, config, v.v.)   | `chore(deps): update lodash to v4.17.21`  |
| `perf`     | Cải thiện hiệu suất                                           | `perf(db): optimize query performance`    |
| `ci`       | Thay đổi cấu hình CI/CD                                       | `ci(github): add linting to workflow`     |
| `build`    | Thay đổi liên quan đến build (webpack, npm scripts, v.v.)    | `build(webpack): add production config`   |

### Các scope thường dùng

* **`auth`**: Xác thực (login, logout, JWT,...)
* `ui`: Giao diện người dùng (CSS, components, v.v.).
* `api`: Các endpoint hoặc logic phía server.
* `db`: Cơ sở dữ liệu (schema, migration, query, v.v.).
* `config`: Cấu hình dự án (env, webpack, v.v.).
