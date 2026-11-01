# Chào mừng đến với Tổ chức Ecovia IoT 👋

> **Ecovia IoT** — Hệ sinh thái giám sát môi trường kho hàng thời gian thực (nhiệt độ, độ ẩm, ánh sáng, CO₂, bụi mịn PM2.5), phân loại ngưỡng tức thì tại biên, lưu trữ cơ sở dữ liệu và cảnh báo đa kênh (còi/LED tại chỗ, Web Audio chime trên dashboard và Telegram Bot).

---

## 🏛️ Kiến trúc & Các Repository Chính

Hệ thống được thiết kế theo kiến trúc vi dịch vụ & IoT biên (Edge Computing), phân chia thành các repository chuyên biệt:

```
┌────────────────────────┐         ┌────────────────────────┐         ┌────────────────────────┐
│  Ecovia-IoT/hardware   │  MQTT   │   Ecovia-IoT/backend   │ WS/HTTP │  Ecovia-IoT/frontend   │
│  ESP32/ESP32-S3 Edge   ├────────►│  Node.js Ingestion     ├────────►│  React 19 Dashboard    │
│  I2C Recovery & Buffer │         │  MongoDB & Telegram    │         │  Realtime + Web Audio  │
└────────────────────────┘         └────────────────────────┘         └────────────────────────┘
                                               ▲
                                               │ Tài liệu & Báo cáo
                                   ┌───────────┴────────────┐
                                   │   Ecovia-IoT/report    │
                                   │  34-page LaTeX & PDF   │
                                   └────────────────────────┘
```

| Repository | Công nghệ & Tính năng nổi bật | Trạng thái |
|---|---|---|
| [**📡 hardware**](https://github.com/Ecovia-IoT/hardware) | Firmware ESP32 DevKit & ESP32-S3 (PlatformIO, C++, FreeRTOS). Hỗ trợ cảm biến đa dạng: SHT31, BH1750, SCD41, PMS7003 và cảm biến phổ thông (DHT11/22, Quang trở LDR, Khí ga MQ). Tự động phục hồi bus I2C (9 SCL clock pulses) và bộ đệm vòng ngoại tuyến (offline ring buffer). | ![Build](https://img.shields.io/badge/PlatformIO-Pass-success) |
| [**⚙️ backend**](https://github.com/Ecovia-IoT/backend) | Dịch vụ Node/Express + MQTT + MongoDB. Xếp loại ngưỡng thông minh, chống báo động giả (alert streak), rate limiting, API Key auth, đẩy cảnh báo khẩn cấp qua **Telegram Bot**, và Socket.IO trực tiếp đến dashboard. Đầy đủ **47 unit test**. | ![Test](https://img.shields.io/badge/Tests-47%20passing-success) |
| [**💻 frontend**](https://github.com/Ecovia-IoT/frontend) | Dashboard React 19 + Vite + Tailwind CSS. Kết nối dữ liệu thật từ Backend qua Socket.IO, tự động phát âm thanh cảnh báo (Web Audio chime), 7 loại biểu đồ thời gian thực, chế độ sáng/tối, hỗ trợ đa thiết bị và đóng gói Docker Nginx. | ![Vite](https://img.shields.io/badge/Vite-Build%20OK-success) |
| [**📄 report**](https://github.com/Ecovia-IoT/report) | Toàn bộ mã nguồn LaTeX, sơ đồ kiến trúc Mermaid và bản PDF chính thức **34 trang** trình bày chi tiết thiết kế hệ thống, phân tích mạch phần cứng, giao thức MQTT và kết quả kiểm thử. | ![PDF](https://img.shields.io/badge/PDF-34%20Pages-blue) |

---

## 🚀 Khởi chạy nhanh toàn bộ dịch vụ (Docker)

```bash
# 1. Khởi động Mosquitto Broker, MongoDB, Backend và Frontend
docker compose up -d

# 2. Truy cập Dashboard:
# http://localhost:3000

# 3. Backend API & Socket.IO:
# http://localhost:4001/health
```

---

*Phát triển bởi nhóm dự án Ecovia IoT — 2026.*
