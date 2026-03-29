# Hệ thống CRM Nội Bộ Tích hợp AI
Nghiên cứu và Ứng dụng AI trong Hệ thống CRM Nội Bộ, Đánh giá Khách hàng và Tóm tắt Cuộc hẹn

## 🎥 Video Demo
Dưới đây là video demo (trải nghiệm hệ thống). Bạn có thể xem trực tiếp hoặc tải về qua link: [video_demo.mp4](./video_demo.mp4)

<video src="./video_demo.mp4" controls="controls" width="100%" style="max-width: 800px;">
  Trình duyệt của bạn không hỗ trợ thẻ video. Bạn có thể <a href="./video_demo.mp4">tải video tại đây</a>.
</video>

## 📖 Giới thiệu dự án
Dự án xây dựng một hệ thống Quản lý Quan hệ Khách hàng (CRM) nhằm hỗ trợ doanh nghiệp quản lý thông tin khách hàng, theo dõi quá trình chăm sóc khách hàng và tự động hóa các nghiệp vụ kinh doanh.
Hệ thống kết hợp các công cụ mã nguồn mở với công nghệ tự động hóa và Trí tuệ Nhân tạo (AI), giúp nhân viên kinh doanh làm việc hiệu quả từ khâu tiếp cận, ký kết hợp đồng đến theo dõi thanh toán.

## 🚀 Tính năng nổi bật
* **Quản trị Dữ liệu (NocoBase):** Quản lý khách hàng, lịch hẹn, hợp đồng và công nợ.
* **Tự động hóa Workflow (n8n):** Tự động tạo lịch hẹn (Google Calendar), gửi email thông báo (Gmail), và ghi nhận thanh toán tự động (qua SePay).
* **AI Tóm tắt Cuộc hẹn:** Sử dụng mô hình **Whisper** (Speech-to-Text) và **Gemini** để tự động chuyển đổi file ghi âm cuộc họp thành văn bản và tóm tắt nội dung trao đổi.
* **Đánh giá Khách hàng (Lead Scoring):** Phân tích và chấm điểm khách hàng tiềm năng dựa trên dữ liệu CRM.

## 🛠️ Công nghệ sử dụng
* **Nền tảng chính:** NocoBase, n8n, Docker, Cloudflare.
* **AI & Xử lý API:** Google Colab, FastAPI, Whisper, Gemini, Google Drive/Docs.

---

## ⚙️ Hướng dẫn Cài đặt & Chạy Ứng dụng

Dự án được cấu trúc thành các module độc lập. Yêu cầu hệ thống đã cài đặt **Docker** và **Docker Compose**.

### 1. Khởi chạy hệ thống NocoBase (Quản lý CRM)
1. Mở Terminal / Command Prompt và di chuyển vào thư mục `nocobase`:
   ```bash
   cd nocobase
   ```
2. Tạo file `.env` từ file mẫu và điền **Cloudflare Tunnel Token**:
   ```bash
   cp .env.example .env
   # Mở file .env và điền TUNNEL_TOKEN=...
   ```
3. Chạy hệ thống bằng Docker:
   ```bash
   docker-compose up -d
   ```
*(Lưu ý: Nếu hệ thống chưa có dữ liệu cấu hình UI, bạn hãy khôi phục từ file dump `nocobase_backup.sql` bằng lệnh sau (yêu cầu chạy trên Terminal/PowerShell) sau khi container đã khởi động:)*
   ```bash
   Get-Content nocobase_backup.sql | docker exec -i n-postgres-1 psql -U nocobase -d nocobase
   ```

### 2. Khởi chạy hệ thống Tự động hóa n8n
1. Di chuyển vào thư mục `self-hosted-ai-starter-kit-main`:
   ```bash
   cd self-hosted-ai-starter-kit-main
   ```
2. Tạo file `.env` từ file mẫu và thiết lập các biến môi trường (API keys, webhook URLs, và **TUNNEL_TOKEN** của Cloudflare Tunnel):
   ```bash
   cp .env.example .env
   # Mở file .env và điền các giá trị cấu hình tương ứng
   ```
3. Chạy n8n bằng Docker:
   ```bash
   docker-compose up -d
   ```

### 3. Khởi chạy Server AI (Whisper & Gemini)
Phần xử lý AI do yêu cầu cấu hình phần cứng (GPU) nên được triển khai trên **Google Colab**.
1. Truy cập thư mục `colab` trong dự án.
2. Tải file `ai-summary.ipynb` lên [Google Colab](https://colab.research.google.com/).
3. Mở file Notebook và chạy toàn bộ các cell để khởi tạo server **FastAPI** (thông qua Ngrok hoặc Cloudflare tunnels) phục vụ xử lý STT và tóm tắt AI cho n8n gọi tới.

---
**Lưu ý:** Đảm bảo các hệ thống (NocoBase, n8n, FastAPI Server) đã kết nối thành công qua Webhook/API theo cấu hình trong `.env` trước khi sử dụng.
