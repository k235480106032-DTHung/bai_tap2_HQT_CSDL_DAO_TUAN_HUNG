## Bài tập Hệ quản trị cơ sở dữ liệu (TEE560)

+ **Họ và tên:** Đào Tuấn Hưng
+ **Lớp:** K59KMT.K01
+ **Mã số sinh viên:** K235480106032
+ **Trường:** Đại học Kỹ thuật Công Nghiệp Thái Nguyên - TNUT
---

### Phần 1: Thiết kế và Khởi tạo Cấu trúc Dữ liệu

1. Chủ đề quản lý được chon cho bài tập này: Quản lý Bán hàng
* Tên Database theo đúng mã sinh viên : QuanLyBanHang_k235480106032

<img width="1920" height="1080" alt="1  tạo database" src="https://github.com/user-attachments/assets/0bca7124-f139-4e9e-b76f-d0a55a49bf82" />

2. Tạo ít nhất 3 bảng có quan hệ với nhau :
* Tạo bảng [LoaiSanPham].

<img width="1920" height="1080" alt="2  bảng loại sản phẩm" src="https://github.com/user-attachments/assets/4990b496-7fe7-468d-961a-2ca279bccbb7" />

* Tạo bảng [SanPham].

<img width="1920" height="1080" alt="3  bảng sản phẩm" src="https://github.com/user-attachments/assets/d8a39223-8f63-48a8-a99e-6b4aec341539" />

* Tạo bảng [ChiTietHoaDon].

<img width="1920" height="1080" alt="4  bảng chi tiết hóa đơn" src="https://github.com/user-attachments/assets/a2e4eed6-24e1-4886-b4e2-372bc9edb516" />

3. Kết quả

<img width="1920" height="1080" alt="5  kết quả" src="https://github.com/user-attachments/assets/3d4ea9a5-4f0a-45ce-ab87-3ddc152c0c46" />

4. Giải thích các thành phần

**PK (Primary Key - Khóa chính):**
* Nằm ở các cột: [MaLoai], [MaSanPham], [MaChiTiet].
* Tác dụng: Đảm bảo mỗi dòng dữ liệu là duy nhất, không trùng lặp.

**FK (Foreign Key - Khóa ngoại):**
* [MaLoai] trong bảng [SanPham] trỏ về [MaLoai] của bảng [LoaiSanPham].
* [MaSanPham] trong bảng [HoaDonChiTiet] trỏ về [MaSanPham] của bảng [SanPham].
* Tác dụng: Đảm bảo tính toàn vẹn dữ liệu, không thể có sản phẩm thuộc một loại không tồn tại.

**CK (Check Constraint - Ràng buộc kiểm tra):**
* [GiaBan] > 0: Ngăn chặn việc nhập sai giá bán bằng 0 hoặc âm.
* [SoLuongTon] >= 0: Đảm bảo kho không bao giờ bị âm số lượng.

**Kiểu dữ liệu:**
* NVARCHAR: Lưu tiếng Việt (Ví dụ: "Đồ điện tử").
* MONEY: Tối ưu cho tính toán tiền tệ và tỷ giá.
* DATETIME: Lưu chính xác thời điểm phát sinh giao dịch.

### Phần 2: Xây dựng Function

**Các loại hàm Build_in Funtion trong SQL Server:**

Hàm chuỗi: `LEN`, `SUBSTRING`, `REPLACE`, `UPPER`, `LOWER`.

Hàm ngày tháng: `GETDATE`, `DATEADD`, `DATEDIFF`, `YEAR`, `MONTH`.

Hàm toán học: `ABS`, `ROUND`, `CEILING`, `FLOOR`.

Hàm chuyển đổi: `CAST`, `CONVERT`, `TRY_PARSE`.

Hàm hệ thống/đặc sắc: `COALESCE`(val1, val2, ...): Trả về giá trị khác NULL đầu tiên. Rất hữu ích khi xử lý dữ liệu thiếu.

* FORMAT(): Định dạng dữ liệu theo chuẩn vùng (Culture), ví dụ định dạng tiền tệ Việt Nam.
