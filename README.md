# 🧭 Jagat Morphe Patches (`io.jagat.lite`)

Bộ patch chính thức dành cho ứng dụng **Jagat** (phiên bản `6.8.4` và các bản cập nhật tiếp theo) được phát triển trên nền tảng **Morphe Patcher**.

---

## 🌟 Các tính năng nổi bật (Features)

### 1. 🚫 Chặn quảng cáo toàn diện (Block Ads) - *Ưu tiên số 1*
- **Triệt tiêu TopOn Mediation SDK**: Hook trực tiếp vào `TopOnAdManager`, vô hiệu hóa hàm `init()`, `start()`, `loadSplashAd()`, `loadBannerAd()`, `loadInterstitialAd()`.
- **Chặn ScreenAdActivity**: Ngăn chặn hoàn toàn activity quảng cáo bật lên che kín màn hình khi mở và sử dụng app; tự động đóng ngay lập tức nếu được kích hoạt.
- **Dừng nạp video chạy ngầm (`ScreenAdFetch`)**: Ngăn app âm thầm tải video quảng cáo về bộ nhớ máy, tiết kiệm tối đa băng thông mạng (4G/5G).
- **Vô hiệu hóa AdConfig & Banner**: Ghi đè `AdConfigManager.getConfigIsShow()` trả về `false`, ẩn triệt để các khung quảng cáo trong tab User Center (`UserAdsBannerView`, `AdsView`).

### 2. 📍 Tùy chỉnh vị trí & Chế độ bóng ma (Ghost Mode)
- **Đóng băng vị trí (Freeze Location)**: Cho phép giữ nguyên toạ độ thực tế tại một vị trí cố định, không gửi toạ độ mới lên server khi bạn di chuyển.
- **Giả lập toạ độ tuỳ chỉnh (Mock Location)**: Ghi đè kinh độ/vĩ độ theo mong muốn.
- **Bypass kiểm tra Fake GPS**: Tự động xóa cờ `isFromMockProvider()` trên đối tượng `Location` trước khi ứng dụng gửi dữ liệu đi, đảm bảo tính ẩn danh và an toàn cho tài khoản.

### 3. 🔋 Tối ưu pin & Giảm tải dịch vụ nền (Battery Optimization)
- **Hạn chế giữ WakeLock**: Giảm tải tần suất chạy của `LongTimeLocWorker` và `PowerSaverReceiver` khi thiết bị đang tắt màn hình.
- Giảm thiểu tình trạng máy nóng và tụt pin do chip GPS bị kích hoạt quét liên tục.

---

## 📱 Cách áp dụng bản patch

### Cách 1: Sử dụng Morphe Manager trên điện thoại Android (Khuyên dùng)
1. Cài đặt **Morphe Manager** trên thiết bị Android.
2. Mở ứng dụng **Morphe Manager** -> Chuyển đến mục **Settings** -> **Sources**.
3. Thêm URL repository GitHub của bạn vào mục **Custom Patch Source**:
   ```text
   https://github.com/pnam-ng/pnamng-morphe-patchs
   ```
4. Chọn ứng dụng **Jagat**, tick chọn các patch mong muốn:
   - `Chặn quảng cáo (Block Ads)`
   - `Chỉnh sửa vị trí & Đóng băng toạ độ (Ghost Mode)`
   - `Tối ưu pin & Giảm tải nền (Battery Optimization)`
5. Nhấn **Patch** và cài đặt file APK hoàn thiện.

---

### Cách 2: Tự động phát hành qua GitHub Actions (Official Release)
Repository này đã được tích hợp sẵn workflow tự động hoá hoàn chỉnh tại `.github/workflows/release.yml`:
1. Đẩy mã nguồn lên GitHub:
   ```bash
   git remote set-url origin https://github.com/pnam-ng/pnamng-morphe-patchs.git
   git push -u origin main
   ```
2. GitHub Actions sẽ tự động biên dịch, ký số và phát hành file `patches-x.x.x.mpp` kèm theo metadata `patches-list.json` trên mục **Releases**.

---

### Cách 3: Biên dịch thủ công trên máy tính
Để build lại file bundle `.mpp`:
```bash
./gradlew :patches:buildAndroid
```
File bundle đầu ra sẽ nằm tại:
`patches/build/libs/patches-1.0.0.mpp`
