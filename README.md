# Sổ Tay HSK

App học tiếng Trung miễn phí, đi theo thứ tự bài của **Giáo trình chuẩn HSK**. Chạy trên điện thoại như một app (PWA), dùng được khi mất mạng, không cần server.

**Bản hiện tại:** Bài 0 (phát âm) và HSK 1 bài 1–5 (52 từ, 16 điểm ngữ pháp). Bài 6–15 hiện ở trạng thái "Đang soạn".

## Tính năng

- **Bài 0 · Phát âm** (không bắt buộc học trước Bài 1): thanh điệu so với dấu tiếng Việt, 21 thanh mẫu, 36 vận mẫu, quy tắc biến điệu (3+3, 不, 一) và cách viết y, w, ü
- **Bảng ghép vần** mở được từ nút Pinyin ở đầu mọi trang: 404 âm tiết × 4 thanh, chạm để nghe, tìm nhanh âm tiết
- Luyện nghe 4 dạng: chọn thanh, bật hơi hay không, zh ch sh · z c s · j q x, -n hay -ng
- Danh sách bài học, tiến độ từng bài
- Từ vựng: chữ Hán, pinyin tô màu theo thanh, âm Hán Việt, nghĩa tiếng Việt, câu ví dụ, cấp độ theo cả HSK 2.0 và HSK 3.0
- Xem thứ tự nét và tập viết từng chữ trong ô chữ điền (田字格)
- Nghe phát âm bằng giọng đọc có sẵn trên máy
- Học thẻ, luyện tập 4 dạng câu hỏi (chọn nghĩa, chọn chữ, nghe chọn chữ, chọn pinyin đúng thanh)
- Ôn tập ngắt quãng: nhớ đúng thì giãn 1 → 2 → 4 → 7 → 15 → 30 ngày
- Chuỗi ngày học, thống kê, cài đặt

## Đưa lên GitHub Pages (miễn phí)

1. Tạo repository mới trên GitHub, ví dụ `so-tay-hsk`, để chế độ **Public**.
2. Bấm **Add file → Upload files**, kéo toàn bộ file trong thư mục này lên (gồm cả thư mục `nguon`). Bấm **Commit changes**.
3. Vào **Settings → Pages**. Ở mục *Build and deployment*, chọn **Deploy from a branch**, nhánh **main**, thư mục **/ (root)**, bấm **Save**.
4. Đợi 1–2 phút, app sẽ có ở địa chỉ `https://<tên-tài-khoản>.github.io/so-tay-hsk/`.
5. Mở địa chỉ đó trên điện thoại:
   - Android (Chrome): menu ⋮ → **Thêm vào màn hình chính** / **Cài đặt ứng dụng**.
   - iPhone (Safari): nút Chia sẻ → **Thêm vào MH chính**.

Tiến độ học được lưu trong trình duyệt của từng máy.

## Thêm bài mới

Nội dung nằm ở `nguon/data/hsk1.json`. Mỗi từ có dạng:

```json
{"h": "你", "p": "ni3", "vi": "bạn", "hv": "nhĩ", "t": "đại từ", "ex": ["你好！", "Nǐ hǎo!", "Chào bạn!"]}
```

- `p`: pinyin dạng số (1–4 là thanh, 5 là thanh nhẹ, `v` thay cho `ü`). Dấu `/` tách hai từ trong pinyin, ví dụ `mei2/guan1 xi5` → méi guānxi.
- `x: true`: từ bổ trợ, không nằm trong danh sách từ mới của bài.

Bỏ `"soon": true` ở bài vừa soạn xong, rồi chạy trong thư mục `nguon`:

```
python3 build.py
```

Lệnh này tự tải dữ liệu nét cho chữ mới, tự tra cấp HSK 2.0/3.0, rồi tạo lại `index.html`. Nhớ tăng số phiên bản `CACHE` trong `sw.js` mỗi lần cập nhật để máy người dùng nhận bản mới.

## Thêm file ghi âm cho bảng ghép vần

Hiện app dùng giọng đọc có sẵn trên máy, đọc một chữ đại diện cho mỗi âm + thanh. Muốn thay bằng ghi âm thật:

1. Tạo thư mục `audio/` ở gốc repo, đặt file theo tên âm tiết + số thanh, dùng `v` thay cho `ü`: `ma1.mp3`, `lv3.mp3`, `nve4.mp3`…
2. Thêm `audio/index.json` liệt kê các file đã có: `{"ext": "mp3", "keys": ["ma1", "ma2", "lv3"]}`.

Âm nào có file thì app phát file, âm nào chưa có thì vẫn dùng giọng máy. Nếu dùng bộ ghi âm có giấy phép phi thương mại (ví dụ CC BY-NC-ND), app phải giữ miễn phí, không quảng cáo, và ghi nguồn trong mục Giới thiệu.

## Bản quyền và nguồn dữ liệu

- Câu ví dụ, giải thích ngữ pháp và bài luyện trong app được soạn riêng. App không chứa bài khoá, audio hay bài tập của Giáo trình chuẩn HSK.
- Cấp độ HSK 2.0/3.0: [complete-hsk-vocabulary](https://github.com/drkameleon/complete-hsk-vocabulary), giấy phép MIT.
- Dữ liệu nét chữ: [Make Me a Hanzi](https://github.com/skishore/makemeahanzi) qua [hanzi-writer-data](https://github.com/chanind/hanzi-writer-data), giấy phép Arphic Public License (xem `nguon/strokes/ARPHICPL.TXT`).
- Hiển thị nét chữ: [Hanzi Writer](https://hanziwriter.org), giấy phép MIT.
- Âm đọc để chọn chữ mẫu cho bảng ghép vần: [pinyin-data](https://github.com/mozillazg/pinyin-data), giấy phép MIT. Bảng tần suất chữ của Jun Da chỉ dùng lúc tạo bảng để ưu tiên chữ thông dụng, không nằm trong app.
- Nội dung Bài 0 ở `nguon/data/phatam.json`. Phần bảng (`chart`, `syl`, `drill`) do `nguon/tools/tao_bang_am.py` tạo ra; các phần chữ còn lại sửa tay được.
