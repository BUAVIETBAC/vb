# Autu Pro trên iPhone

> **Không thể chạy trực tiếp app Python (Playwright/Chrome) trên iOS.**
> Cách làm: app Autu vẫn chạy trên máy tính Windows; iPhone là **bộ điều khiển từ xa** (xem tác vụ, hộp thư AI, Zalo CRM, nhật ký; bấm Dừng/Quét/Gửi).

## Cách 1 — Cài ngay, không cần Mac, không cần .ipa (khuyên dùng)
1. Máy tính: mở app Autu V14.30 → **Hệ thống → Điện thoại → Bật**. Ghi lại địa chỉ `http://IP:8765` và mã 6 số.
2. iPhone (cùng Wi-Fi): mở **Safari** → nhập địa chỉ → nhập mã 6 số.
3. Bấm **Chia sẻ** → **Thêm vào Màn hình chính**. Từ giờ có icon "Autu", mở toàn màn hình như app.
4. Tường lửa Windows: lần đầu chọn **Cho phép** (mạng riêng) khi được hỏi.
5. Dùng ngoài nhà: cài **Tailscale** trên cả máy tính và iPhone, rồi dùng địa chỉ Tailscale của máy tính. Đừng mở cổng ra Internet.

## Cách 3 — Lấy file .ipa KHÔNG cần Mac (GitHub Actions, miễn phí)
1. Tạo tài khoản GitHub → tạo repository **riêng tư** mới → upload toàn bộ nội dung thư mục này (kể cả `.github`).
2. Vào tab **Actions** → **Build Autu IPA (unsigned)** → **Run workflow**. Chờ khoảng 10 phút.
3. Mở lần chạy xong → mục **Artifacts** → tải **Autu-ipa** → giải nén được `Autu.ipa`.
4. Cài lên iPhone bằng **Sideloadly** hoặc **AltStore** trên Windows, đăng nhập Apple ID miễn phí (không cần tài khoản Developer). App hết hạn sau 7 ngày, cài lại để gia hạn.
(Quy trình này chưa được chạy thử; nếu báo lỗi ở bước nào, gửi mình dòng log.)

## Cách 2 — Đóng gói thành app iOS (.ipa) — cần máy Mac
Yêu cầu: macOS, Xcode, Node.js 18+, Apple ID (miễn phí: app hết hạn sau 7 ngày; tài khoản Developer 99 USD/năm: 1 năm).
```bash
cd Autu_iOS_Wrapper
npm install
npx cap add ios
# thêm các khóa trong Info.plist.additions.txt vào ios/App/App/Info.plist
npx cap sync ios
npx cap open ios
```
Trong Xcode: chọn target **App** → *Signing & Capabilities* → chọn Team (Apple ID của bạn) → đổi Bundle Identifier cho duy nhất
(ví dụ `com.tenban.autu`) → cắm iPhone → bấm ▶ để cài thẳng lên máy.
Muốn xuất file `.ipa`: **Product → Archive → Distribute App → Ad Hoc / Development**.

Lần đầu mở app: nhập địa chỉ máy tính (ví dụ `http://192.168.1.10:8765`) → nhập mã 6 số. Địa chỉ được nhớ cho lần sau.

## Lưu ý
- Máy tính phải đang bật và app Autu đang chạy thì iPhone mới điều khiển được.
- Mã ghép nối đổi được bất cứ lúc nào; nút **Ngắt mọi điện thoại** thu hồi toàn bộ phiên.
- Sai mã 5 lần: khóa 5 phút.
