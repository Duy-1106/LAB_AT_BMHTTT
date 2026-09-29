LAB4 - Nmap

1. Môi Trường Thực Hành

Công cụ ảo hóa: VMware Workstation.

Máy quét (Attacker): Kali Linux.

Máy đích (Target): Metasploitable 2.

Dải mạng nội bộ: 192.168.154.0/24.

2. Các Bước Thực Hiện Chụp Ảnh Minh Chứng

Bước 1: Kiểm tra địa chỉ IP máy Kali Linux (Ảnh 1)

Mở Terminal trên máy Kali Linux.

Gõ lệnh:

ip -br addr

Ghi nhận IP của giao diện mạng (ví dụ eth0) là 192.168.154.129.

Bước 2: Kiểm tra địa chỉ IP máy Metasploitable 2 (Ảnh 2)

Đăng nhập vào máy ảo Metasploitable 2.

Gõ lệnh:

ifconfig

Ghi nhận IP hiển thị ở phần eth0 là 192.168.154.128.

Bước 3: Phát hiện các host đang hoạt động (Ảnh 3)

Từ máy Kali, kiểm tra kết nối tới máy đích bằng lệnh:

ping -c 4 192.168.154.128

Tiến hành quét dò tìm các thiết bị trong mạng bằng lệnh:

sudo nmap -sn 192.168.154.0/24

Dữ liệu thu được:

192.168.154.128: Máy đích Metasploitable 2.

192.168.154.1: Card mạng ảo (VMnet) trên máy thật.

192.168.154.254: Dịch vụ DHCP/NAT của VMware.

Bước 4: Khảo sát cổng TCP (Ảnh 4)

Sử dụng kỹ thuật SYN scan để quét các cổng TCP trên máy đích:

sudo nmap -sS 192.168.154.128

Dữ liệu thu được: Phát hiện 23 cổng đang mở (open) và 977 cổng đóng (closed).

Bước 5: Nhận diện phiên bản dịch vụ (Ảnh 5)

Quét chi tiết phiên bản các phần mềm đang chạy trên các cổng mở bằng lệnh:

sudo nmap -sV 192.168.154.128

Dữ liệu thu được (ví dụ):

Cổng 21 (ftp): vsftpd 2.3.4.

Cổng 22 (ssh): OpenSSH 4.7p1.

Cổng 80 (http): Apache httpd 2.2.8.

Cổng 445 (smb): Samba smbd 3.X - 4.X.

Bước 6: Nhận diện hệ điều hành (Ảnh 6)

Tiến hành dự đoán hệ điều hành của máy đích bằng lệnh:

sudo nmap -O 192.168.154.128

Lệnh này sẽ trả về các thông tin chi tiết về Linux kernel đang chạy.

Bước 7: Quét lỗ hổng bằng Nmap Scripting Engine (Ảnh 7)

Kiểm tra xem mục tiêu có dính lỗ hổng MS17-010 hay không bằng lệnh:

sudo nmap -p 445 --script smb-vuln-ms17-010 192.168.154.128

Kết luận: Nmap chỉ báo cổng 445 mở, không có cảnh báo VULNERABLE. Do mục tiêu chạy Linux/Samba nên không bị ảnh hưởng bởi lỗ hổng Windows này.

Bước 8: Xuất kết quả ra file (Ảnh 8)

Thực hiện quét tổng hợp và lưu kết quả vào file văn bản bằng lệnh:

sudo nmap -sV -O 192.168.154.128 -oN ket_qua.txt

Kiểm tra lại xem file đã được tạo chưa bằng lệnh:

ls

3. Trả Lời Các Câu Hỏi Phân Tích Lý Thuyết

1. Phân biệt trạng thái cổng

Open: Có ứng dụng/dịch vụ đang lắng nghe.

Closed: Có thể truy cập nhưng không có dịch vụ lắng nghe.

Filtered: Bị tường lửa hoặc cơ chế lọc gói tin chặn nên Nmap không xác định được trạng thái chính xác.

2. Quyền của lệnh -sS

Lệnh -sS cần quyền root để can thiệp vào Raw Sockets và tạo gói tin RST đột ngột, khác với -sT sử dụng hàm connect() tiêu chuẩn.

3. Lỗi quét FIN/Xmas/NULL

Kết quả có thể sai lệch vì nhiều hệ điều hành không tuân thủ chuẩn RFC 793 hoặc do tường lửa chặn các gói tin.

4. Chức năng ACK scan

ACK scan dùng để xác định bộ luật của tường lửa, cụ thể là cổng có bị lọc hay không; không dùng để tìm cổng mở.

5. Vì sao UDP scan chậm?

UDP không có cơ chế bắt tay. Khi không có phản hồi, Nmap phải gửi lại nhiều lần và có thể báo trạng thái open|filtered.

6. Vai trò của -sV

-sV dùng để trích xuất tên và phiên bản phần mềm đang chạy, ví dụ Apache 2.2.8, từ đó hỗ trợ tra cứu chính xác mã lỗ hổng (CVE).

7. Giới hạn của -O

Nhận diện hệ điều hành có thể bị sai lệch nếu đi qua tường lửa, proxy, load balancer hoặc khi quản trị viên cố tình chỉnh sửa TCP/IP stack.

8. Ý nghĩa của Timeout

Timeout không đồng nghĩa với hệ thống an toàn. Nguyên nhân có thể là mạng kém hoặc hệ thống phòng thủ ngắt kết nối.

9. Dấu hiệu Hardening

Một dấu hiệu có thể quan sát là cổng chuyển từ trạng thái open sang filtered (bị chặn) hoặc closed (đã tắt dịch vụ).

10. Biện pháp phòng thủ

Đóng các dịch vụ không cần thiết.

Quản lý truy cập bằng tường lửa.

Cập nhật phần mềm thường xuyên.
