---
title: "Tao SSH Key Linux"
date: 2021-06-17
---

Bước 1: Tạo Key
Đầu tiên bạn mở Terminal lên, thường sẽ có sẵn trên hệ điều hành Linux. Bạn nhập như sau:

ssh-keygen
Sau đó ssh-keygen sẽ tạo ra và kết quả của lệnh trên sẽ như sau:

Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): 
Bạn sẽ cần nhập đường dẫn lưu key, tên key. Nếu không thì key sẽ được lưu theo đường dẫn và tên file mặc định. Lời khuyên của mình là nên đặt tên để dễ phân biệt nếu bạn có tạo nhiều key cho nhiều VPS. Ví dụ ở dòng này mình sẽ nhập như sau: home/.ssh/key_vps.pub

Tiếp theo, bạn sẽ được hỏi nhập passphrase, và bạn sẽ cần nhập 2 lần để xác thực, hoặc nhấn Enter hai lần để bỏ trống.

Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Và cuối cùng cũng đã hoàn thành, bạn sẽ có output như sau:

Your identification has been saved in /home/.ssh/key_vps
Your public key has been saved in /home/.ssh/key_vps.pub
The key fingerprint is:
SHA256:6I7xW6mDYRcTLU5XHQncFssTocqmuwlQCokvwUEbkZE thanhtam@thanhtam
The key's randomart image is:
+---[RSA 3072]----+
|.   = . o o+==   | 
|o  E+  + o  .o=o | 
|= o  .o   +  ..+ | 
| +  o  + o  .  . | 
|. +    . o  S    | 
| . .o.   .o   .  | 
| .o  + o     o   | 
|   .  .  =       |
| .   O      +    |
+----[SHA256]-----+
Bước 2: Nhập key lên VPS.
Bạn thực hiện tạo thư mục chứa file key và gán quyền như sau:

mkdir ~/.ssh
touch ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
Sau đó mở file authorized_keys và nhập public key được tạo ra ở bước 1 vào:

vi ~/.ssh/authorized_keys
Bước 3: Kiểm tra đăng nhập
Bạn dùng Terminal và nhập lệnh SSH vào VPS để kiểm tra lại thử nhé:

ssh root@123.123.123.123 -p 1234
The authenticity of host ‘[123.123.123.123]:1234 ([123.123.123.123]:1234)’ can’t be established.
ECDSA key fingerprint is SHA256:v2D9JCGHw0Jtb7NMPGJHidypftdr8LNW+gZ3sSpT3sQ.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added ‘[123.123.123.123]:1234’ (ECDSA) to the list of known hosts.

root@123.123.123.123’s password:

Bước 4: Tắt đăng nhập bằng mật khẩu
Sửa file sshd_config bằng lệnh: vi /etc/ssh/sshd_config và thay đổi tham số sau:

PasswordAuthentication no
Cuối cùng bạn khởi động lại service ssh để nhận được cấu hình mới nhé.

service sshd restart
Chúc các bạn thành công.
