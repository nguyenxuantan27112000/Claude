# Claude — Automation Projects

Chỉ mục các dự án tự động hoá xây bằng Claude (Cowork) và các version của trang đánh giá.
Trang chỉ mục: `index.html` (GitHub Pages, mặc định tiếng Trung, có 中文 / EN / VI).

## Cấu trúc

```
index.html          trang chỉ mục (đọc dữ liệu từ projects.json)
projects.json       danh sách dự án, version, tài liệu chung
docs/               tài liệu chung, không thuộc dự án nào
<project-id>/       mỗi dự án một thư mục: v1.html, v2.html, ...
*.html (ở gốc)      trang chuyển hướng giữ link cũ
.nojekyll           tắt Jekyll trên GitHub Pages
```

## Thêm version mới cho một dự án

1. Chép file vào `<project-id>/v<N>.html`.
2. Thêm một mục vào đầu mảng `versions` của dự án trong `projects.json`:
   ```json
   { "v": N, "date": "YYYY-MM-DD", "path": "<project-id>/v<N>.html",
     "note": { "vi": "...", "en": "...", "zh": "..." } }
   ```
3. Sửa `"updated"` ở đầu `projects.json`.
4. `git add . && git commit -m "..." && git push`

## Thêm dự án mới

Tạo thư mục `<project-id>/`, rồi thêm một object vào `projects` trong `projects.json`.
Các trường: `id`, `name`, `summary`, `module`, `type` (`scheduled-task` / `script` / `report`),
`status` (`active` / `paused` / `archived`), `since`, `schedule`, `stack`, `steps`, `versions`.
Các trường text có 3 ngôn ngữ: `{ "vi": "...", "en": "...", "zh": "..." }`.

## Trước khi push (repo đang Public)

Kiểm tra trang mới không còn: địa chỉ IP, đường dẫn mạng (`\\...`), đường dẫn máy (`E:\...`),
tên model, session id / trigger id.

## Xem thử trên máy

Mở `index.html` bằng double-click sẽ không tải được `projects.json` (trình duyệt chặn `file://`).
Chạy trong thư mục repo:

```
python -m http.server 8000
```

rồi mở http://localhost:8000
