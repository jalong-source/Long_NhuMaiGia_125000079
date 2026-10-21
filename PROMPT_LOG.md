# Nhật ký Prompt Engineering

- **Họ tên:** Nhữ Mai Gia Long
- **MSSV:** 125000079
- **Đề tài:** Website Mix Nhạc - VibeMix Studio
- **Công cụ:** Antigravity

> Mình ghi lại ý chính các lần nhờ AI. Một số prompt được rút gọn cho dễ đọc, không phải bản chép nguyên văn từng tin nhắn.

## 1. Dựng giao diện ban đầu

**Prompt:**

> Làm giúp mình website chủ đề mix nhạc tên VibeMix Studio. Dùng HTML semantic, CSS variables, có responsive desktop với mobile. Chia trang thành phần giới thiệu, mixer, tính năng, beat demo, bảng giá, đánh giá và form liên hệ. Tách HTML với CSS cho dễ chỉnh.

**Sau đó mình xem lại:** AI dựng được bố cục và các khu vực chính. Mình yêu cầu dùng `article` cho các card và giữ danh sách dưới dạng `ul`/`li`, thay vì bọc mọi thứ bằng `div`.

## 2. Thêm mixer và hiệu ứng

**Prompt:**

> Thêm bàn mixer có hai deck, EQ, crossfader và vài nút FX. Cho đĩa than với visualizer chuyển động, nhưng giữ các nút dễ nhìn và đừng để hiệu ứng làm rối nội dung.

**Kết quả:** Có giao diện mixer và animation CSS. Mình dùng Animate.css cho một số nội dung đầu trang và AOS cho các section khi cuộn.

**Debug prompt:**

> Kiểm tra giúp mình AOS: các phần tử có `data-aos` nhưng khi cuộn chưa thấy hiệu ứng. Kiểm tra thứ tự nạp thư viện và chỗ gọi `AOS.init()`, sửa để nội dung không bị ẩn nếu thư viện không tải được.

**Ghi chú:** Trong `index.html` hiện có AOS CDN, thuộc tính `data-aos` và đoạn gọi `AOS.init()` gần cuối trang. Mình cần xem lại trên trình duyệt sau khi chỉnh sửa để chắc hiệu ứng hiển thị đúng.

## 3. Chỉnh giao diện và link

**Prompt:**

> Chuyển giao diện sang tông vàng, đen và trắng. Bỏ phần tên sinh viên trên thanh đầu trang, bỏ hai cột công nghệ và thông tin sinh viên ở footer. Gắn link cho các icon mạng xã hội, giữ lại phần thương hiệu và điều hướng.

**Kết quả:** Header và footer được tinh gọn, các icon social có thể mở link. Mình cũng nhờ AI thêm hiệu ứng viền sáng cho header và mixer.

## 4. Sửa giao diện mobile

**Prompt:**

> Trên màn hình nhỏ, phần form liên hệ và tiêu đề bị tràn ngang. Kiểm tra nguyên nhân trong CSS rồi chỉnh padding, kích thước nút và grid cho vừa mobile; đừng làm ảnh hưởng desktop.

**Kết quả:** CSS có media query cho màn hình nhỏ, giảm padding của form và cho nút được xuống dòng. Mình cần kiểm tra ở vài kích thước màn hình, vì chỉ nhìn trên desktop chưa đủ.

## 5. Thêm nhạc Tokyo Drift

**Prompt ban đầu:**

> Cho bài Tokyo Drift phát sau khi người dùng thao tác trên trang và để chạy được trên GitHub Pages. Nếu trình duyệt chặn autoplay thì xử lý theo cách phù hợp.

**Điều chỉnh sau đó:** Mình đổi ý, không muốn nhạc tự bật sau bất kỳ cú chạm nào nữa. Nhạc chỉ nên phát khi nhấn Play ở mixer; phần đĩa than và trạng thái trên hero đi theo trạng thái phát nhạc.

**Ghi chú kỹ thuật:** Trình duyệt thường chặn âm thanh tự phát trước khi có thao tác của người dùng. File nhạc hiện nằm trong `assets/`, nên mình dùng đường dẫn tương đối để phù hợp với GitHub Pages.

## 6. Thêm chế độ sáng/tối và đổi màu

**Prompt:**

> Thêm nút đổi sáng/tối và vài lựa chọn màu chủ đạo. Lưu lựa chọn để tải lại trang vẫn giữ theme, rồi gom bộ điều khiển vào nút nổi ở góc màn hình.

**Kết quả:** JavaScript dùng `data-theme`, `data-accent` và `localStorage` để lưu lựa chọn. Khi tự kiểm tra, mình thấy có vài phần vẫn giữ màu cũ vì CSS viết màu trực tiếp thay vì dùng biến.

**Debug prompt:**

> Khi đổi màu chủ đạo, một số chỗ như mixer, nút, viền và nền card vẫn còn màu vàng/đen cũ. Rà CSS, đưa các màu nhấn và nền cần đổi vào biến dùng chung; kiểm tra cả sáng lẫn tối. Giữ nguyên màu riêng của các trạng thái như YouTube và đèn báo.

**Kết quả lần sửa:** Mình chuyển thêm màu nhấn, viền và bề mặt điều khiển sang CSS variables, đồng thời thêm biến RGB để dùng màu nhấn với độ trong suốt. Màu đỏ YouTube và màu báo trạng thái được giữ riêng.

## 7. Rà soát trước khi nộp

**Prompt:**

> So sánh website với rubric của bài. Nêu phần đã có, phần còn thiếu và dẫn chứng từ file cụ thể. Đừng kết luận đạt điểm tối đa nếu chưa kiểm tra link deploy, Git hoặc giao diện thực tế.

**Ghi chú:** Tên repository, commit và link Live Preview cần đối chiếu trực tiếp trên GitHub. Mình không nên ghi là đã đạt đủ điểm nếu chưa kiểm tra các mục đó.

## 8. Tự đánh giá

### AI giúp mình tiết kiệm thời gian ở đâu?

AI giúp mình dựng nhanh bố cục ban đầu, viết CSS cho các trạng thái giao diện và tạo hiệu ứng cho mixer. Khi gặp lỗi cụ thể như tràn ngang hoặc màu không đổi theo palette, mình cũng dễ khoanh vùng phần cần kiểm tra hơn.

### Mình rút ra điều gì khi viết prompt?

Mình nên nói rõ phần nào cần sửa, phần nào cần giữ nguyên và cách kiểm tra kết quả. Với lỗi giao diện, mô tả đúng vị trí, trạng thái và thiết bị gặp lỗi hữu ích hơn câu chung chung như “làm đẹp hơn”. Sau khi AI sửa, mình vẫn phải tự xem trang và thử các tương tác.

## 9. Khó khăn và cách debug

Khó khăn mình gặp là đổi màu theme chưa đồng nhất: một vài component vẫn giữ màu cố định trong CSS. Mình yêu cầu AI tìm các màu hard-code liên quan đến accent, chuyển chúng sang biến CSS và rà lại cả hai chế độ sáng/tối. Sau khi sửa, cần thử từng palette và bật/tắt theme để kiểm tra nút, card, mixer, viền và chữ.
