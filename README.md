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
* [MaSanPham] trong bảng [ChiTietHoaDon] trỏ về [MaSanPham] của bảng [SanPham].
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

**Một số ví dụ khai thác các hàm:**

* Hàm Chuỗi: `UPPER` (Viết hoa tên sản phẩm).

<img width="1920" height="1080" alt="1  vd Hàm Chuỗi UPPER" src="https://github.com/user-attachments/assets/67b1a16e-c1ef-4093-9eb7-0a1394a33973" />

* Hàm Ngày tháng: `DATEDIFF` (Tính số ngày đã bán).

<img width="1920" height="1080" alt="2  vd Hàm Ngày tháng DATEDIFF" src="https://github.com/user-attachments/assets/1fe5c81c-db66-499a-8003-b6309d13fec1" />

* Hàm Toán học: `ROUND` (Làm tròn giá tiền hàng nghìn).

<img width="1920" height="1080" alt="3  vd Hàm Toán học ROUND" src="https://github.com/user-attachments/assets/771e385c-8ffb-412f-b740-4159021012d7" />

* Hàm Chuyển đổi: `CAST` (Ghép chữ "VNĐ" vào sau số tiền).

<img width="1920" height="1080" alt="4  vd Hàm Chuyển đổi CAST" src="https://github.com/user-attachments/assets/752c0504-9041-4a77-b4da-f37bf19e408c" />

* Hàm hệ thống/đặc sắc: `COALESCE` (Xử lý các ô bị trống/NULL).

<img width="1920" height="1080" alt="4  vd Hàm hệ thống đặc sắc COALESCE" src="https://github.com/user-attachments/assets/1554a59d-2b25-4c4d-b492-491e9a1fcd67" />

**Hàm do người dùng tự viết trong SQL (User-Defined Functions - UDF)**

* **Mục đích:** Đóng gói các logic nghiệp vụ (business logic) lặp đi lặp lại, giúp code gọn gàng, dễ bảo trì và tái sử dụng.

* **Tại sao cần tự viết?:** Vì System Function chỉ giải quyết các bài toán chung (cắt chuỗi, tính ngày). Các bài toán riêng của doanh nghiệp (ví dụ: tính lương theo bậc, tính chiết khấu khách hàng thân thiết) thì SQL Server không thể có sẵn, ta phải tự viết.

**Tất cả loại hàm**

1. Hàm Scalar Function (Hàm trả về một giá trị):

* Mục đích: Trả về 1 giá trị duy nhất.

* Khi nào dùng?: Tính toán con số cụ thể (thuế, giảm giá, điểm trung bình).

<img width="1920" height="1080" alt="5  Thực hành viết Function Scalar Function" src="https://github.com/user-attachments/assets/bb7aa47e-8863-474c-8d4d-3815be157730" />

2. Hàm Inline Table-Valued Function

* Mục đích: Trả về 1 bảng dữ liệu.

* Khi nào dùng?: Thay thế cho View khi cần truyền tham số (lọc danh sách), hiệu năng rất cao.

<img width="1920" height="1080" alt="6  Thực hành viết Function Inline Table-Valued Function" src="https://github.com/user-attachments/assets/9659e465-b105-443f-a583-2b529a83f8b8" />

3. Hàm Multi-statement Table-Valued Function

* Mục đích: Trả về 1 bảng với logic phức tạp.

* Khi nào dùng?: Khi cần khai báo biến, dùng vòng lặp, IF/ELSE trước khi trả về bảng kết quả.

<img width="1920" height="1080" alt="7  Thực hành viết Multi-statement Table-Valued Function" src="https://github.com/user-attachments/assets/58536edf-c819-4922-a643-adbc20dd645d" />

### Phần 3: Xây dựng Store Procedure

1. Tìm hiểu về System Stored Procedures

System Stored Procedures (SP có sẵn) là các thủ tục được Microsoft viết sẵn để hỗ trợ quản trị hệ thống. Chúng thường bắt đầu bằng tiền tố sp_ và nằm trong Database master.

**Một số SP hệ thống đặc sắc:**

`sp_help`: Dùng để xem thông tin chi tiết về một đối tượng (bảng, hàm, view).

*	Cách dùng: `EXEC sp_help '[SanPham]';`

<img width="1920" height="1080" alt="1  sp_help" src="https://github.com/user-attachments/assets/67da7f45-2dca-4a81-8468-fb5aaa7187dc" />

`sp_spaceused`: Hiển thị kích thước dữ liệu và không gian lưu trữ mà bảng hoặc database đang chiếm dụng.

*	Cách dùng: `EXEC sp_spaceused '[ChiTietHoaDon]';`

<img width="1920" height="1080" alt="2  sp_spaceused" src="https://github.com/user-attachments/assets/70fd1e55-872c-4dda-b5bc-65d3aedee209" />

`sp_helpconstraint`: Liệt kê tất cả các ràng buộc (Constraints) đang áp dụng lên bảng, bao gồm Khóa chính (PK), Khóa ngoại (FK) và Ràng buộc kiểm tra (CK).

*	Cách dùng: `EXEC sp_helpconstraint '[ChiTietHoaDon]';`

<img width="1920" height="1080" alt="3  sp_helpconstraint" src="https://github.com/user-attachments/assets/1bc2b5ed-7813-41a7-b51f-f5a3b975d408" />

`sp_databases`: Liệt kê toàn bộ các cơ sở dữ liệu đang có trên Server. Giúp người dùng xác định nhanh tên và kích thước của các DB hiện tại.

*	Cách dùng: `EXEC sp_databases;`

<img width="1920" height="1080" alt="4  sp_databases" src="https://github.com/user-attachments/assets/9edbce5b-a2d7-4de3-881d-25d2b86ed762" />

2. Thực hành viết Stored Procedure

SP Thêm Sản phẩm mới (Có kiểm tra điều kiện logic)

* Yêu cầu: Tạo SP thêm sản phẩm. Nếu giá bán $\le 0$ hoặc mã loại không tồn tại thì không cho thêm và báo lỗi.

<img width="1920" height="1080" alt="5  SP Thêm Sản phẩm mới" src="https://github.com/user-attachments/assets/f8990d2d-f02b-4e37-b5d2-10aefd6a838a" />

SP Tính tổng tiền kho hàng (Sử dụng tham số OUTPUT)

* Yêu cầu: Tính tổng giá trị tồn kho của một loại sản phẩm nhất định và trả kết quả về thông qua biến OUTPUT.Công thức: $\text{Tổng giá trị} = \sum (\text{GiaBan} \times \text{SoLuongTon})$

<img width="1920" height="1080" alt="7  SP Xuất báo cáo bán hàng chi tiết" src="https://github.com/user-attachments/assets/22a7958e-1561-4b77-b3d5-dcfec8bbd450" />

### Phần 4: Trigger và Xử lý logic nghiệp vụ

1. Trigger tự động cập nhật số lượng tồn kho

**Kịch bản thực tế:** Khi một mặt hàng được bán (chèn dữ liệu vào bảng `ChiTietHoaDon`), hệ thống phải tự động trừ số lượng tương ứng trong bảng `SanPham` để quản lý kho chính xác.

<img width="1920" height="1080" alt="1  Trigger tự động cập nhật số lượng tồn kho" src="https://github.com/user-attachments/assets/b5ae66d5-1b4e-4101-a4f6-72ab91894ffc" />

* Thử Nghiệm

<img width="1920" height="1080" alt="2  Thử nghiệm Trigger tự động cập nhật số lượng tồn kho" src="https://github.com/user-attachments/assets/9c7c7ff6-69da-4563-acea-bc6a722de31f" />

* Kiểm tra lại bảng `SanPham` để thấy `SoLuongTon` đã tự động trừ đi 5

<img width="1920" height="1080" alt="3  Kiểm tra lại bảng SanPham để thấy SoLuongTon đã tự động trừ đi 5" src="https://github.com/user-attachments/assets/10303281-48d0-4fbe-a898-6c9cfc797724" />

* Thử nghiệm Trigger vòng lặp (Recursive Trigger)

**Yêu cầu:** Tạo 2 trigger đá qua lại giữa bảng A `(SanPham)` và bảng B `(ChiTietHoaDon)` để quan sát hiện tượng.

* Bước 1: Tạo Trigger trên bảng A cập nhật bảng B

<img width="1920" height="1080" alt="4  Bước 1 Tạo Trigger trên bảng A cập nhật bảng B" src="https://github.com/user-attachments/assets/1a8b4e56-29f7-4e20-ae30-ea992d5358ce" />

* Bước 2: Tạo Trigger trên bảng B cập nhật ngược lại bảng A

<img width="1920" height="1080" alt="5  Bước 2 Tạo Trigger trên bảng B cập nhật ngược lại bảng A" src="https://github.com/user-attachments/assets/82d85452-0dea-417c-942b-af4a7fac9561" />

* Bước 3: Kích hoạt thử nghiệm

<img width="1920" height="1080" alt="6  Bước 3 Kích hoạt thử nghiệm" src="https://github.com/user-attachments/assets/e3ea2fb1-3d7e-4807-bf51-d93076f7a2c6" />

3. Giải thích và Nhận xét

**Hiện tượng quan sát được:** Khi chạy lệnh cập nhật ở Bước 3, hệ thống sẽ báo lỗi hoặc dừng lại sau một loạt thông báo. SQL Server có một cơ chế bảo vệ gọi là `"Maximum stored procedure, function, trigger, or view nesting level exceeded (limit 32)"`.

**Giải thích thông báo:**

* Trigger A kích hoạt làm bảng B thay đổi.

* Bảng B thay đổi lại kích hoạt Trigger B.

* Trigger B cập nhật ngược lại bảng A, làm Trigger A chạy tiếp lần nữa...

* Đây gọi là hiện tượng Đệ quy (Recursion) hoặc Vòng lặp vô tận (Infinite Loop).

Nhận xét cuối cùng:

*1. Về logic:* Việc thiết kế trigger cập nhật chéo nhau như trên là một lỗi nghiêm trọng trong thiết kế CSDL (Circular Dependency). Nó gây tốn tài nguyên hệ thống và làm treo các giao dịch.
  
*2. Về kỹ thuật:* SQL Server chỉ cho phép lồng nhau tối đa 32 cấp. Nếu vượt quá, nó sẽ tự ngắt để bảo vệ Database không bị sụp đổ.

*3. Lời khuyên:* Khi viết Trigger, chỉ nên viết theo một chiều (từ bảng nghiệp vụ sang bảng dữ liệu tổng hợp) và phải kiểm soát chặt chẽ điều kiện cập nhật để tránh gây ra lỗi vòng lặp.

### Phần 5: Cursor và Duyệt dữ liệu

1. Sử dụng CURSOR để duyệt và xử lý từng bản ghi

**Bài toán:** Duyệt qua danh sách sản phẩm trong kho. Với mỗi sản phẩm, dựa vào số lượng tồn để in ra một thông báo cụ thể (Nhãn dán trạng thái) để nhân viên kho dễ dàng theo dõi.

<img width="1920" height="1080" alt="1  Sử dụng CURSOR để duyệt và xử lý từng bản ghi" src="https://github.com/user-attachments/assets/c936ada8-ce76-4668-a049-5e7999cf3a5e" />

2. Giải quyết bài toán không dùng CURSOR (Set-based)

Trong SQL, cách tối ưu hơn là dùng lệnh SELECT kết hợp biểu thức CASE.

<img width="1920" height="1080" alt="2  Giải quyết bài toán không dùng CURSOR (Set-based)" src="https://github.com/user-attachments/assets/0a7fa779-9d73-47b2-8216-0790725ac7f0" />

3. So sánh tốc độ và Minh chứng

**Cách đo thời gian:** bật chế độ đo thời gian bằng lệnh sau trước khi chạy cả 2 đoạn code trên:

<img width="1920" height="1080" alt="3  So Sánh Tốc Độ" src="https://github.com/user-attachments/assets/d99aa29e-ae40-4a2d-957d-9e3dea67a9fb" />

**Nhận xét:**

* Kết quả: Sau khi chạy, ở tab Messages, thời gian "CPU time" và "Elapsed time" của lệnh SELECT (không dùng cursor) gần như bằng 0ms, trong khi Cursor sẽ tốn thời gian hơn (đặc biệt nếu bảng có hàng ngàn dòng).

* Kết luận: SQL Server được tối ưu hóa cho các thao tác tập hợp (Set-based). Cursor bắt hệ thống phải mở/đóng và di chuyển con trỏ qua từng dòng, gây tốn tài nguyên hơn rất nhiều. Không nên dùng Cursor nếu lệnh SELECT thông thường có thể giải quyết được.

4. Bài toán "Chỉ CURSOR mới giải quyết được"

Có những tình huống mà SQL thuần (Set-based) rất khó giải quyết, đó là Các thao tác nghiệp vụ bên ngoài Database cho từng dòng dữ liệu.

**Ví dụ thực tế:**
Cần duyệt qua danh sách các hóa đơn bán hàng trong ngày. Với mỗi hóa đơn, không chỉ tính tổng tiền mà còn phải:

* Gửi một Email/Tin nhắn cảm ơn riêng biệt cho khách hàng đó (thông qua một thủ tục hệ thống hoặc gọi API bên ngoài).

* Thực thi một chuỗi các câu lệnh SQL động (Dynamic SQL) khác nhau tùy thuộc vào dữ liệu của từng dòng (Ví dụ: Nếu là khách VIP thì chạy Procedure giảm giá, nếu khách vãng lai thì chạy Procedure tích điểm).

**Tại sao SQL thông thường khó làm?** Vì các lệnh `SELECT`, `UPDATE` chỉ tác động lên dữ liệu trong bảng. Chúng không thể thực hiện các hành động "ngắt quãng" và "gọi lệnh thực thi bên ngoài" cho từng dòng một cách tuần tự như Cursor.
