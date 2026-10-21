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

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
1. **Viết mã CSS Boilerplate & Variables:** Tự động tạo bảng màu HSL/HEX neon hài hòa, tính toán spacing, border-radius và shadow phát sáng nhanh gấp 5 lần so với viết thủ công.
2. **Xây dựng cấu trúc Layout Grid & Flexbox:** Việc căn chỉnh bố cục phức tạp của bàn Mixer (3 cột trên desktop chuyển thành 1 cột trên mobile) được AI xử lý chính xác chỉ sau một câu lệnh.
3. **Tích hợp CDN & Icon:** Tự động liên kết đúng phiên bản CDN của FontAwesome, Animate.css, Google Fonts và AOS mà không cần tra cứu tài liệu thủ công.

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Đưa ra ràng buộc kỹ thuật rõ ràng ngay từ đầu (Constraint-first Prompting):** Nếu không nhấn mạnh "Semantic HTML5 100% và cấm lạm dụng thẻ `<div>`", AI sẽ mặc định dùng rất nhiều thẻ `<div>` tiện lợi nhưng sai chuẩn ngữ nghĩa.
- **Tiếp cận theo từng bước (Iterative Refinement):** Không nên yêu cầu AI làm tất cả trong một lần duy nhất mà nên đi từ Dựng khung chuẩn -> Áp dụng hệ thống biến CSS -> Tích hợp hiệu ứng/thư viện -> Tối ưu Responsive và Tinh chỉnh chi tiết.
- **Biết đọc hiểu code và debug kịp thời:** Lập trình viên phải hiểu rõ cơ chế hoạt động của thư viện (như vòng đời của AOS cần được kích hoạt bằng `AOS.init()`) để nhanh chóng phát hiện lỗi và đưa ra "Debug Prompt" chuẩn xác cho AI.
