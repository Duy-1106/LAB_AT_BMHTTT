Nội dung đã thực hiện

Thiết lập môi trường thực hành

Sử dụng VMware Workstation để xây dựng môi trường mạng ảo.

Tạo mạng riêng DNS-LAB bằng VMnet3 (Host-only).

Cấu hình mạng 10.9.0.0/24, subnet mask 255.255.255.0.

Tắt DHCP trên VMnet3 và sử dụng địa chỉ IP tĩnh.

Cấu hình pfSense để quản lý và kiểm soát lưu lượng mạng.

Kiểm tra kết nối giữa các máy ảo.

Cấu hình DNS Server bằng BIND9

Tạo máy ảo LAB8_DNS_SERVER sử dụng Kali Linux.

Đặt địa chỉ IP tĩnh 10.9.0.10/24.

Cài đặt dịch vụ BIND9.

Cấu hình các tệp named.conf.options và named.conf.local.

Tạo DNS Zone lab8.test.

Tạo bản ghi DNS cho tên miền www.lab8.test trỏ đến địa chỉ 10.9.0.100.

Kiểm tra cấu hình bằng named-checkconf và named-checkzone.

Khởi động dịch vụ BIND9 bằng systemctl.

Kiểm tra phân giải tên miền bằng công cụ dig.

Kết quả: DNS Server hoạt động và phân giải thành công www.lab8.test thành địa chỉ 10.9.0.100.

Cấu hình máy Victim

Tạo máy ảo LAB8_VICTIM sử dụng Kali Linux.

Kết nối máy Victim vào mạng VMnet3.

Thiết lập IP tĩnh 10.9.0.100/24.

Cấu hình DNS Server là 10.9.0.10.

Kiểm tra kết nối đến pfSense và DNS Server.

Kiểm tra khả năng phân giải tên miền trong mạng DNS-LAB.

Khắc phục sự cố kết nối mạng do trùng địa chỉ IP trên mạng ảo.

Kết quả: Máy Victim kết nối thành công đến DNS Server và có thể thực hiện truy vấn DNS.

Cấu hình máy Attacker

Sử dụng máy Clone of Kali2 làm máy Attacker.

Kết nối máy Attacker vào mạng VMnet3.

Thiết lập IP tĩnh 10.9.0.200/24.

Kiểm tra kết nối đến DNS Server 10.9.0.10.

Kiểm tra kết nối đến Victim 10.9.0.100.

Sử dụng công cụ dig để kiểm tra bản ghi DNS.

Kết quả: Máy Attacker kết nối thành công đến DNS Server và Victim, tỷ lệ mất gói tin khi kiểm tra ping là 0%.

Giám sát lưu lượng DNS bằng tcpdump

Sử dụng công cụ tcpdump trên Kali Linux.

Theo dõi lưu lượng DNS qua cổng 53.

Thực hiện truy vấn tên miền www.lab8.test từ máy Victim.

Quan sát gói DNS Query gửi đến DNS Server.

Quan sát gói DNS Response trả về từ DNS Server.

Xác định địa chỉ IP nguồn, địa chỉ IP đích và nội dung phản hồi DNS.

Kết quả: Công cụ tcpdump bắt được gói truy vấn và phản hồi DNS. DNS Server trả về bản ghi A của www.lab8.test với địa chỉ 10.9.0.100.

Nội dung kiểm thử tiếp theo

Mô phỏng DNS Spoofing trong môi trường mạng ảo.

Kiểm tra sự thay đổi kết quả phân giải DNS.

Nghiên cứu và mô phỏng DNS Cache Poisoning.

Phân tích kết quả và các biện pháp phòng chống.

Các nội dung này đang trong quá trình chuẩn bị kiểm thử, chưa được xác nhận hoàn thành.

Công cụ sử dụng

VMware Workstation

Kali Linux

pfSense Firewall

BIND9 DNS Server

dig

tcpdump

ping

arping

nmcli

Kết quả đạt được

Xây dựng thành công môi trường DNS-LAB.

Cấu hình hệ thống DNS Server bằng BIND9.

Thiết lập kết nối giữa DNS Server, Victim và Attacker.

Phân giải thành công tên miền www.lab8.test.

Giám sát được lưu lượng truy vấn và phản hồi DNS bằng tcpdump.

Khắc phục các lỗi kết nối mạng trong quá trình thực hành.

Kết luận

Qua quá trình thực hành LAB 8, em đã xây dựng được môi trường mạng riêng phục vụ kiểm thử DNS, cấu hình DNS Server bằng BIND9 và kiểm tra khả năng phân giải tên miền.

Bên cạnh đó, em đã thực hiện cấu hình các máy Victim, Attacker và sử dụng công cụ tcpdump để giám sát quá trình trao đổi dữ liệu DNS.

Bài thực hành giúp em hiểu rõ hơn về nguyên lý hoạt động của hệ thống DNS, quá trình truy vấn và phản hồi DNS, đồng thời tạo nền tảng để tiếp tục nghiên cứu các nguy cơ DNS Spoofing và DNS Cache Poisoning cũng như các biện pháp bảo vệ hệ thống DNS.
