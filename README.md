# Web tổng hợp các website của tôi

Một trang tĩnh **HTML/CSS/JS thuần**, không cần build, không cần cài gì. Chỉ cần sửa file `link.json` là toàn bộ nội dung (thông tin cá nhân + danh sách web) tự cập nhật.

```
/
├── index.html        ← giao diện web (CSS + JS nằm trong này)
├── link.json         ← NƠI BẠN SỬA DỮ LIỆU
├── images/           ← ảnh đại diện + ảnh bìa mẫu
│   ├── avatar.svg
│   ├── cover-portfolio.svg
│   ├── cover-todo.svg
│   ├── cover-weather.svg
│   └── cover-blog.svg
└── README.md
```

---

## 1. Đưa lên GitHub Pages (khoảng 2 phút)

1. Vào https://github.com/new → tạo repo mới, đặt tên ví dụ `my-links`, chọn **Public**.
2. Bấm **Add file → Upload files**, kéo thả **toàn bộ** các file ở trên (`index.html`, `link.json`, thư mục `images/`, `README.md`) vào, rồi **Commit changes**.
3. Trong repo: **Settings → Pages** → phần *Build and deployment* → **Deploy from a branch** → chọn branch `main`, thư mục `/ (root)` → **Save**.
4. Đợi 1–2 phút, rồi mở: `https://TEN-GITHUB-CUA-BAN.github.io/my-links/`.

> Mỗi lần sửa `link.json` (hoặc thêm ảnh), chỉ cần commit lại lên GitHub. GitHub Pages tự cập nhật sau vài chục giây. Nhấn `Ctrl + F5` nếu trình duyệt còn hiện nội dung cũ.

---

## 2. Sửa nội dung trong `link.json`

File gồm 2 phần: `profile` (cột trái) và `projects` (cột phải).

### `profile` — thông tin bên trái

| Trường | Ý nghĩa |
| --- | --- |
| `name` | Tên hiển thị |
| `username` | Dòng @ bên dưới tên |
| `avatar` | Đường dẫn ảnh đại diện (để `""` để web tự tạo ảnh chữ cái) |
| `bio` | Mô tả ngắn về bạn |
| `location` | Địa điểm |
| `status` | Dòng trạng thái có chấm xanh |
| `email` | Hiện nút **Sao chép email** |
| `socials` | Mảng các nút mạng xã hội (thêm/bớt tuỳ ý) |

Mỗi phần tử trong `socials`:

```json
{ "name": "TikTok", "icon": "tiktok", "url": "https://www.tiktok.com/@yourname", "color": "#ff2d55" }
```

Các `icon` đang có sẵn: `tiktok`, `facebook`, `github`, `youtube`, `instagram`, `linkedin`, `x`, `telegram`, `discord`, `mail`, `globe`. Nếu ghi tên khác, web sẽ dùng icon hình cầu mặc định.

### `projects` — các thẻ website

```json
{
  "name": "Tên website",
  "description": "Mô tả ngắn gọn, 1-2 câu.",
  "url": "https://link-website-cua-ban.com",
  "image": "images/ten-anh.jpg",
  "tags": ["Web", "Tool"],
  "featured": true
}
```

- `url`: link sẽ mở ra khi người dùng bấm vào thẻ (mở tab mới).
- `image`: ảnh bìa. Có 3 cách dùng:
  1. **Ảnh trong repo** (khuyên dùng): bỏ file vào `images/` rồi ghi `"image": "images/ten-file.png"`.
  2. **Ảnh online**: ghi thẳng URL, ví dụ `"image": "https://example.com/anh.jpg"`.
  3. **Để trống** `""`: web tự tạo ảnh bìa gradient có tên dự án (2 dự án cuối trong file mẫu đang dùng cách này).
- `tags`: dùng để lọc theo nhóm – các nút lọc phía trên lưới được tạo tự động từ danh sách này.
- `featured: true` → hiện nhãn **Nổi bật** trên ảnh bìa.

> Lưu ý: `link.json` phải là JSON hợp lệ (dấu phẩy giữa các phần tử, không có dấu phẩy ở phần tử cuối, dùng dấu ngoặc kép). Nếu sai cú pháp, web sẽ hiện dữ liệu mẫu và báo "Đang dùng dữ liệu mẫu".

---

## 3. Xem thử trên máy tính

Vì trình duyệt chặn đọc file JSON khi mở trực tiếp bằng `file://`, hãy chạy một server nhỏ trong thư mục chứa project:

```bash
python3 -m http.server 8000
```

Rồi mở `http://localhost:8000`. (Khi đã lên GitHub Pages thì không cần làm bước này.)

Nếu bạn mở trực tiếp `index.html` mà không có server, web vẫn chạy nhưng sẽ dùng **dữ liệu mẫu** nhúng sẵn trong file HTML – đây là cơ chế dự phòng để web không bao giờ bị trống.

---

## 4. Tuỳ biến thêm

- **Đổi màu chủ đạo**: mở `index.html`, sửa 2 biến `--accent` và `--accent2` trong block `:root` ở đầu phần CSS.
- **Đổi tiêu đề tab / chia sẻ**: sửa thẻ `<title>` và các thẻ `<meta property="og:...">` trong `index.html`.
- **Sáng / tối**: nút "Giao diện" dưới cùng cột trái, lựa chọn được lưu trong trình duyệt.

Tính năng có sẵn: ô tìm kiếm (nhấn `/` để focus), lọc theo tag, responsive trên điện thoại, chuyển sáng/tối, sao chép email, tự tạo ảnh bìa khi thiếu ảnh, và tự nhận dạng tên miền hiển thị trên mỗi thẻ.
