---
title: "Hướng dẫn cấu hình ngăn chặn DDOS qua Memcached"
date: 2021-06-28
---

<!-- wp:heading -->
<h2>I. Giới thiệu</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Memcached là gì?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Theo định nghĩa trên trang chủ <a aria-label="Memcached (opens in a new tab)" href="https://memcached.org/" target="_blank" rel="noreferrer noopener" class="rank-math-link">Memcached</a>:</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p><strong>Free &amp; open source, high-performance, distributed memory object caching system</strong>, generic in nature, but intended for use in speeding up dynamic web applications by alleviating database load.<br>Memcached is an in-memory key-value store for small chunks of arbitrary data (strings, objects) from results of database calls, API calls, or page rendering.<br><strong>Memcached is simple yet powerful</strong>. Its simple design promotes quick deployment, ease of development, and solves many problems facing large data caches. Its API is available for most popular languages.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:heading {"level":3} -->
<h3>DDOS là gì?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Theo <a aria-label="Wikipedia (opens in a new tab)" href="https://en.wikipedia.org/wiki/Denial-of-service_attack" target="_blank" rel="noreferrer noopener" class="rank-math-link">Wikipedia</a>, tấn công từ chối dịch vụ phân tán(DDOS - viết tắt của&nbsp;<strong>Distributed Denial of Service</strong>) là một cuộc tấn công mạng trong đó thủ phạm tìm cách làm cho máy hoặc tài nguyên mạng không khả dụng cho người dùng dự định của nó bằng cách làm gián đoạn tạm thời hoặc vô thời hạn các dịch vụ của máy chủ được kết nối với Internet. Từ chối dịch vụ thường được thực hiện bằng cách làm ngập máy hoặc tài nguyên được nhắm mục tiêu với các yêu cầu thừa nhằm cố gắng làm quá tải hệ thống và ngăn một số hoặc tất cả các yêu cầu hợp pháp được thực hiện. </p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>II. Ngăn chặn DDOS qua Memcached</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>File cấu hình mặc định của memcached sẽ nằm tại vị trí <code><strong>/etc/sysconfig/memcached</strong></code>, và file này sẽ có nội dung như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">PORT="11211"<br>USER="memcached"<br>MAXCONN="1024"<br>CACHESIZE="64"<br>OPTIONS=""</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Với cấu hình này thì memcached sẽ lắng nghe ở giao thức TCP và UDP, cổng 11211, không cần xác thực để truy cập memcached.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Vì vậy, để cấu hình tắt kết nối qua UDP và chỉ cho phép kết nối qua TCP, bạn sẽ cần cấu hình sửa đổi lại giá trị <em>OPTIONS</em> như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">OPTIONS="-U 0"</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Và để cấu hình bắt buộc memcached chỉ cho phép kết nối truy cập từ trên máy chủ cài đặt(localhost), hạn chế kết nối từ bên ngoài thì bạn sẽ cần cấu hình sửa đổi giá trị <em>OPTIONS</em> như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">OPTIONS="-l 127.0.0.1"</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Và để kết hợp cấu hình vừa chặn UDP, vừa bắt buộc memcache kết nối qua localhost thì bạn sẽ cấu hình sửa đổi giá trị <em>OPTIONS</em> như sau:</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">OPTIONS="-U 0 -l 127.0.0.1"</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Tổng hợp lại cấu hình file <code><strong>/etc/sysconfig/memcached</strong></code> sau khi được thay đổi tắt kết nối qua UDP và tắt kết nối từ bên ngoài như sau.</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre id="block-ed602003-0ba1-4e4a-86cc-58e1588fe776" class="wp-block-preformatted">PORT="11211"
USER="memcached"
MAXCONN="1024"
CACHESIZE="64"
OPTIONS="-U 0 -l 127.0.0.1"</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph {"className":"terminal shadow"} -->
<p class="terminal shadow">Bây giờ bạn có thể kiểm tra lại kết nối của memcached đã không còn qua UDP nữa bằng lệnh <code><strong>netstat -tulpn | grep memcached</strong></code></p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<div class="terminal shadow"> 
    <pre class="body"> 
[root@server ~]# netstat -tulpn | grep memcached
tcp        0      0 127.0.0.1:11211         0.0.0.0:*               LISTEN      830/memcached
    </pre> 
</div>
<!-- /wp:html -->

<!-- wp:heading -->
<h2>III. Tổng kết</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Như vậy là mình đã hướng dẫn các bạn thao tác cấu hình Memcached để ngăn chặn DDOS thông qua UDP chỉ với vài dòng lệnh cơ bản. Việc này cũng sẽ giúp bảo mật, đem lại hiệu quả sử dụng VPS, server của bạn hơn. Chúc các bạn thành công.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Bài viết tham khảo: <a aria-label="Preventing DDoS amplification attacks using memcached (opens in a new tab)" href="https://access.redhat.com/solutions/3369081" target="_blank" rel="noreferrer noopener" class="rank-math-link">Preventing DDoS amplification attacks using memcached</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://thanhtam.works/category/kien-thuc/hosting-vps/" target="_blank" aria-label="Tổng hợp hướng dẫn về hosting-vps. (opens in a new tab)" rel="noreferrer noopener" class="rank-math-link">Tổng hợp hướng dẫn về hosting-vps.</a></p>
<!-- /wp:paragraph -->
