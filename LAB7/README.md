Bài thực hành triển khai hệ thống bảo vệ truy cập Web trên môi trường VMware Workstation, sử dụng pfSense làm Firewall, Squid làm Proxy Server, E2Guardian để lọc website và ClamAV để kiểm tra mã độc.

Hệ thống gồm pfSense có địa chỉ LAN 10.6.0.1, Windows Server 2025 địa chỉ 10.6.0.10, Kali Linux Client-A địa chỉ 10.6.0.22 và máy Proxy Linux địa chỉ 10.6.0.30. Proxy sử dụng cổng 8080 cho E2Guardian và cổng 3128 cho Squid.

Quá trình thực hành đã tiến hành cài đặt Squid, E2Guardian và cấu hình kết nối mạng giữa các máy ảo. Firewall pfSense được sử dụng để quản lý lưu lượng truy cập, kết hợp Proxy nhằm kiểm soát các yêu cầu HTTP từ máy Client.

Trên Proxy Server, Squid được cấu hình cho phép mạng 10.6.0.0/24 sử dụng dịch vụ. E2Guardian được thiết lập để kiểm tra và chặn các website nằm trong danh sách cấm.

Việc kiểm thử được thực hiện từ Kali Linux thông qua Proxy 10.6.0.30:8080. Website example.com được đưa vào danh sách chặn để kiểm tra hoạt động của E2Guardian.

Kết quả kiểm thử cho thấy E2Guardian trả về trang Access Denied khi Client truy cập website bị chặn. Điều này chứng minh chức năng Hard Block đã hoạt động thành công.

Hệ thống cũng ghi nhận các yêu cầu truy cập trong file /var/log/e2guardian/access.log. Log thể hiện địa chỉ Client 10.6.0.22, website example.com và trạng thái DENIED, giúp xác nhận chính sách chặn đã được áp dụng.

Các lệnh kiểm tra được sử dụng trong quá trình thực hành:

sudo systemctl status squid
sudo systemctl status e2guardian
sudo ss -lntp | grep -E '3128|8080'
ping -c 4 10.6.0.30
curl -i -x http://10.6.0.30:8080 http://example.com/
sudo tail -n 10 /var/log/e2guardian/access.log

Ngoài chức năng Hard Block, bài thực hành còn tìm hiểu các cơ chế Warning, Temporary Bypass, Schedule, Antivirus và HTTPS Inspection. Các chức năng này cần có kết quả kiểm thử và minh chứng riêng để xác nhận mức độ hoàn thành.

Qua bài thực hành, đã triển khai và kiểm thử thành công chức năng lọc website bằng Squid và E2Guardian kết hợp với pfSense Firewall. Hệ thống có khả năng kiểm soát truy cập Web, chặn website theo chính sách và ghi nhận log phục vụ công tác giám sát an toàn mạng.

Bài LAB giúp củng cố kiến thức về Firewall, Web Proxy, quản lý truy cập Internet và các phương pháp bảo vệ hệ thống mạng trong môi trường thực tế.
