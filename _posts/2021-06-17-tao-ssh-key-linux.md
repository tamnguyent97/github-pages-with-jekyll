---
title: "Tao SSH Key Linux"
date: 2021-06-17
---

<!-- wp:paragraph -->
<p>Trước đây mình có hướng dẫn bạn cách tạo SSH key VPS trên hệ điều hành Windows, nay mình sẽ tiếp tục hướng dẫn các bạn thực hiện tạo SSH key cho hệ điều hành Linux.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 1: Tạo Key</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Đầu tiên bạn mở Terminal lên, thường sẽ có sẵn trên hệ điều hành Linux. Bạn nhập như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:verse -->
<pre class="wp-block-verse">ssh-keygen</pre>
<!-- /wp:verse -->

<!-- wp:paragraph -->
<p>Sau đó ssh-keygen sẽ tạo ra và kết quả của lệnh trên sẽ như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Generating public/private rsa key pair.<br>Enter file in which to save the key (/home/user/.ssh/id_rsa): </pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Bạn sẽ cần nhập đường dẫn lưu key, tên key. Nếu không thì key sẽ được lưu theo đường dẫn và tên file mặc định. Lời khuyên của mình là nên đặt tên để dễ phân biệt nếu bạn có tạo nhiều key cho nhiều VPS. Ví dụ ở dòng này mình sẽ nhập như sau: <strong>home/.ssh/key_vps.pub</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Tiếp theo, bạn sẽ được hỏi nhập passphrase, và bạn sẽ cần nhập 2 lần để xác thực, hoặc nhấn Enter hai lần để bỏ trống.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Enter passphrase (empty for no passphrase):<br>Enter same passphrase again:</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Và cuối cùng cũng đã hoàn thành, bạn sẽ có output như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Your identification has been saved in /home/.ssh/key_vps
Your public key has been saved in /home/.ssh/key_vps.pub
The key fingerprint is:
SHA256:6I7xW6mDYRcTLU5XHQncFssTocqmuwlQCokvwUEbkZE thanhtam@thanhtam
The key's randomart image is:
+---[RSA 3072]----+
|.   <em>= . o o+==   | </em>
<em>|o  E+  + o  .o=o | </em>
<em>|= o  .o   +  ..+ | </em>
<em>| +  o  + o  .  . | </em>
<em>|. +    . o  S    | </em>
<em>| . .o.   .o   .  | </em>
<em>| .o  + o     o   | </em>
<em>|   .</em>  .  =       |
| .   O      +    |
+----[SHA256]-----+</pre>
<!-- /wp:preformatted -->

<!-- wp:heading -->
<h2>Bước 2: Nhập key lên VPS.</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn thực hiện tạo thư mục chứa file key và gán quyền như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">mkdir ~/.ssh
touch ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Sau đó mở file authorized_keys và nhập public key được tạo ra ở bước 1 vào:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">vi ~/.ssh/authorized_keys</pre>
<!-- /wp:preformatted -->

<!-- wp:heading -->
<h2>Bước 3: Kiểm tra đăng nhập</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn dùng Terminal và nhập lệnh SSH vào VPS để kiểm tra lại thử nhé:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>ssh root@123.123.123.123 -p 1234<br>The authenticity of host '[123.123.123.123]:1234 ([123.123.123.123]:1234)' can't be established.<br>ECDSA key fingerprint is SHA256:v2D9JCGHw0Jtb7NMPGJHidypftdr8LNW+gZ3sSpT3sQ.<br>Are you sure you want to continue connecting (yes/no/[fingerprint])? yes<br>Warning: Permanently added '[123.123.123.123]:1234' (ECDSA) to the list of known hosts.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>root@123.123.123.123's password:</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 4: Tắt đăng nhập bằng mật khẩu</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Sửa file sshd_config bằng lệnh: <strong>vi /etc/ssh/sshd_config</strong> và thay đổi tham số sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">PasswordAuthentication no</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Cuối cùng bạn khởi động lại service ssh để nhận được cấu hình mới nhé.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">service sshd restart</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Chúc các bạn thành công.</p>
<!-- /wp:paragraph -->
