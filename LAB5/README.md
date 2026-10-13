# LAB 5 – CẤU HÌNH VÀ KIỂM TRA FIREWALL

**Sinh viên:** Phạm Hồng Duy  
**MSSV:** 1150070008  
**Tài liệu minh chứng:** `11TTMT-LAB5_PhạmHồngDuy_1150070008.docx`

## 1. Giới thiệu

Bài thực hành LAB 5 sử dụng giao diện quản trị **pfSense Firewall** để thiết lập các quy tắc kiểm soát lưu lượng mạng và kiểm tra tác động của chúng trên các máy ảo. Nội dung báo cáo gồm ba tình huống:

1. Chặn ICMP nhưng vẫn cho phép Web/DNS.
2. Chỉ cho phép một host cụ thể truy cập Internet.
3. Cô lập mạng DMZ khỏi mạng LAN.

## 2. Môi trường thực hành

Các thành phần xuất hiện trong tài liệu:

| Thành phần | Vai trò / thông tin |
|---|---|
| VMware Workstation | Môi trường chạy máy ảo |
| pfSense | Cấu hình quy tắc firewall trên giao diện quản trị |
| Windows Server | Máy kiểm tra trong mạng, IP `10.0.0.2` ở tình huống 2 |
| Kali Linux | Máy kiểm tra, IP `10.0.0.3` ở tình huống 2 |
| `8.8.8.8` | Địa chỉ IP đích dùng để thử kết nối |

> Tài liệu không nêu đầy đủ phiên bản phần mềm, sơ đồ mạng, địa chỉ các interface hoặc cấu hình chi tiết từng rule; README không tự bổ sung các thông số đó.

## 3. Nội dung thực hành

### Tình huống 1 – Chặn ICMP, cho phép Web/DNS

**Mục tiêu:** Giới hạn lưu lượng ICMP từ LAN trong khi vẫn cho phép các dịch vụ Web và DNS cần thiết.

**Thao tác được ghi trong báo cáo:**

1. Truy cập **Firewall → Rules → LAN** trên pfSense.
2. Disable rule **LAN to Internet** đang có.
3. Tạo **3 rule** theo cấu hình minh họa trong ảnh báo cáo.
4. Sử dụng lệnh `ping 8.8.8.8` để kiểm tra ICMP.
5. Mở PowerShell trên máy Windows để kiểm tra bổ sung.

**Minh chứng:** Hình ảnh cấu hình và các cửa sổ kiểm tra ở trang 1–2 của file Word. Báo cáo có ảnh thao tác nhưng không diễn giải rõ bằng văn bản kết quả kiểm thử Web/DNS, vì vậy không khẳng định mọi phép kiểm thử đều đạt.

### Tình huống 2 – Chỉ một host được ra Internet

**Mục tiêu:** Cho phép Windows Server `10.0.0.2` kết nối Internet, đồng thời giới hạn Kali Linux `10.0.0.3`.

**Thao tác được ghi trong báo cáo:**

1. Tạo rule trên pfSense theo ảnh minh họa ở trang 3.
2. Từ Windows Server `10.0.0.2`, chạy `ping 8.8.8.8`.
3. Từ Kali Linux `10.0.0.3`, chạy `ping 8.8.8.8`.
4. Đối chiếu kết quả từ hai máy.

**Kết quả ghi nhận trong báo cáo:**

| Máy | Địa chỉ IP | Kiểm tra | Kết quả |
|---|---|---|---|
| Windows Server | `10.0.0.2` | Ping `8.8.8.8` | Thành công |
| Kali Linux | `10.0.0.3` | Ping `8.8.8.8` | Thất bại |

**Lưu ý:** Phép ping chứng minh sự khác biệt về lưu lượng ICMP tới địa chỉ kiểm tra; để kết luận đầy đủ về khả năng truy cập Internet qua HTTP/HTTPS/DNS cần kiểm tra thêm các giao thức tương ứng.

### Tình huống 3 – Cô lập DMZ khỏi LAN

**Mục tiêu:** Ngăn kết nối trái phép từ vùng mạng DMZ vào LAN theo chính sách firewall.

Báo cáo hiện có tiêu đề tình huống này ở **trang 4**, nhưng chưa cung cấp các bước cấu hình, danh sách rule hoặc kết quả kiểm tra cụ thể. Do đó, trạng thái hoàn thành tình huống 3 **chưa thể xác nhận từ tài liệu đính kèm**.

## 4. Cách xem và đối chiếu kết quả

1. Mở `11TTMT-LAB5_PhạmHồngDuy_1150070008.docx`.
2. Xem **trang 1–2**: hình ảnh thao tác chặn ICMP, tạo 3 rule và thử lệnh kiểm tra.
3. Xem **trang 3–4**: ảnh tạo rule và thử ping từ Windows Server/Kali Linux.
4. Đối chiếu kết quả hiển thị trên các máy ảo với bảng ở tình huống 2.
5. Nếu cần báo cáo hoàn chỉnh cho tình huống 3, bổ sung ảnh rule DMZ/LAN và ảnh thử kết nối theo cả chiều được phép/chặn.

## 5. Kết luận

Bài LAB 5 minh họa cách sử dụng rule của pfSense để kiểm soát lưu lượng theo **giao thức** và **máy nguồn**. Tình huống 2 có kết quả kiểm tra ping được báo cáo rõ ràng: `10.0.0.2` thành công, `10.0.0.3` thất bại. Tình huống 1 có minh chứng bằng ảnh thao tác; tình huống 3 mới có tiêu đề và cần bổ sung minh chứng để đánh giá đầy đủ.

## 6. Tài liệu tham khảo nội bộ

- Báo cáo thực hành: `11TTMT-LAB5_PhạmHồngDuy_1150070008.docx` (4 trang, ảnh chụp môi trường thực hành và phần mô tả thao tác).
