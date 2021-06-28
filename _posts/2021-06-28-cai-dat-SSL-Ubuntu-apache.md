---
title: "Cài đặt chứng chỉ SSL lên máy chủ Ubuntu sử dụng webserver Apache"
date: 2021-06-28
---
<!-- wp:paragraph -->
<p>Trước đây mình có hướng dẫn về cài đặt SSL cho webserver Apache trên CentOS, vậy còn cài đặt trên Ubuntu thì sẽ như thế nào, cùng mình tìm hiểu nhé.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Bài viết cũ bạn có thể xem:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a aria-label="Cài đặt chứng chỉ SSL lên máy chủ CentOS sử dụng webserver Apache (opens in a new tab)" rel="noreferrer noopener" class="rank-math-link" href="http://thanhtam.works/cai-dat-chung-chi-ssl-len-may-chu-ubuntu-su-dung-webserver-apache/" target="_blank">Cài đặt chứng chỉ SSL lên máy chủ CentOS sử dụng webserver Apache</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 1: Tạo chứng chỉ SSL</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn cần tạo chứng chỉ SSL để sử dụng, bạn có thể tạo chứng chỉ miễn phí hoặc có phí của bất kỳ đơn vị nào, bạn cũng có thể xem lại bài viết tạo chứng chỉ miễn phí.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a aria-label=" (opens in a new tab)" rel="noreferrer noopener" class="rank-math-link" href="https://thanhtam.co.uk/huong-dan-cai-ssl-mien-phi/" target="_blank">Hướng dẫn cài SSL miễn phí</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><br>Bước 2: Thực hiện SSH vào máy chủ Ubuntu</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn dùng bất kỳ phần mềm nào có tính năng SSH vào VPS thì bạn hãy sử dụng nhé, ngoài ra thì bạn cũng có thể tham khảo thêm cách dùng SSH key để bảo mật hơn.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="http://thanhtam.works/huong-dan-tao-ssh-key-vps-tren-windows/" target="_blank" aria-label="Hướng dẫn tạo SSH key VPS trên Windows (opens in a new tab)" rel="noreferrer noopener" class="rank-math-link">Hướng dẫn tạo SSH key VPS trên Windows</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="http://thanhtam.works/huong-dan-tao-ssh-key-vps-tren-linux/" target="_blank" aria-label="Hướng dẫn tạo SSH key VPS trên Linux (opens in a new tab)" rel="noreferrer noopener" class="rank-math-link">Hướng dẫn tạo SSH key VPS trên Linux</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 3: Cài đặt a2enmod SSL</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn sẽ cần phải cài đặt a2enmod này để hỗ trợ cho kết nối SSL.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">a2enmod ssl</pre>
<!-- /wp:preformatted -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">root@sv:~# a2enmod ssl<br>Considering dependency setenvif for ssl:<br>Module setenvif already enabled<br>Considering dependency mime for ssl:<br>Module mime already enabled<br>Considering dependency socache_shmcb for ssl:<br>Enabling module socache_shmcb.<br>Enabling module ssl.<br>See /usr/share/doc/apache2/README.Debian.gz on how to configure SSL and create self-signed certificates.<br>To activate the new configuration, you need to run:<br>service apache2 restart</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Sau khi lệnh trên chạy xong thì bạn hãy restart lại apache luôn nhé.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Trước và sau khi cài a2enmod SSL</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">root@sv:~# netstat -tulpn | grep apache
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp6 0 0 :::80 :::* LISTEN 1080/apache2

root@sv:~# service apache2 restart

root@sv:~# netstat -tulpn | grep apache
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp6 0 0 :::80 :::* LISTEN 2178/apache2
tcp6 0 0 :::443 :::* LISTEN 2178/apache2</pre>
<!-- /wp:preformatted -->

<!-- wp:heading -->
<h2>Bước 4: Tạo thư mục, file chứa chứng chỉ</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Sau khi có đầy đủ các file chứng chỉ, bạn hãy thực hiện tạo các file crt, key, ca-bundle tương ứng tại đường dẫn</p>
<!-- /wp:paragraph -->

<!-- wp:verse -->
<pre class="wp-block-verse">/etc/ssl/certs/</pre>
<!-- /wp:verse -->

<!-- wp:paragraph -->
<p>Thông thường thì mình sẽ đặt tên các file bao gồm tên miền để dễ phân biệt. Ví dụ: <strong>domain.crt, domain.key, ca-domain.crt</strong></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 5: Cấu hình lại file virtual host</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn thực hiện thêm đoạn sau vào file config website, thường file config sẽ nằm tại <strong>/etc/apache2/sites-enabled/domain.conf</strong> , bạn hãy thay lại cho đúng với website của bạn nhé</p>
<!-- /wp:paragraph -->

<!-- wp:verse -->
<pre class="wp-block-verse">&lt;VirtualHost *:443&gt;
ServerName www.domain.com                      
ServerAlias domain.com             
DocumentRoot /var/www/domain.com/public_html                         
ErrorLog /var/www/domain.com/error.log                         
CustomLog /var/www/domain.com/requests.log combined                         SSLEngine on                         
SSLCertificateFile /etc/ssl/certs/domain.crt                         SSLCertificateKeyFile /etc/ssl/certs/domain.key                                  SSLCertificateChainFile /etc/ssl/certs/ca-domain.crt
&lt;/VirtualHost&gt;</pre>
<!-- /wp:verse -->

<!-- wp:heading -->
<h2>Bước 6: Kiểm tra lại service Apache</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bạn thực hiện chạy lệnh sau để kiểm tra lại cấu hình cài đặt trước đó xem có lỗi gì xảy ra không.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">apachectl configtest</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Khi bạn chạy lệnh này xong sẽ bạn sẽ nhận được thông báo sau là thành công.</p>
<!-- /wp:paragraph -->

<!-- wp:verse -->
<pre class="wp-block-verse">Syntax OK.</pre>
<!-- /wp:verse -->

<!-- wp:paragraph -->
<p>Cuối cùng bạn khởi động lại dịch vụ Apache để nhận lại cấu hình mới nhé.</p>
<!-- /wp:paragraph -->

<!-- wp:verse -->
<pre class="wp-block-verse">systemctl restart httpd</pre>
<!-- /wp:verse -->

<!-- wp:paragraph -->
<p>Vậy là quá trình cài đặt SSL lên máy chủ Apache trên server Ubuntu đã hoàn tất. Chúc bạn thực hiện thành công.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Ngoài ra thì bạn hãy kiểm tra thêm trạng thái SSL của website theo link <a aria-label="này (opens in a new tab)" rel="noreferrer noopener nofollow sponsored" href="https://www.sslshopper.com/ssl-checker.html" target="_blank" class="rank-math-link">này</a> nhé.</p>
<!-- /wp:paragraph -->
