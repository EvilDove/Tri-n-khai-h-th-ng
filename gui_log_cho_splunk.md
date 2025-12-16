# Triển khai hệ thống
IP của Fortinet firewal: 192.168.0.150

<img width="641" height="572" alt="image" src="https://github.com/user-attachments/assets/8c7283b0-4fef-463f-a0fb-98206554ae0f" />

IP của ubuntu: 192.168.0.16

<img width="734" height="338" alt="image" src="https://github.com/user-attachments/assets/de9f8e0a-c2f9-4ce6-b4ab-856a4cc6a79d" />

IP của win server 2019: 192.168.0.11

<img width="541" height="439" alt="image" src="https://github.com/user-attachments/assets/40a9efcc-f809-4ee2-af20-8ae953bea8d2" />

- Ping thử xem kết nối: 

<img width="570" height="232" alt="image" src="https://github.com/user-attachments/assets/7240af2a-dfb6-4840-8df7-42d7b894cf20" />


- Máy ảo Ubuntu gửi log đến Splunk Server

<img width="678" height="447" alt="image" src="https://github.com/user-attachments/assets/39fd85f3-2f57-4710-b537-101606a70969" />

- Splunk Server nhận log

<img width="1919" height="887" alt="Screenshot 2025-06-09 215402" src="https://github.com/user-attachments/assets/ca72f481-3ac2-4793-9583-07337eb2279e" />

- Giao diện của FortiGate firewall

<img width="1919" height="993" alt="image" src="https://github.com/user-attachments/assets/3f66a96c-3926-475f-a15f-0b503e63a6d4" />

- Trên Splunk_Server và Apache_Server, tạo một user tên splunk để cô lập cài đặt Splunk với quyền tối thiểu.

      useradd -s /bin/bash -d /opt/splunk -m splunk
- Trên máy Splunk_Server, tải Splunk Enterprise từ trang chủ Splunk.
Trên máy Apache_Server, tải Universal Forwarder.

Giải nén các file, cài đặt Splunk và tạo tài khoản để sử dụng.

Để nhận log, thêm data input vào Splunk và cấu hình.

<img width="1919" height="390" alt="398198153-e58b6343-84c4-48c2-9264-2a8d99f23e40" src="https://github.com/user-attachments/assets/6f43c369-19a6-4787-9ac3-1c2807117c2c" />

<img width="1132" height="257" alt="398198173-db30c457-e2dc-4f53-ac9d-ca549a9f9585" src="https://github.com/user-attachments/assets/319e22d8-3ab7-4b90-b7ea-6ac636bed4f5" />

- Để giải quyết hạn chế về việc tài khoản thông thường trong Splunk không có khả năng chuyển tiếp dữ liệu qua các cổng có 3 chữ số, tôi đã thực hiện một giải pháp bằng cách chuyển hướng cổng. Mục đích của việc này là để vượt qua giới hạn về cổng và đảm bảo dữ liệu có thể được chuyển tiếp một cách chính xác đến Splunk.

- Trên máy chủ Apache_Server, tôi đã tiến hành cấu hình để gửi các bản ghi nhật ký (log) đến hệ thống Splunk. Quá trình này bao gồm các bước cụ thể để đảm bảo rằng Apache Server có thể giao tiếp và gửi dữ liệu nhật ký đến Splunk một cách hiệu quả.

- Các bước cụ thể đã được thực hiện như sau:

+ Đầu tiên, tôi tiến hành cài đặt phần mềm Apache2 trên máy chủ. Sau khi cài đặt hoàn tất, tôi kích hoạt Apache2 để đảm bảo nó đang chạy và sẵn sàng ghi lại các sự kiện.

+ Tiếp theo, tôi truy cập vào trang mặc định của Apache Server.

<img width="1556" height="762" alt="398198914-b5cf54b6-ffcf-40d9-bdb1-65cb73f35eec" src="https://github.com/user-attachments/assets/44980c6b-8352-4836-9596-ffa7a8f5e238" />

Tạo traffic truy cập trang để sinh log:

<img width="756" height="393" alt="398199643-94dc84fd-b1e2-4bcd-b435-ea4c942c8e3e" src="https://github.com/user-attachments/assets/0e116587-d6b6-4f80-bbb7-ed9e1b8cb3dc" />
<img width="952" height="42" alt="398199687-5d2d79e5-79f6-4d0a-afa1-fffaf080401c" src="https://github.com/user-attachments/assets/59cbe92e-57b5-499c-ba92-17953c25b92b" />

Các log realtime có thể xem tại file *access.log* trong thư mục log của apache2:

<img width="1436" height="199" alt="398199933-68011c61-e38d-487f-b0ca-f89af40c5316" src="https://github.com/user-attachments/assets/58b4a46f-eebc-489d-a805-2c4d88638842" />

Để phân tích nhật ký bằng Splunk, tôi đã cấu hình hai tệp trên Apache Server
      
      cat /opt/splunkforwarder/etc/system/local/outputs.conf
Và sau đó khởi động lại cấu hình
