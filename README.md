# 📚 eLibrary - Hệ thống Thư viện Điện tử

Dự án eLibrary là một hệ thống quản lý thư viện điện tử hiện đại, cho phép người dùng đọc sách trực tuyến, mượn sách, đánh giá sách và quản lý gói đăng ký. Dự án được xây dựng với kiến trúc microservices, sử dụng Spring Boot cho backend và React cho frontend.

## 🎯 Tính năng chính

### Quản lý Sách
- Tìm kiếm sách với Elasticsearch
- Xem chi tiết sách
- Lọc sách theo danh mục, ngôn ngữ
- Đánh giá và xếp hạng sách
- Xem sách mới nhất

### Quản lý Người dùng
- Đăng ký/Đăng nhập
- Xác thực email với OTP
- OAuth2 (Google, GitHub)
- Quản lý profile
- Quên mật khẩu

### Mượn sách
- Mượn sách trực tuyến
- Gia hạn thời gian mượn
- Tự động kiểm tra hạn mượn

### Gói đăng ký
- Xem các gói đăng ký
- Đăng ký gói với VNPay
- Quản lý gói đăng ký của người dùng
- Tự động gia hạn/hủy gói

### Thanh toán
- Tích hợp VNPay
- Xử lý callback thanh toán
- Lịch sử thanh toán

## 🛠️ Công nghệ sử dụng

### Backend
- **Framework**: Spring Boot 3.5.5
- **Java**: 21
- **Database**: MySQL 8.1.0
- **Cache**: Redis
- **Search Engine**: Elasticsearch 8.15.3
- **ORM**: Spring Data JPA / Hibernate
- **Security**: Spring Security, OAuth2, JWT
- **API Documentation**: SpringDoc OpenAPI (Swagger)
- **Mapping**: MapStruct
- **Build Tool**: Maven
- **Email**: Spring Mail
- **Payment**: VNPay Integration

### Frontend
- **Framework**: React 19.1.1
- **Build Tool**: Vite 7.1.7
- **Routing**: React Router DOM 7.9.3
- **Testing**: Vitest 4.0.8, React Testing Library
- **Linting**: ESLint
- **Infinite Scroll**: react-infinite-scroll-component

### DevOps
- **Containerization**: Docker, Docker Compose
- **Web Server**: Nginx (cho frontend)

## 📁 Cấu trúc dự án

```
Doancnpm/
├── eLibrary_service/          # Backend Spring Boot
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/cnpm/eLibrary_service/
│   │   │   │   ├── configuration/    # Cấu hình (Security, OAuth2, JWT, VNPay)
│   │   │   │   ├── controller/       # REST Controllers
│   │   │   │   ├── dto/              # Data Transfer Objects
│   │   │   │   ├── entity/           # JPA Entities
│   │   │   │   ├── es_document/      # Elasticsearch Documents
│   │   │   │   ├── es_repository/    # Elasticsearch Repositories
│   │   │   │   ├── exception/        # Exception Handling
│   │   │   │   ├── mapper/           # MapStruct Mappers
│   │   │   │   ├── repository/       # JPA Repositories
│   │   │   │   ├── scheduler/        # Scheduled Tasks
│   │   │   │   ├── service/          # Business Logic
│   │   │   │   └── util/             # Utilities
│   │   │   └── resources/
│   │   │       └── application.yml   # Application Configuration
│   │   └── test/                     # Unit Tests
│   ├── docker/
│   │   └── mysql/
│   │       └── init.sql              # Database Initialization
│   ├── dockerfile                    # Dockerfile cho backend
│   ├── docker-compose.yml            # Docker Compose cho backend
│   └── pom.xml                       # Maven Dependencies
│
├── eLibrary_UI/                      # Frontend React
│   ├── src/
│   │   ├── components/               # React Components
│   │   │   ├── AuthForm/            # Authentication Forms
│   │   │   ├── Book/                # Book Components
│   │   │   ├── Home/                # Home Components
│   │   │   └── UserProfile/         # User Profile Components
│   │   ├── pages/                   # Page Components
│   │   ├── utils/                   # Utility Components
│   │   ├── verification/            # OAuth & Payment Pages
│   │   └── test/                    # Test Files
│   ├── dockerfile                    # Dockerfile cho frontend
│   ├── nginx.conf                    # Nginx Configuration
│   ├── vite.config.js                # Vite Configuration
│   └── package.json                  # NPM Dependencies
│
├── docker-compose.yml                # Docker Compose chính (tất cả services)
└── README.md                         # File này
```

## 📋 Yêu cầu hệ thống

- **Java**: JDK 21 hoặc cao hơn
- **Node.js**: 18.x hoặc cao hơn
- **Maven**: 3.8+ (hoặc sử dụng Maven Wrapper)
- **Docker**: 20.10+ và Docker Compose 2.0+
- **MySQL**: 8.1.0+ (hoặc sử dụng Docker)
- **Redis**: Latest (hoặc sử dụng Docker)
- **Elasticsearch**: 8.15.3+ (hoặc sử dụng Docker)

## 🚀 Cài đặt và Chạy dự án

### Cách 1: Chạy với Docker Compose (Khuyến nghị)

1. **Clone repository**
```bash
git clone <repository-url>
cd Doancnpm
```

2. **Tạo file `.env` cho backend**
```bash
cd eLibrary_service
# Tạo file .env với các biến môi trường cần thiết (xem phần Environment Variables)
```

3. **Chạy tất cả services với Docker Compose**
```bash
cd ..
docker-compose up -d
```

Các services sẽ chạy trên các port:
- **Backend API**: http://localhost:8080
- **Frontend**: http://localhost:5173
- **MySQL**: localhost:3306
- **Redis**: localhost:6379
- **Elasticsearch**: http://localhost:9200
- **Kibana**: http://localhost:5601

4. **Kiểm tra logs**
```bash
docker-compose logs -f
```

### Cách 2: Chạy thủ công (Development)

#### Backend

1. **Cài đặt MySQL, Redis, Elasticsearch**
   - Hoặc chạy chỉ các services này với Docker:
   ```bash
   docker-compose up -d elibrary-db elibrary-redis elibrary-es
   ```

2. **Cấu hình file `.env`**
   ```bash
   cd eLibrary_service
   # Tạo file .env với các biến môi trường
   ```

3. **Chạy Spring Boot**
   ```bash
   # Sử dụng Maven Wrapper
   ./mvnw spring-boot:run
   
   # Hoặc sử dụng Maven
   mvn spring-boot:run
   ```

#### Frontend

1. **Cài đặt dependencies**
   ```bash
   cd eLibrary_UI
   npm install
   ```

2. **Chạy development server**
   ```bash
   npm run dev
   ```

3. **Build production**
   ```bash
   npm run build
   ```

## 🔧 Biến môi trường

Tạo file `.env` trong thư mục `eLibrary_service/` với các biến sau:

```env
# Database
SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/eLibrary_service
SPRING_DATASOURCE_USERNAME=root
SPRING_DATASOURCE_PASSWORD=root

# Redis
SPRING_DATA_REDIS_HOST=localhost
SPRING_DATA_REDIS_PORT=6379

# Elasticsearch
SPRING_ELASTICSEARCH_URIS=http://localhost:9200

# JWT
JWT_SIGNER_KEY=your-secret-key-here-minimum-256-bits

# Email (Gmail)
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD=your-app-password

# OAuth2 - Google
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# OAuth2 - GitHub
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret

# VNPay
VNPAY_TMN_CODE=your-tmn-code
VNPAY_HASH_SECRET=your-hash-secret
```

## 📚 API Documentation

Sau khi chạy backend, truy cập Swagger UI tại:
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **API Docs (JSON)**: http://localhost:8080/api-docs

## 🧪 Testing

### Backend Tests
```bash
cd eLibrary_service
./mvnw test
```

### Frontend Tests
```bash
cd eLibrary_UI
npm test              # Chạy tests một lần
npm run test:watch    # Chạy tests ở chế độ watch
npm run test:ui       # Chạy tests với UI
```

## 🌿 Cấu trúc Branch

Dự án có 3 branch chính:

- **`feature/core`**: Chứa logic backend (Spring Boot)
- **`UI`**: Chứa giao diện frontend (React)
- **`test`**: Chứa tất cả các chức năng và được chạy thông qua `docker-compose.yml`

## 📦 API Endpoints chính

### Authentication
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/register` - Đăng ký
- `POST /api/auth/refresh` - Làm mới token
- `POST /api/auth/logout` - Đăng xuất
- `GET /oauth2/authorization/{provider}` - OAuth2 login (google, github)

### Books
- `GET /api/books` - Lấy danh sách sách
- `GET /api/books/{id}` - Lấy chi tiết sách
- `GET /api/books/search` - Tìm kiếm sách
- `GET /api/books/new` - Lấy sách mới nhất
- `GET /api/books/filter` - Lọc sách

### Borrow
- `POST /api/borrow` - Mượn sách
- `GET /api/borrow` - Lấy danh sách mượn
- `POST /api/borrow/renew` - Gia hạn mượn

### Categories
- `GET /api/categories` - Lấy danh sách danh mục

### Payment
- `POST /api/payment/create` - Tạo thanh toán
- `POST /api/payment/vnpay-callback` - Callback từ VNPay

### Subscription
- `GET /api/subscription-plans` - Lấy danh sách gói đăng ký
- `POST /api/user-subscription/subscribe` - Đăng ký gói

### User
- `GET /api/users/profile` - Lấy thông tin profile
- `PUT /api/users/profile` - Cập nhật profile

## 🔐 Bảo mật

- JWT Authentication với access token và refresh token
- OAuth2 với Google và GitHub
- Spring Security cho authorization
- Password encryption với BCrypt
- CORS configuration
- Email verification với OTP

## 📝 Lưu ý

- Đảm bảo các services (MySQL, Redis, Elasticsearch) đã chạy trước khi start backend
- Cần cấu hình đúng các biến môi trường trong file `.env`
- VNPay cần cấu hình IPN URL (có thể sử dụng ngrok cho development)
- Elasticsearch cần thời gian khởi động, đợi vài giây sau khi container start


## 📄 License

Dự án này được phát triển cho mục đích học tập và nghiên cứu.

## 👥 Tác giả

Dự án được phát triển bởi:
1. Nguyễn Vũ Hoàng - 2311069
2. Đoàn Minh Đức - 2310767
3. Cấn Hoàng Hà - 2310836
4. Ngọ Văn Hiệp - 2311007
5. Lê Vũ Minh Hiếu - 2310953
---


