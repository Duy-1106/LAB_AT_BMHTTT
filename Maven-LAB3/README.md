LAB 3 – MÃ HÓA KHÓA CÔNG KHAI
Sinh viên: Phạm Hồng Duy
MSSV: 1150070008
Công nghệ: Java 17, Maven, Apache NetBeans, Microsoft SQL Server
Nội dung thực hành và minh chứng
Bài 3.1 – RSA (chạy Console) và chuẩn bị môi trường
- Thiết lập project Maven trong NetBeans, kiểm tra quá trình Build.
- Chuẩn bị cơ sở dữ liệu SQL Server và tài khoản truy cập phục vụ ghi lịch sử.
- Thử kết nối SQL Server qua giao diện frm_KetNoiSQL.
- Chạy chương trình RSA Console (RSADemo.java), minh họa RSA với độ dài khóa 2048 và 3072 bit.
Bài 3.2 – RSA (giao diện Swing)
- Xây dựng form frm_RSA.java.
- Tạo cặp khóa RSA, mã hóa và giải mã bản rõ ngắn.
- Minh họa RSA-2048 và RSA-3072 trên giao diện.
Dữ liệu kiểm thử: HELLO RSA.
Bài 3.3 – ECC
- Xây dựng form frm_ECC.java cho mã hóa dựa trên mật mã đường cong elliptic.
- Tạo cặp khóa, mã hóa và giải mã thông điệp.
- Sử dụng các tiện ích mật mã và AES-GCM trong chương trình.
Dữ liệu kiểm thử: HELLO ECC.
Bài 3.4 – Hệ mã lai RSA + AES-GCM
- Xây dựng form frm_RSA_AES.java.
- Kết hợp RSA để bảo vệ khóa AES và AES-GCM để mã hóa dữ liệu.
- Hỗ trợ kiểm thử văn bản dài và phát hiện trường hợp bản mã bị chỉnh sửa.
Dữ liệu kiểm thử theo hướng dẫn LAB: Văn bản dài trên 1.000 ký tự.
Bài 3.5 – Bài tập nâng cao: Chữ ký số ECDSA
- Xây dựng lớp ECCSignature.java và form frm_ECC_Signature.java.
- Tạo cặp khóa ECDSA, dùng khóa riêng để Sign, dùng khóa công khai để Verify.
- Kiểm tra tính toàn vẹn thông điệp thông qua kết quả VALID hoặc INVALID.
Dữ liệu kiểm thử:
Thao tác	Thông điệp	Kết quả mong đợi
Generate Keys → Sign → Verify	THONG DIEP A	VALID
Đổi nội dung, giữ nguyên chữ ký → Verify	THONG DIEP B	INVALID
3. Cấu trúc project
LAB3_MaHoaKhoaCongKhai/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── week_03/
                ├── CryptoSupport.java
                ├── FileTextIO.java
                ├── DbConfig.java
                ├── HistoryDao.java
                ├── RSACipher.java
                ├── RSADemo.java
                ├── ECCCipher.java
                ├── ECCSignature.java
                ├── RSA_AES_Cipher.java
                ├── frm_KetNoiSQL.java
                ├── frm_LichSu.java
                ├── frm_RSA.java
                ├── frm_ECC.java
                ├── frm_RSA_AES.java
                └── frm_ECC_Signature.java
4. Yêu cầu môi trường
- JDK 17 hoặc phiên bản tương thích.
- Apache NetBeans và Maven.
- Microsoft SQL Server Express cùng SQL Server Management Studio (SSMS).
- Microsoft JDBC Driver qua dependency Maven (mssql-jdbc).
