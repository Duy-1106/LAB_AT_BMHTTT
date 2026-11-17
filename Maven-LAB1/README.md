

- **Họ và tên:** Phạm Hồng Duy
- **Mã số sinh viên:** 1150070008
- **Môn học:** An toàn và bảo mật hệ thống thông tin
- **Bài thực hành:** LAB 1 – Mã hóa cổ điển

## Các thuật toán đã thực hiện

| STT | Thuật toán | Chức năng |
|---|---|---|
| 1 | Caesar Cipher | Mã hóa và giải mã bằng phép dịch chuyển ký tự |
| 2 | Vigenère Cipher | Mã hóa và giải mã bằng khóa chữ |
| 3 | Rail Fence Cipher | Mã hóa và giải mã theo hàng rào |
| 4 | Playfair Cipher | Mã hóa và giải mã theo từng cặp ký tự |
| 5 | Transposition Cipher | Mã hóa và giải mã bằng hoán vị |
| 6 | Autokey Cipher | Mã hóa và giải mã bằng khóa tự động mở rộng |

## Công nghệ sử dụng

- **Ngôn ngữ:** Java
- **IDE:** Apache NetBeans
- **Công cụ quản lý dự án:** Maven
- **Giao diện:** Java Swing
- **Cơ sở dữ liệu:** Microsoft SQL Server
- **Công cụ quản lý database:** SQL Server Management Studio (SSMS)
- **Kết nối cơ sở dữ liệu:** JDBC

## Các chức năng chính

Ứng dụng hỗ trợ:

- Mã hóa và giải mã văn bản bằng các thuật toán mật mã cổ điển.
- Nhập văn bản và khóa mã hóa.
- Kiểm tra dữ liệu đầu vào.
- Hiển thị kết quả mã hóa và giải mã.
- Sử dụng giao diện tổng hợp để lựa chọn thuật toán.
- Thực hiện các chức năng phân tích và minh họa tấn công mật mã cổ điển.
- Kết nối Microsoft SQL Server.
- Lưu lịch sử thao tác vào cơ sở dữ liệu.
- Xem lịch sử mã hóa và giải mã.
- Sử dụng Menu chính để mở các giao diện chức năng.

## Cấu trúc chương trình

**LAB1_MaHoaCoDien**

- `pom.xml`: Cấu hình Maven và các thư viện.
- Các lớp xử lý thuật toán Caesar, Vigenère, Rail Fence, Playfair, Transposition và Autokey.
- `frm_TongHop.java`: Giao diện tổng hợp các thuật toán.
- `AttackDemos.java`: Các chức năng minh họa phân tích mật mã.
- `frm_TanCong.java`: Giao diện phân tích và thử nghiệm.
- `frm_KetNoiSQL.java`: Giao diện kết nối SQL Server.
- `frm_LichSu.java`: Giao diện xem lịch sử thao tác.
- `frm_Menu.java`: Giao diện Menu chính.
- Các tệp `.form`: Thiết kế giao diện Java Swing.

## Cơ sở dữ liệu

**Tên database:** `LAB1_MaHoaCoDien`

Bảng chính:

- `dbo.history`: Lưu lịch sử các thao tác mã hóa và giải mã.

Chương trình sử dụng JDBC để kết nối ứng dụng Java với SQL Server.

## Hướng dẫn chạy chương trình

1. Mở Apache NetBeans.
2. Chọn **File → Open Project**.
3. Mở project `LAB1_MaHoaCoDien`.
4. Chờ Maven tải các thư viện cần thiết.
5. Cấu hình kết nối SQL Server.
6. Chọn **Clean and Build** để biên dịch.
7. Chạy `frm_Menu.java`.
8. Chọn thuật toán hoặc chức năng cần thực hiện.

## Kiểm thử chương trình

Các trường hợp kiểm thử bao gồm:

- Mã hóa và giải mã thành công.
- Kiểm tra dữ liệu đầu vào và khóa.
- So sánh kết quả giữa các thuật toán.
- Kiểm tra chức năng giao diện tổng hợp.
- Kiểm tra chức năng phân tích mật mã.
- Kiểm tra kết nối SQL Server.
- Kiểm tra việc lưu và hiển thị lịch sử thao tác.

**Ví dụ kiểm thử Caesar Cipher:**

- Plaintext: `HELLO`
- Key: `3`
- Ciphertext mong đợi: `KHOOR`
- Giải mã kết quả: `HELLO`

## Kết quả đạt được

Sau khi thực hiện LAB 1, sinh viên đã xây dựng ứng dụng Java Swing nhằm minh họa các thuật toán mật mã cổ điển.

Chương trình tích hợp nhiều chức năng trong cùng một ứng dụng, có giao diện thao tác, hỗ trợ mã hóa và giải mã, minh họa phân tích mật mã và kết nối SQL Server để lưu lịch sử.

## Kết luận

Bài thực hành LAB 1 giúp sinh viên hiểu rõ nguyên lý hoạt động của các thuật toán mã hóa cổ điển, cách sử dụng khóa và quá trình chuyển đổi giữa bản rõ và bản mã.

Thông qua bài thực hành, sinh viên cũng rèn luyện kỹ năng lập trình Java, thiết kế giao diện Swing, tổ chức dự án Maven và tích hợp cơ sở dữ liệu SQL Server.

Các thuật toán mật mã cổ điển chủ yếu phục vụ mục đích học tập, không phù hợp để bảo vệ dữ liệu nhạy cảm trong các hệ thống hiện đại.

--
