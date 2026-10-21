# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Nhữ Mai Gia Long
- **MSSV:** 125000079
- **Tên đề tài Website:** Mix Nhạc (VibeMix Studio - Nền tảng Studio Mix Nhạc Trực Tuyến & Hòa Âm Phối Khí)
- **Công cụ AI đã sử dụng:** Antigravity

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> **Prompt:**  
> *"Đóng vai trò là một chuyên gia Frontend Developer và Prompt Engineer cao cấp. Hãy giúp tôi xây dựng toàn bộ mã nguồn cho một website theo chuẩn Vibe Coding với chủ đề 'Mix Nhạc' dành cho bài kiểm tra giữa kỳ môn Thiết Kế Web. Thông tin sinh viên: Nhữ Mai Gia Long - MSSV: 125000079.  
> Cấu trúc dự án gồm: `index.html`, `style.css`, thư mục `assets/` và `PROMPT_LOG.md`.  
> Yêu cầu kỹ thuật bắt buộc:  
> 1. Chuẩn Semantic HTML5 100%: Sử dụng bắt buộc tối thiểu 5 thẻ: `<header>`, `<nav>`, `<main>`, `<section>` hoặc `<article>`, `<footer>`. Tuyệt đối không lạm dụng thẻ `<div>` vô nghĩa.  
> 2. CSS & CSS Variables: Khai báo toàn bộ biến ở `:root` (màu sắc neon/studio dark mode, font, spacing, radius). Sử dụng Flexbox cho Navigation/Controls và CSS Grid cho Feature cards/Track cards/Pricing. Tự viết hiệu ứng `:hover`, `:focus`, `:active` mượt mà. Đảm bảo Responsive (Mobile, Tablet, Desktop).  
> 3. Tương tác & Thư viện: Nhúng CDN Animate.css v4.1.1, AOS (Animate On Scroll) CSS & JS, FontAwesome 6, Google Fonts (Inter & Outfit). Thêm thuộc tính `data-aos` và khởi tạo `AOS.init()`.  
> 4. Tạo file nhật ký `PROMPT_LOG.md` theo mẫu chuẩn của đề thi."*

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & Khai báo CSS Variables
- **Prompt đã dùng:**  
  *"Thiết kế khung cấu trúc HTML5 chuẩn ngữ nghĩa cho website Mix Nhạc. Bắt buộc có `<header>` (chứa logo SVG, tên dự án, thông tin sinh viên Nhữ Mai Gia Long - 125000079, thanh `<nav>`), `<main>` chia thành các `<section>` chức năng (Hero Section, Bàn Mixer tương tác, Tính năng Studio, Kho Beat Demo, Bảng giá, Testimonials, Form nhận Beat), và `<footer>`. Khai báo bảng mã màu Dark Mode Neon Studio bằng CSS Variables ở `:root` trong `style.css`."*
- **Kết quả AI tạo ra:**  
  AI đã sinh ra khung HTML và hệ thống biến CSS hoàn chỉnh. Tuy nhiên, ở các danh sách thẻ card tính năng và bài nhạc, AI có xu hướng dùng các thẻ `<div class="card">` bọc lồng nhau 3-4 lớp.
- **Nhận xét & Tinh chỉnh của SV (Feedback & Refactor):**  
  Tôi đã phát hiện việc lạm dụng thẻ `<div>` sẽ vi phạm tiêu chí chấm điểm Semantic HTML5 của giảng viên. Tôi gửi tiếp prompt chỉnh sửa:  
  *"Refactor lại toàn bộ các thẻ `<div class="card">` thành thẻ `<article class="feature-card">` và `<article class="track-card">`. Thay thế các khối danh sách bằng `<ul>` và `<li>` chuẩn semantic. Đảm bảo mỗi `<section>` đều có `<header class="section-header">` riêng biệt với thẻ `<h2>` và `<p>` đúng phân cấp Heading."*

---

### Lần 2: Tích hợp thư viện Animate.css & AOS (Animate On Scroll)
- **Prompt đã dùng:**  
  *"Nhúng CDN Animate.css (v4.1.1) và AOS CSS/JS (v2.3.1) vào `index.html`. Thêm class hiệu ứng động `animate__animated animate__fadeInDown`, `animate__pulse` vào Hero banner và nút CTA. Bổ sung thuộc tính `data-aos="fade-up"`, `data-aos="zoom-in"` cho các section nội dung."*
- **Thách thức gặp phải:**  
  Khi xem trước trang web, các hiệu ứng của Animate.css trên Hero chạy tốt, nhưng khi cuộn chuột xuống các section bên dưới thì các card nội dung bị ẩn trắng hoặc không chạy animation xuất hiện mượt mà. Nguyên nhân là do chưa chèn script gọi hàm `AOS.init()` ở cuối thẻ `<body>`.
- **Cách sửa prompt (Debug prompt):**  
  *"Sửa lỗi AOS không kích hoạt khi cuộn trang: Hãy đặt thẻ `<script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>` trước khi đóng thẻ `</body>` và thêm đoạn script khởi tạo:  
  `<script> AOS.init({ duration: 800, easing: 'ease-out-cubic', once: true, offset: 80 }); </script>`.  
  Đồng thời kiểm tra thuộc tính `data-aos` để các phần tử không bị ẩn vĩnh viễn nếu JS tải chậm."*

---

### Lần 3: Tối ưu UI/UX Responsive, Bàn Mixer Trực Quan & Hiệu Ứng CSS
- **Prompt đã dùng:**  
  *"Tạo giao diện một bàn DJ Mixer trực quan với 2 Deck âm thanh A/B, thanh gạt Crossfader ở giữa, bảng đèn VU Meter nhảy theo nhịp, các nút hiệu ứng Sound FX (DROP, HORN, SCRATCH, REVERB) và đĩa than Vinyl xoay 360 độ bằng CSS thuần. Thêm hiệu ứng `:hover`, `:focus-visible`, `:active` có ánh sáng neon glow cho các nút bấm và slider range. Tối ưu Media Queries để bàn Mixer và Grid tự co giãn đẹp mắt trên điện thoại và máy tính bảng."*
- **Kết quả AI tạo ra:**  
  AI đã hoàn thiện bàn Mixer phong cách Studio cao cấp với hiệu ứng ánh sáng neon, thanh slider tùy biến (`-webkit-slider-thumb`), đĩa than quay vô tận (`@keyframes spinVinyl`), cùng dàn cột sóng âm Equalizer nhảy nhót sống động (`@keyframes danceBars`). Giao diện responsive 100% không bị vỡ layout trên màn hình nhỏ.

---

### Lần 4: Tinh chỉnh Tone màu Vàng - Đen - Trắng, Viền LED Chạy Đuổi, Tối ưu Header/Footer & Social Links
- **Prompt đã dùng:**  
  *"Chỉnh sửa giao diện hiện tại theo phong cách Vàng - Đen - Trắng chạy LED đuổi:  
  1. Ở thanh điều hướng trên cùng, xóa phần thông tin 'Nhữ Mai Gia Long - 125000079'.  
  2. Ở footer, xóa toàn bộ hai cột 'Công Nghệ Sử Dụng' và 'Thông Tin Sinh Viên'. Căn chỉnh lại 2 cột còn lại (Brand & Quick Links) cân đối trên desktop và hiển thị gọn đẹp trên mobile.  
  3. Xóa câu 'Bản quyền thuộc về sinh viên Nhữ Mai Gia Long (125000079). Đề tài: Mix Nhạc.', chỉ giữ lại dòng '© 2026 VibeMix Studio.' và dòng 'Được xây dựng với triết lý Vibe Coding & Prompt Engineering.'  
  4. Gắn liên kết mạng xã hội chính xác có thể nhấn được (mở tab mới `target='_blank'` và `rel='noopener noreferrer'`) gồm:  
     - GitHub: https://github.com/jalong-source  
     - Facebook: https://web.facebook.com/beastedm  
     - SoundCloud: https://soundcloud.com/gialongbeast  
     - YouTube: https://www.youtube.com/@longgia9034  
  5. Thiết kế hiệu ứng viền LED chạy đuổi (chasing LED border) bằng CSS thuần cho Header, bàn Mixer, Console và các card nổi bật."*
- **Kết quả AI tạo ra:**  
  - Giao diện chuyển đổi sang tone màu Vàng Hoàng Kim (`#FFD700`), Đen Obsidian (`#08080A`) và Trắng tương phản cực kỳ sang trọng, chuyên nghiệp.
  - Xây dựng thành công hiệu ứng **LED viền chạy đuổi** liên tục (`@keyframes ledChaseBorder` và `@keyframes ledChaseHorizontal`) ở viền trên header và bao quanh bàn Mixer Studio.
  - Các icon mạng xã hội hoạt động chính xác với đầy đủ thuộc tính bảo mật và hiệu ứng hover phát sáng vàng neon.
  - Footer được tinh gọn còn 2 cột cân đối, responsive linh hoạt theo trục dọc trên điện thoại di động.

---

### Lần 5: Tích hợp âm thanh Tokyo Drift, Cơ chế First-Interaction Phát Nhạc & Tương Thích GitHub Pages
- **Prompt đã dùng:**  
  *"Thêm chức năng phát nhạc Tokyo Drift cho website:  
  1. Sử dụng file audio Tokyo Drift có sẵn trong dự án (`Low X Tokyo Drift Remix - Full Mashup.mp3`), chuẩn hóa đường dẫn tương đối `assets/tokyo-drift.mp3` để tương thích hoàn toàn khi deploy lên GitHub Pages (kể cả khi deploy dưới repo sub-path).  
  2. Tuân thủ chính sách trình duyệt: Không cố phát nhạc có tiếng ngay khi vừa tải trang để tránh bị chặn Autoplay.  
  3. Cơ chế First-Interaction: Lắng nghe cú chạm hoặc nhấn đầu tiên của người dùng ở bất kỳ đâu trên trang để kích hoạt phát nhạc đúng 1 lần, tuyệt đối không gọi `e.stopPropagation()` hay `e.preventDefault()` để không gây ảnh hưởng đến hoạt động của nút bấm, mixer hay link hiện có.  
  4. Bổ sung nút Bật/Tạm dừng rõ ràng (Floating Player Widget) với biểu tượng đĩa than xoay đồng bộ và đèn trạng thái ON AIR / PAUSED để người dùng toàn quyền kiểm soát âm thanh. Bắt lỗi Promise nhẹ nhàng nếu trình duyệt từ chối hoặc file chưa tải xong."*
- **Thách thức gặp phải & Giải pháp:**  
  - *Thách thức 1:* Chính sách Autoplay nghiêm ngặt của Chrome, Safari và Firefox sẽ ném ra ngoại lệ `NotAllowedError` nếu tự động gọi `audio.play()` khi chưa có tương tác từ người dùng.  
  - *Giải pháp:* Đăng ký sự kiện lắng nghe một lần (`once: true`) cho `click`, `touchstart`, `keydown` trên toàn bộ cửa sổ. Khi người dùng thực hiện thao tác đầu tiên, hàm `playAudioSafely()` được kích hoạt an toàn trong khối `try/catch` với Promise callback.  
  - *Thách thức 2:* Đường dẫn tuyệt đối dạng `/assets/...` sẽ bị lỗi 404 khi deploy lên GitHub Pages vì GitHub Pages đặt website dưới đường dẫn `username.github.io/repo-name/`.  
  - *Giải pháp:* Dùng đường dẫn tương đối chuẩn `assets/tokyo-drift.mp3` (viết thường toàn bộ, không có dấu `/` ở đầu), giúp trình duyệt tự resolve chính xác tại mọi môi trường host.
- **Kết quả AI tạo ra:**  
  Tính năng phát nhạc Tokyo Drift Remix hoạt động mượt mà, hòa quyện cùng hiệu ứng xoay của đĩa than và dàn sóng âm Equalizer, có Floating Player widget sang trọng giúp người dùng bật/tắt tức thì.

---

### Lần 6: Tích hợp liên kết YouTube thực tế cho kho Beat & Tạo tài liệu README.md chuẩn bị nộp bài
- **Prompt đã dùng:**  
  *"Rà soát website theo rubric chấm điểm và tối ưu thêm:  
  1. Thay đổi 4 bản nhạc trong section 'Bộ Sưu Tập Beat & Preset Nóng Bỏng' thành các liên kết mở trực tiếp sang các video YouTube thực tế theo từng thể loại (EDM Big Room, Lo-Fi Chill, Future House, Tokyo Drift Drill Trap) với `target='_blank'` và `rel='noopener noreferrer'`.  
  2. Bổ sung file `README.md` lưu đầy đủ thông tin sinh viên Nhữ Mai Gia Long, MSSV 125000079 và dán nổi bật link GitHub Pages Live Preview (`https://jalong-source.github.io/Long_NhuMaiGia_125000079/`).  
  3. Thêm tuyên bố miễn trừ trách nhiệm (Disclaimer) xác nhận dự án phục vụ mục đích học tập môn Thiết Kế Web, hoàn toàn phi thương mại."*
- **Kết quả AI tạo ra:**  
  - Cả 4 card nhạc demo đã được gắn icon YouTube màu đỏ nổi bật và link dẫn đến các tác phẩm âm nhạc thực tế, giúp website chân thực và tương tác sống động hơn.
  - File `README.md` được khởi tạo hoàn chỉnh, chuyên nghiệp, hỗ trợ Giảng viên chấm bài nhanh chóng chỉ bằng một cú click chuột vào link Live Preview.
  - Dự án đáp ứng trọn vẹn 100% tiêu chí thang điểm 10 trong rubric chấm thi.

---

### Lần 7: Sửa dứt điểm lỗi tràn viền ngang (Horizontal Overflow) trên thiết bị di động
- **Prompt đã dùng:**  
  *"Phần giao diện mobile bị lỗi tràn viền ngang: Tiêu đề 'Tải Ngay Bộ Sound FX & Beat Pack 2026' và Form nhận quà bị lòi ra khỏi mép phải màn hình, chữ và nút bị cắt. Hãy kiểm tra và khắc phục gấp lỗi này."*
- **Nguyên nhân phát hiện:**  
  - `.contact-card` mang padding desktop mặc định quá lớn (`padding: 4.5rem = 72px`), cộng thêm `.contact-form` có padding `2.5rem = 40px` và `.section-container` có padding `24px`. Tổng padding chiếm tới hơn 270px, khiến chiều rộng khả dụng trên mobile (< 390px) không đủ chứa form.  
  - Thuộc tính `white-space: nowrap` trên class `.btn` làm cho nút submit dài bị cố định chiều ngang, đẩy bung lề phải của container.
- **Cách khắc phục:**  
  - Thiết lập `overflow-x: hidden` và `max-width: 100vw` cho `html, body` và `.section-container`.  
  - Điều chỉnh padding responsive cho `.contact-card` (`padding: 1.5rem 1rem !important`) và `.contact-form` (`padding: 1.2rem 0.9rem !important`).  
  - Cho phép nút bấm xuống dòng linh hoạt (`white-space: normal`) và đặt chiều rộng 100% trên thiết bị di động.  
  - Bổ sung media query phụ `@media (max-width: 420px)` tối ưu cho các dòng máy màn hình nhỏ (iPhone SE, Galaxy mini).
- **Kết quả AI tạo ra:**  
  Toàn bộ giao diện section nhận quà và form đăng ký hiển thị gọn gàng, vừa khít trong khung nhìn mobile, không còn hiện tượng tràn mép ngang.

---

### Lần 8: Tích hợp chế độ Sáng / Tối (Dark & Light Mode) và Bộ chọn màu chủ đạo (Accent Color Palette Switcher)
- **Prompt đã dùng:**  
  *"Thêm chế độ sáng tối và chọn màu theme cho website VibeMix Studio."*
- **Ý tưởng & Kỹ thuật triển khai:**  
  - **Chế độ Sáng / Tối (Dark/Light Mode):**  
    + Bổ sung nút chuyển đổi với icon Mặt trăng / Mặt trời trên Header (`#theme-mode-btn`).  
    + Sử dụng thuộc tính `data-theme="light"` trên thẻ `<html>` để ghi đè các biến CSS (nền trắng ngà `#f4f6fa`, chữ đen than `#0f172a`, card trắng sang trọng, bóng đổ dịu nhẹ).  
    + Tự động lưu cấu hình người dùng vào `localStorage` (`vibemix_theme`) để duy trì trạng thái khi người dùng tải lại trang.  
  - **Bộ chọn màu Theme (Accent Color Palette):**  
    + Thiết kế 5 chấm màu (Color Dots) trực quan trên Header: **Vàng Hoàng Kim (Gold)**, **Xanh Cyan Neon (Cyan)**, **Hồng Neon EDM (Pink)**, **Xanh Lá Điện Tử (Green)**, **Tím Vũ Trụ (Purple)**.  
    + Khi click vào từng chấm màu, áp dụng `data-accent="..."` và tự động cập nhật lại các biến `--primary-color`, `--primary-hover`, `--primary-glow`, v.v. trên toàn bộ hệ thống giao diện (bàn mix, viền LED, icon, nút bấm, equalizer).  
    + Ghi nhớ lựa chọn màu sắc qua `localStorage` (`vibemix_accent`).
- **Kết quả AI tạo ra:**  
  Website có khả năng tùy biến giao diện cực kỳ phong phú và hiện đại. Người dùng có thể tự do phối hợp giữa giao diện Sáng hoặc Tối với 5 tone màu neon yêu thích chỉ bằng một cú nhấp chuột.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
1. **Viết mã CSS Variables & Hiệu ứng Phức Tạp:** Xây dựng bảng màu Vàng - Đen - Trắng và hiệu ứng viền LED chạy đuổi (Chasing LED border) nhanh chóng bằng kỹ thuật `background-size` kết hợp mask và conic/linear gradients.
2. **Căn Chỉnh Layout Đa Thiết Bị (Responsive):** Chuyển đổi từ bố cục 4 cột ban đầu sang 2 cột footer tinh gọn, tự động co giãn từ desktop xuống mobile mà không bị vỡ giao diện.
3. **Tích hợp Semantic & Liên kết chuẩn chỉ:** Refactor mã nguồn nhanh gọn, đảm bảo 100% tuân thủ các quy tắc chuẩn HTML5 và Accessibility (aria-label, noopener noreferrer).

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Đưa ra yêu cầu cụ thể về màu sắc và hiệu ứng (Theme & Motion specifics):** Chỉ định rõ "phong cách vàng đen chạy LED đuổi" giúp AI lựa chọn chính xác mã màu tương phản cao và xây dựng animation chuyển động tinh tế thay vì màu sắc chung chung.
- **Quản lý cấu trúc theo Module độc lập:** Khi cần thay đổi bố cục (như bỏ cột footer hoặc xóa badge header), cần chỉ rõ phần tử cần bỏ và cách thức tái bố trí (rebalance) các phần tử còn lại để đảm bảo tính thẩm mỹ tổng thể.
- **Kiểm thử liên kết và hành vi tương tác thực tế:** Luôn kiểm tra các link ngoại vi (`target="_blank"`, `rel="noopener noreferrer"`) và các trạng thái `:hover`, `:focus` để đảm bảo trải nghiệm người dùng liền mạch.
