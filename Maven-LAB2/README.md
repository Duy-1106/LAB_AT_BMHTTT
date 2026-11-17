
# LAB 2 – MÃ HÓA ĐỐI XỨNG HIỆN ĐẠI

- **Họ và tên:** Phạm Hồng Duy
- **Mã số sinh viên:** 1150070008
- **Môn học:** An toàn và bảo mật hệ thống thông tin
- **Bài thực hành:** LAB 2 – Mã hóa đối xứng hiện đại

## Các thuật toán đã thực hiện

| STT | Thuật toán | Chức năng |
|---|---|---|
| 1 | DES | Mã hóa và giải mã bằng DES/CBC |
| 2 | TripleDES | Mã hóa và giải mã bằng 3DES/CBC |
| 3 | AES | AES-256-GCM, đăng ký và đăng nhập |
| 4 | RC4 | Mã hóa và giải mã dạng HEX |
| 5 | Twofish | Mã hóa và giải mã với Key và IV |
| 6 | AES-CTR | Mã hóa và giải mã AES-256 chế độ CTR |

## Công nghệ sử dụng

- Ngôn ngữ lập trình: Java
- IDE: Apache NetBeans
- Công cụ quản lý dự án: Maven
- Giao diện: Java Swing
- Cơ sở dữ liệu: Microsoft SQL Server
- Công cụ quản lý database: SQL Server Management Studio (SSMS)
- Thư viện: Microsoft JDBC Driver và BouncyCastle

## 5. Các chức năng chính

Ứng dụng hỗ trợ:

- Mã hóa và giải mã văn bản bằng các thuật toán đối xứng.
- Kiểm tra độ dài khóa và dữ liệu đầu vào.
- Sinh Key, IV hoặc Nonce đối với các thuật toán tương ứng.
- Lưu và mở tệp chứa bản mã.
- Đăng ký và đăng nhập tài khoản trong bài AES.
- Tạo Ticket sau khi đăng nhập thành công.
- Lưu lịch sử thao tác mã hóa, giải mã vào SQL Server.
- Xem lịch sử thao tác thông qua giao diện Java Swing.
- Sử dụng Menu chính để truy cập các chức năng.

## Cấu trúc chương trình

**LAB2_MaHoaHienDai**

- `pom.xml`: Cấu hình Maven và các thư viện.
- `CipherUtil.java`: Các hàm hỗ trợ xử lý dữ liệu.
- `DESCipher.java`: Thuật toán DES.
- `TripleDESCipher.java`: Thuật toán TripleDES.
- `AESCipher.java`: Thuật toán AES-GCM.
- `RC4Cipher.java`: Thuật toán RC4.
- `TwofishCipher.java`: Thuật toán Twofish.
- `AESCTRCipher.java`: Thuật toán AES-CTR.
- `DbConfig.java`: Cấu hình kết nối SQL Server.
- `HistoryDao.java`: Quản lý lịch sử thao tác.
- `UserDao.java`: Quản lý tài khoản người dùng.
- `FileTextIO.java`: Đọc và ghi tệp văn bản.
- `frm_Menu.java`: Giao diện Menu chính.
- Các file `frm_*.java` và `frm_*.form`: Giao diện các thuật toán.

## Cơ sở dữ liệu

**Tên database:** `LAB2_MaHoaHienDai`

Các bảng chính:

- `dbo.app_users`: Lưu tài khoản và thông tin xác thực đã được xử lý bằng thuật toán băm mật khẩu.
- `dbo.crypto_history`: Lưu lịch sử các thao tác của chương trình.

Ứng dụng sử dụng JDBC để kết nối Java với Microsoft SQL Server.

## Hướng dẫn chạy chương trình

1. Mở Apache NetBeans.
2. Chọn **File → Open Project**.
3. Mở project `LAB2_MaHoaHienDai`.
4. Kiểm tra các thư viện Maven.
5. Cấu hình kết nối đến SQL Server.
6. Chọn **Clean and Build** để biên dịch.
7. Chạy `frm_Menu.java` để mở giao diện chính.
8. Chọn thuật toán cần sử dụng và thực hiện mã hóa, giải mã.

## 9. Kiểm thử chương trình

Các trường hợp kiểm thử bao gồm:

- Mã hóa và giải mã thành công.
- Giải mã bằng khóa không chính xác.
- Kiểm tra khóa không đủ độ dài.
- Kiểm tra quá trình đăng ký và đăng nhập.
- Kiểm tra lưu và mở tệp bản mã.
- Kiểm tra kết nối SQL Server.
- Kiểm tra lịch sử thao tác trong cơ sở dữ liệu.

Đối với RC4, sử dụng bộ dữ liệu kiểm thử:

- Plaintext: `Plaintext`
- Key: `Key`
- Ciphertext mong đợi: `BBF316E8D940AF0AD3`

## Kết luận

Qua bài thực hành LAB 2, sinh viên được tìm hiểu và triển khai các thuật toán mã hóa đối xứng DES, TripleDES, AES, RC4, Twofish và AES-CTR.

Bài thực hành giúp củng cố kiến thức về nguyên lý mã hóa, giải mã, quản lý khóa, IV, Nonce, xây dựng giao diện Java Swing và tích hợp SQL Server để lưu trữ thông tin phục vụ quản lý ứng dụng.

---

**Sinh viên thực hiện:** Phạm Hồng Duy

**MSSV:** 1150070008
