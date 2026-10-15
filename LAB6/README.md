1. Mục tiêu

Thực hành cấu hình và kiểm thử các chính sách kiểm soát truy cập mạng bằng pfSense, kết hợp tìm hiểu xác thực Active Directory/LDAP, Captive Portal, Firewall Rules, Alias và Schedule.

2. Môi trường thực hành

pfSense CE: Thiết bị tường lửa, quản lý và kiểm soát truy cập.

Windows Server 2025: Máy chủ Windows và truy cập giao diện quản trị pfSense.

Kali Linux: Máy khách dùng kiểm thử.

Metasploitable 2: Máy chủ web mô phỏng trong DMZ.

Địa chỉ IP sử dụng:

pfSense LAN: 10.6.0.1

pfSense DMZ: 172.16.6.1

Client-A: 10.6.0.21

Client-B: 10.6.0.22

GENERAL_SITE: 172.16.6.10

JOB_SITE: 172.16.6.20

SOCIAL_SITE: 172.16.6.30

RESTRICTED_SITE: 172.16.6.40

DC01: 10.6.0.10

3. Nội dung thực hành

Kịch bản 1 – Chặn Client-A truy cập JOB_SITE

Cấu hình Firewall Rule để chặn Client-A truy cập JOB_SITE, đồng thời cho phép truy cập các website hợp lệ theo chính sách.

Kịch bản 2 – Chặn RESTRICTED_SITE

Sử dụng Firewall Rules và Alias để ngăn cả Client-A và Client-B truy cập RESTRICTED_SITE.

Kịch bản 3 – Truy cập SOCIAL_SITE theo giờ nghỉ

Tạo Schedule LUNCH_WINDOW từ 11:30 đến 13:00, thứ Hai đến thứ Sáu. Cho phép Client-B truy cập SOCIAL_SITE trong khoảng thời gian này và chặn ngoài lịch.

Kịch bản 4 – Chỉ cho phép HTTP/HTTPS trong giờ hành chính

Tạo Alias WEB_PORTS gồm TCP 80 và 443, kết hợp Schedule WORK_HOURS. Cho phép truy cập web trong giờ hành chính và chặn các dịch vụ khác theo chính sách.

Kịch bản 5 – Cô lập DMZ khỏi LAN

Tạo Firewall Rule chặn các kết nối khởi tạo từ DMZ đến LAN, đồng thời duy trì truy cập từ LAN đến các website cần thiết trong DMZ.

4. Các lệnh kiểm thử

Kiểm tra GENERAL_SITE:

curl -I --max-time 5 http://172.16.6.10

Kiểm tra JOB_SITE:

curl -I --max-time 5 http://172.16.6.20

Kiểm tra SOCIAL_SITE:

curl -I --max-time 5 http://172.16.6.30

Kiểm tra RESTRICTED_SITE:

curl -I --max-time 5 http://172.16.6.40

Kiểm tra ICMP:

ping -c 4 172.16.6.10
