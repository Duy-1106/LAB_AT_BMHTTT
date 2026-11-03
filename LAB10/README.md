## Mục tiêu
Mô phỏng Remote DNS Cache Poisoning/Kaminsky trong mạng ảo cô lập, phân biệt với tấn công DNS spoofing tại chỗ, quan sát vai trò của DNS TXID, UDP source port, NS/glue và cache, sau đó đánh giá biện pháp phòng vệ.

## Sơ đồ và địa chỉ

| Thành phần | IP | Mạng / nhiệm vụ |
|---|---|---|
| pfSense DNSLAB | 10.9.0.1/24 | VMnet3 (host-only) |
| DNS Server | 10.9.0.10/24 | BIND9 hoặc vulnerable resolver |
| Victim | 10.9.0.100/24 | Truy vấn DNS |
| pfSense DMZ | 172.16.6.1/24 | LAN Segment `dmz-net` |
| AUTH-DNS/relay (Kali2) | 172.16.6.20/24 | UDP 53/5300 |
| Web hợp lệ | 172.16.6.10 | Đích DNS baseline |
| pfSense ATTACKNET | 10.10.0.1/24 | VMnet4 (host-only) |
| Attacker (Clone of Kali2) | 10.10.0.200/24 | Remote attack simulation |

**Tên miền thử nghiệm:** `www.example.lab10.test`; **DNS giả lập:** `ns.evil.example.lab10.test` → `10.10.0.200`. Các địa chỉ thuộc mạng private, chỉ dùng trong môi trường lab.

## Công cụ
VMware Workstation, pfSense, Kali Linux Live, Python 3, dnspython, BIND9, dig, tcpdump. Script từ tài nguyên LAB 10: `vuln_resolver_lab10.py`, `auth_dns_relay_lab10.py`, `kaminsky_remote_lab10.py`; tài nguyên có `evil_dns_lab10.py` và `fake_index.html`.

## Quy trình đã thực hiện

- Tạo ATTACKNET `10.10.0.0/24`, gán gateway pfSense `10.10.0.1`, tách Attacker khỏi DNSLAB; cho phép DNS (UDP/TCP 53) tới resolver và UDP 5300 tới relay trong lab.
- Chuẩn bị DNS Server `10.9.0.10`, BIND9 và AUTH-DNS `172.16.6.20`.
- Xác minh truy vấn DNS hợp lệ bằng `dig`, trả `www.example.lab10.test A 172.16.6.10`.
- Dừng BIND9 trong pha mô phỏng, chạy vulnerable resolver trên `10.9.0.10:53` với upstream source port **33333**.
- Trên Attacker, chạy `kaminsky_remote_lab10.py`; script kích hoạt truy vấn tên ngẫu nhiên và gửi 16 batch TXID, mỗi batch 4096 giá trị, tới `172.16.6.20:5300`.
- Bắt lưu lượng UDP 5300 trên AUTH-DNS, quan sát `[PENDING]`, `[LEGIT]` và `[HIT]`.
- Chụp ảnh cấu hình, baseline, capture, log và trạng thái phòng vệ cho báo cáo.

## Lệnh kiểm tra (chỉ trên các máy LAB)

```bash
# Victim: baseline DNS
dig @10.9.0.10 www.example.lab10.test +time=7 +tries=1

# DNS Server: xác minh chương trình lắng nghe UDP 53
sudo ss -lunp | grep ':53'

# AUTH-DNS: quan sát các gói tin mô phỏng vào race relay
sudo tcpdump -ni eth0 'udp dst port 5300'

# Attacker: kiểm tra DNS được trả về
dig @10.9.0.10 www.example.lab10.test +short
```

## Kết quả quan sát và giới hạn

- **Baseline:** Victim và Attacker truy vấn thành công, IP hợp lệ `172.16.6.10`; `status: NOERROR`.
- **Mạng:** Attacker `10.10.0.200` truy cập pfSense `10.10.0.1`; các UDP packet tới relay `172.16.6.20:5300` được tcpdump ghi nhận.
- **Race:** AUTH-DNS ghi `[PENDING]` và `[HIT] batch 12288-16383 contains txid=14830`, forged delegation đến `ns.evil.example.lab10.test` / `10.10.0.200`.
- **Chưa xác nhận:** Không có bằng chứng `[CACHE]` và truy vấn Victim sau poison trả `10.10.0.200` trong hồ sơ đã cung cấp. **Không được diễn giải `[HIT]` thành cache poisoning thành công.**
- **Phòng vệ:** Có ảnh trạng thái phòng vệ và cấu hình baseline BIND9, nhưng chưa xác minh đầy đủ phân giải sau restore và source-port randomization qua capture.

## Khôi phục, hardening và dọn lab

Trên DNS Server, dừng chương trình mô phỏng (Ctrl+C trong Terminal chạy resolver), khởi động lại BIND9:

```bash
sudo systemctl start named
sudo systemctl status named --no-pager
```

Giới hạn recursion cho DNSLAB, bật DNSSEC validation phù hợp, duy trì source-port randomization; không cho ATTACKNET dùng recursion như một open resolver. Disable/xóa rule UDP 5300 khi kết thúc bài. Riêng zone `.test` có `validate-except` trong cấu hình thử nghiệm, không áp dụng ngoại lệ tương tự bừa bãi ở production.


## Kết luận

Đã dựng môi trường thực nghiệm, xác minh phân giải DNS hợp lệ, quan sát gói tin gửi đến race relay và ghi nhận TXID `[HIT]`. Chưa có dữ liệu đủ để xác nhận resolver đã cache malicious delegation hoặc Victim bị chuyển hướng sau poison.

