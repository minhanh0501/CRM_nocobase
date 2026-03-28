# Hệ thống CRM Nội Bộ Tích hợp AI
Nghiên cứu và Ứng dụng AI trong Hệ thống CRM Nội Bộ, Đánh giá Khách hàng và Tóm tắt Cuộc hẹn


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
2. Cấu hình các biến môi trường trong file `.env` nếu cần.
3. Chạy hệ thống bằng Docker:
   ```bash
   docker-compose up -d
   ```
*(Lưu ý: Nếu hệ thống chưa có dữ liệu, bạn có thể restore từ file dump `nocobase_backup.sql` đi kèm trong thư mục).*

### 2. Khởi chạy hệ thống Tự động hóa n8n
1. Di chuyển vào thư mục `self-hosted-ai-starter-kit-main`:
   ```bash
   cd self-hosted-ai-starter-kit-main
   ```
2. Cấu hình biến môi trường trong `.env` (ví dụ: API keys, webhook URLs).
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
