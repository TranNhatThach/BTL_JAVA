# Tutor Connect - Smart Tutoring Ecosystem

[![Java](https://img.shields.io/badge/Java-17-orange.svg?style=flat-square&logo=java)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.4.0-green.svg?style=flat-square&logo=spring-boot)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18.x-blue.svg?style=flat-square&logo=react)](https://react.dev/)
[![SQL Server](https://img.shields.io/badge/SQL_Server-2022-red.svg?style=flat-square&logo=microsoft-sql-server)](https://www.microsoft.com/en-us/sql-server/)
[![Ollama](https://img.shields.io/badge/AI-Ollama--Llama3.2-black.svg?style=flat-square&logo=ollama)](https://ollama.com/)

**Tutor Connect** là hệ thống kết nối học sinh và gia sư thông minh, tích hợp trí tuệ nhân tạo để tối ưu hóa quá trình học tập và giảng dạy. Đây là sản phẩm thuộc bài tập lớn môn Công nghệ Java.

---

## Key Features

- **Smart AI Chatbot**: Hỗ trợ giải đáp thắc mắc 24/7 thông qua model Llama 3.2.
- **OAuth2 Security**: Đăng nhập nhanh chóng qua Google (Yêu cầu cấu hình Client ID).
- **Token Auth**: Xác thực người dùng bảo mật qua JWT.
- **Schedule Management**: Quản lý lịch học, thời khóa biểu trực quan.
- **Real-time Interaction**: Giao tiếp trực tiếp giữa học sinh và gia sư.

---

## Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Backend** | Spring Boot 3, Spring Security, Hibernate, JWT, Maven |
| **Frontend** | React, TypeScript, Vite, TailwindCSS, Lucide Icons |
| **Database** | SQL Server |
| **AI/ML** | Ollama (Llama 3.2) |

---

## Getting Started

### 1. Prerequisites
- **JDK 17+**
- **Node.js (LTS)**
- **SQL Server**
- **Ollama** (Nếu muốn sử dụng AI)

### 2. Database Setup
1. Tạo database `HeThongGiaSu` trong SQL Server.
2. Cập nhật file `BE/src/main/resources/application.properties`:
   ```properties
   spring.datasource.username=YOUR_USERNAME
   spring.datasource.password=YOUR_PASSWORD
   ```

### 3. Google OAuth2 Setup (Quan trọng)
Để tính năng **Google Login** hoạt động cần:
1. Truy cập [Google Cloud Console](https://console.cloud.google.com/).
2. Tạo dự án mới và thiết lập **OAuth 2.0 Client IDs**.
3. Thêm URI điều hướng: `http://localhost:8080/login/oauth2/code/google`.
4. Tạo file `.env` trong thư mục `BE/` (hoặc cấu hình trực tiếp trong `application.properties`):
   ```env
   GOOGLE_CLIENT_ID=your_client_id_here
   GOOGLE_CLIENT_SECRET=your_client_secret_here
   ```

### 4. AI Model Setup (Optional)
```bash
# Di chuyển vào BE và tạo model
ollama create tutor-connect-ai -f BE/Modelfile
```

### 5. Running the Project

**Backend (Port 8080):**
```bash
cd BE
./mvnw spring-boot:run
```

**Frontend (Port 5173):**
```bash
cd FE
npm install
npm run dev
```

---

## Credentials (Demo Account)

| Role | Username | Password |
| :--- | :--- | :--- |
| **Admin** | `admin@example.com` | `admin123` |
| **Sample Tutor** | `tutor@example.com` | `password` |

---

## Project Structure

```text
├── BE/                   # Spring Boot Source Code (Java 17)
├── FE/                   # React Frontend Source Code (Vite)
├── README.md             # Project Documentation
└── .env                  # Environment Variables Container
```

---
💡 *Dự án được phát triển bởi **Trần Nhật Thạch và Nhóm 10** - UTC. Mọi ý kiến đóng góp vui lòng liên hệ qua GitHub.*
