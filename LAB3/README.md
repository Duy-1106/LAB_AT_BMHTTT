
TH1 – Baseline & Risk Register
Phân biệt Asset, Vulnerability, Threat, Risk và Attack.
Phân loại 5 nhóm nguồn đe dọa:
Hành động vô ý
Hành động cố ý
Thảm họa tự nhiên
Lỗi kỹ thuật
Lỗi quản lý
Xây dựng risk register cho các tài sản và nguy cơ trong hệ thống.
TH2 – Malware / EICAR
Kiểm tra Microsoft Defender và Real-time Protection.
Tạo EICAR test file để kiểm tra khả năng phát hiện mã độc.
Xác nhận Defender phát hiện/quarantine mẫu EICAR.
Kiểm tra bằng Protection History và Get-MpThreatDetection.
TH3 – Password Attack / Keylogging
Bật Audit Logon Success/Failure.
Tạo tài khoản thử nghiệm lab3user.
Tạo các lần đăng nhập đúng và sai.
Kiểm tra các Event ID:
4624: đăng nhập thành công
4625: đăng nhập thất bại
4648: sử dụng explicit credentials
Đổi mật khẩu và xác minh mật khẩu cũ không còn sử dụng được.
Phân tích nguy cơ keylogging và biện pháp giảm thiểu bằng endpoint protection, MFA/passkey và credential rotation.
TH4 – Persistence / Backdoor Detection
Cài và cấu hình Sysmon.
Kiểm tra Sysmon Event ID 1 khi chạy Notepad.
Tạo hai persistence lành tính:
LAB3_Run_Demo
LAB3_Persistence_Demo
Xác minh persistence bằng Sysmon và Autoruns.
Chạy HTTP server chỉ trên localhost:
python -m http.server 8080 --bind 127.0.0.1
Kiểm tra listener bằng Get-NetTCPConnection.
Dùng Process Explorer đối chiếu PID và tiến trình python.exe.
Xác nhận cổng 8080 chỉ bind trên 127.0.0.1.
TH5 – Sniffing HTTP vs HTTPS
Dùng Wireshark capture traffic loopback.
Tạo HTTP request:
curl.exe "http://127.0.0.1:8080/?lab_user=lab3_student&lab_code=TRAINING_ONLY"
Quan sát được URL HTTP ở dạng plaintext trong Wireshark.
So sánh với HTTPS/TLS port 443:
vẫn thấy IP, port, thời gian, kích thước packet
không thấy trực tiếp nội dung URL plaintext như HTTP
Qua đó thấy được sự khác biệt giữa HTTP và HTTPS về bảo vệ nội dung truyền tải.
TH6 – DoS / DDoS / Mail Bombing
Chạy local load test giới hạn trên:
127.0.0.1:8080
Script sử dụng:
50 request
5 worker
Phân tích ddos_sample.csv theo SourceIP.
Nhận biết DDoS có nhiều nguồn phân tán, khác với DoS thường có ít nguồn hơn.
Phân tích mailbomb_sample.csv theo:
số lượng email theo sender
tổng dung lượng
dung lượng trung bình
Không thực hiện DDoS thật và không gửi email hàng loạt.
TH7 – Social Engineering / Phishing
Phân tích mẫu phishing_email.txt.
Nhận diện các dấu hiệu phishing:
tạo cảm giác khẩn cấp
display name có vẻ đáng tin
domain cần xác minh
Reply-To khác From
yêu cầu truy cập link hoặc cung cấp thông tin xác thực
Phân loại các tình huống:
SE01: Phishing
SE02: Spear Phishing
SE03: Pretexting
SE04: Baiting
SE05: Quid Pro Quo
SE06: Watering Hole
Công cụ sử dụng
Windows Server 2022
Microsoft Defender
Event Viewer
PowerShell
Sysmon
Autoruns
Process Explorer
Wireshark
Python
VMware Workstation
Cleanup và Recovery
Xóa LAB3_Run_Demo.
Xóa LAB3_Persistence_Demo.
Dừng HTTP listener trên port 8080.
Xóa tài khoản lab3user.
Kiểm tra Microsoft Defender vẫn hoạt động.
Tính SHA-256 cho các file trong thư mục Evidence.
Xác minh hệ thống không còn artefact thử nghiệm của LAB.
Kết luận

Qua LAB 3, đã thực hành quy trình:

Baseline → Observe → Detect → Contain → Recover → Verify

Nội dung bao gồm nhận diện malware, tấn công mật khẩu, persistence/backdoor, sniffing, HTTP/HTTPS, DoS/DDoS, mail bombing và social engineering/phishing trong môi trường VM an toàn.
