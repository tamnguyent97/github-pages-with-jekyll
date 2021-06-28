Cấu hình SFTP bằng SSH Key với FileZilla
<!-- wp:paragraph -->
<p>Bạn đang quản trị VPS và cấu hình bảo mật trên VPS không cho thực hiện SSH bằng mật khẩu mà thực hiện SSH qua SSH Key. Vì vậy việc bạn thực hiện upload dữ liệu thông qua FTP sẽ không thực hiện được. Hôm nay mình sẽ hướng dẫn các bạn cách thực hiện dùng SSH Key với phần mềm FileZilla thông qua giao thức SFTP.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Bước 1: Tạo SSH Key</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Bài viết tạo SSH Key bạn có thể xem lại.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a aria-label=" (opens in a new tab)" href="https://thanhtam.works/tao-ssh-key-vps-tren-linux/" target="_blank" rel="noreferrer noopener" class="rank-math-link">Tạo SSH Key VPS trên Linux</a></li><li><a aria-label=" (opens in a new tab)" href="https://thanhtam.works/huong-dan-tao-ssh-key-vps-tren-windows/" target="_blank" rel="noreferrer noopener" class="rank-math-link">Tạo SSH key VPS trên Windows</a></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Bước 2: Cấu hình phần mềm FTP với SSH Key</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Có rất nhiều phần mềm FTP bạn có thể tham khảo sử dụng, ở đây mình sẽ sử dụng phần mềm <strong>FileZilla</strong>, link tải phần mềm này bạn có thể truy cập ở <a aria-label="link (opens in a new tab)" href="https://filezilla-project.org/" target="_blank" rel="noreferrer noopener" class="rank-math-link">link</a>. Phần mềm này có đủ các hệ điều hành Windows, MacOS, Linux.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Cách cấu hình.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Mở phần mềm FileZilla và chọn menu <strong>Edit</strong>, nhấn vào <strong>Settings</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Ở tab <strong>Connection</strong>,  chọn <strong>SFTP</strong>, ở đây sẽ có khung chứa các key đã thêm vào nếu có, và ở đây mình sẽ nhấn vào <strong>Add key file</strong> để thiết lập key. Một khung thư mục mới hiện ra, bạn di chuyển đến vị trí file private key đã tạo ở bước 1, FileZilla sẽ thiết lập key này.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":2795,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="https://thanhtam.works/wp-content/uploads/2020/12/ftp-ssh-key-1.png" alt="" class="wp-image-2795"/><figcaption>Add key file.</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Lưu ý: Nếu bạn sử dụng MacOS hoặc Linux thì khi thêm key vào thì FileZilla sẽ convert lại định dạng key. Bạn cần nhấn <strong>Yes</strong> khi được yêu cầu.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2796,"sizeSlug":"large"} -->
<div class="wp-block-image"><figure class="aligncenter size-large"><img src="https://thanhtam.works/wp-content/uploads/2020/12/ftp-ssh-key-2.png" alt="" class="wp-image-2796"/><figcaption>Convert key file.</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Và nếu key của bạn tạo ra có passphase thì sẽ có khung yêu cầu nhập lại passphase này.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2797,"sizeSlug":"large"} -->
<div class="wp-block-image"><figure class="aligncenter size-large"><img src="https://thanhtam.works/wp-content/uploads/2020/12/ftp-ssh-key-3.png" alt="" class="wp-image-2797"/><figcaption>Yêu cầu nhập passphase của private key.</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:heading -->
<h2>Bước 3: Tạo kết nối SFTP</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Sau khi hoàn tất hai bước cấu hình ở trên thì bây giờ bạn có thể thực hiện việc kết nối FTP qua tạo một kết nối đến VPS của bạn.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2803,"sizeSlug":"large"} -->
<div class="wp-block-image"><figure class="aligncenter size-large"><img src="https://thanhtam.works/wp-content/uploads/2020/12/ftp-ssh-key-4-1.png" alt="" class="wp-image-2803"/><figcaption>Tạo kết nối SFTP.</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:image {"align":"center","id":2801,"sizeSlug":"large"} -->
<div class="wp-block-image"><figure class="aligncenter size-large"><img src="https://thanhtam.works/wp-content/uploads/2020/12/ftp-ssh-key-5.png" alt="" class="wp-image-2801"/><figcaption>Nhập passphase của private key đã tạo ra ở bước 1 và được lặp lại ở bước 2.</figcaption></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Như vậy mình đã hướng dẫn hoàn tất thao tác dùng SSH Key để sử dụng cho công việc upload dữ liệu qua SFTP để bảo mật. Chúc các bạn thành công.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Tài liệu tham khảo: How to set up SFTP access for multiple users</p>
<!-- /wp:paragraph -->
