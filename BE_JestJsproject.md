

# Rancangan Backend LaundryKu Management System

## 1. Arsitektur Backend

### 1.1 High-Level Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway                                │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │ Auth    │ │ Rate    │ │ Monitor │ │ Cache   │ │ Router  │    │
│  │ Service │ │ Limit   │ │ ing     │ │ Layer   │ │ Service │    │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘    │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌───────────────────────────────────────────────────────────────────┐
│                   Microservices Layer                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────────┐ │
│  │ Order       │ │ Customer    │ │ Payment     │ │ Notification │ │
│  │ Service     │ │ Service     │ │ Service     │ │ Service      │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────────┘ │
│                                                                   │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────────┐ │
│  │ Analytics   │ │ Report      │ │ Integration │ │ Inventory    │ │
│  │ Service     │ │ Service     │ │ Service     │ │ Service      │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────────┘ │
└───────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────┐
│                    Data Layer                                    │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │ Primary     │ │ Cache       │ │ Search      │ │ Time-Series │ │
│  │ Database    │ │ Layer       │ │ Engine      │ │ Database    │ │
│  │ (PostgreSQL)│ │ (Redis)     │ │ (Elastic)   │ │ (InfluxDB)  │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### 1.2 Teknologi Utama
- **Framework**: NestJS 10+ dengan TypeScript
- **Runtime**: Node.js 18+
- **Database**: PostgreSQL 15+ dengan Prisma ORM
- **Cache**: Redis 7+
- **Search**: Elasticsearch 8+
- **Message Queue**: Bull Queue (Redis-based)
- **Authentication**: JWT + OAuth 2.0
- **Documentation**: Swagger/OpenAPI

## 2. Struktur Folder Backend

```
laundryku-backend/
├── src/
│   ├── common/                  // Modul umum yang digunakan di seluruh aplikasi
│   │   ├── constants/          // Konstanta aplikasi
│   │   ├── decorators/         // Decorator kustom
│   │   ├── exceptions/         // Exception kustom
│   │   ├── filters/            // Filter untuk error handling, logging, dll
│   │   ├── interceptors/       // Interceptor untuk transformasi, caching, dll
│   │   ├── interfaces/         // Interface TypeScript
│   │   ├── pipes/              // Pipe untuk validasi dan transformasi data
│   │   └── utils/              // Fungsi utilitas
│   ├── config/                 // Konfigurasi aplikasi
│   │   ├── app.config.ts      // Konfigurasi utama aplikasi
│   │   ├── database.config.ts // Konfigurasi database
│   │   └── index.ts           // Ekspor semua konfigurasi
│   ├── modules/               // Modul-modul fitur aplikasi
│   │   ├── auth/              // Modul autentikasi
│   │   │   ├── dto/           // Data Transfer Objects
│   │   │   ├── entities/      // Entitas database
│   │   │   ├── strategies/    // Strategi autentikasi (JWT, OAuth, dll)
│   │   │   ├── auth.controller.ts
│   │   │   ├── auth.module.ts
│   │   │   ├── auth.service.ts
│   │   │   └── auth.repository.ts
│   │   ├── users/             // Modul manajemen pengguna
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── users.controller.ts
│   │   │   ├── users.module.ts
│   │   │   ├── users.service.ts
│   │   │   └── users.repository.ts
│   │   ├── laundries/         // Modul manajemen laundry
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── laundries.controller.ts
│   │   │   ├── laundries.module.ts
│   │   │   ├── laundries.service.ts
│   │   │   └── laundries.repository.ts
│   │   ├── customers/         // Modul manajemen pelanggan
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── customers.controller.ts
│   │   │   ├── customers.module.ts
│   │   │   ├── customers.service.ts
│   │   │   └── customers.repository.ts
│   │   ├── orders/            // Modul manajemen pesanan
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── orders.controller.ts
│   │   │   ├── orders.module.ts
│   │   │   ├── orders.service.ts
│   │   │   └── orders.repository.ts
│   │   ├── services/          // Modul manajemen layanan
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── services.controller.ts
│   │   │   ├── services.module.ts
│   │   │   ├── services.service.ts
│   │   │   └── services.repository.ts
│   │   ├── payments/          // Modul pembayaran
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── payments.controller.ts
│   │   │   ├── payments.module.ts
│   │   │   ├── payments.service.ts
│   │   │   └── payments.repository.ts
│   │   ├── subscriptions/     // Modul langganan
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── subscriptions.controller.ts
│   │   │   ├── subscriptions.module.ts
│   │   │   ├── subscriptions.service.ts
│   │   │   └── subscriptions.repository.ts
│   │   ├── analytics/         // Modul analitik
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── analytics.controller.ts
│   │   │   ├── analytics.module.ts
│   │   │   ├── analytics.service.ts
│   │   │   └── analytics.repository.ts
│   │   ├── notifications/     // Modul notifikasi
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── notifications.controller.ts
│   │   │   ├── notifications.module.ts
│   │   │   ├── notifications.service.ts
│   │   │   └── notifications.repository.ts
│   │   ├── integrations/      // Modul integrasi dengan pihak ketiga
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── integrations.controller.ts
│   │   │   ├── integrations.module.ts
│   │   │   ├── integrations.service.ts
│   │   │   └── integrations.repository.ts
│   │   ├── inventory/         // Modul inventaris
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── inventory.controller.ts
│   │   │   ├── inventory.module.ts
│   │   │   ├── inventory.service.ts
│   │   │   └── inventory.repository.ts
│   │   └── reports/           // Modul laporan
│   │       ├── dto/
│   │       ├── entities/
│   │       ├── reports.controller.ts
│   │       ├── reports.module.ts
│   │       ├── reports.service.ts
│   │       └── reports.repository.ts
│   ├── database/              // Konfigurasi dan setup database
│   │   ├── migrations/        // Migrasi database
│   │   ├── seeds/             // Data seeding
│   │   └── prisma/            // Schema dan client Prisma
│   ├── mail/                  // Template dan konfigurasi email
│   │   ├── templates/         // Template email
│   │   └── mail.service.ts    // Service untuk mengirim email
│   ├── redis/                 // Konfigurasi dan utilitas Redis
│   │   └── redis.service.ts   // Service untuk operasi Redis
│   ├── websocket/             // Konfigurasi WebSocket
│   │   ├── gateway.ts         // WebSocket Gateway
│   │   ├── events.ts          // Event handlers
│   │   └── adapters.ts        // Adapters untuk WebSocket
│   ├── app.controller.ts      // Controller root
│   ├── app.module.ts          // Module root
│   ├── app.service.ts         // Service root
│   └── main.ts                // Entry point aplikasi
├── test/                      // File testing
│   ├── e2e/                   // End-to-end tests
│   └── unit/                  // Unit tests
├── .env.example               // Contoh file environment
├── .eslintrc.js               // Konfigurasi ESLint
├── .gitignore                 // File yang diabaikan Git
├── .prettierrc                // Konfigurasi Prettier
├── Dockerfile                 // Konfigurasi Docker
├── docker-compose.yml         // Konfigurasi Docker Compose
├── jest.config.js             // Konfigurasi Jest
├── nest-cli.json              // Konfigurasi Nest CLI
├── package.json               // Dependencies dan scripts
├── pm2.config.js              // Konfigurasi PM2
├── README.md                  // Dokumentasi proyek
├── tsconfig.build.json        // Konfigurasi TypeScript untuk build
└── tsconfig.json              // Konfigurasi TypeScript
```

## 3. Library yang Dibutuhkan

### 3.1 Dependencies Utama
```json
{
  "dependencies": {
    "@nestjs/common": "^10.0.0",
    "@nestjs/core": "^10.0.0",
    "@nestjs/platform-express": "^10.0.0",
    "@nestjs/config": "^3.0.0",
    "@nestjs/jwt": "^10.1.0",
    "@nestjs/passport": "^10.0.0",
    "@nestjs/throttler": "^4.0.0",
    "@nestjs/swagger": "^7.1.8",
    "@nestjs/serve-static": "^4.0.0",
    "@nestjs/websockets": "^10.0.0",
    "@nestjs/platform-socket.io": "^10.0.0",
    "reflect-metadata": "^0.1.13",
    "rxjs": "^7.8.1",
    "class-validator": "^0.14.0",
    "class-transformer": "^0.5.1",
    "bcrypt": "^5.1.0",
    "passport": "^0.6.0",
    "passport-jwt": "^4.0.1",
    "passport-local": "^1.0.0",
    "passport-google-oauth20": "^2.0.0",
    "passport-facebook": "^3.0.0",
    "jsonwebtoken": "^9.0.0",
    "uuid": "^9.0.0",
    "dayjs": "^1.11.9",
    "lodash": "^4.17.21",
    "compression": "^1.7.4",
    "helmet": "^7.0.0",
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "morgan": "^1.10.0"
  }
}
```

### 3.2 Database dan ORM
```json
{
  "dependencies": {
    "@prisma/client": "^5.0.0",
    "prisma": "^5.0.0"
  }
}
```

### 3.3 Cache dan Message Queue
```json
{
  "dependencies": {
    "redis": "^4.6.7",
    "cache-manager": "^5.2.3",
    "cache-manager-redis-store": "^3.0.1",
    "bull": "^4.10.4",
    "@nestjs/bull": "^10.0.1",
    "@nestjs/cache-manager": "^2.1.0"
  }
}
```

### 3.4 Email dan Notifikasi
```json
{
  "dependencies": {
    "@nestjs-modules/mailer": "^1.9.1",
    "nodemailer": "^6.9.4",
    "handlebars": "^4.7.8",
    "twilio": "^4.14.0",
    "firebase-admin": "^11.10.1"
  }
}
```

### 3.5 File Upload dan Storage
```json
{
  "dependencies": {
    "@nestjs/terminus": "^10.1.1",
    "multer": "^1.4.5-lts.1",
    "@types/multer": "^1.4.7",
    "aws-sdk": "^2.1446.0",
    "sharp": "^0.32.4"
  }
}
```

### 3.6 Monitoring dan Logging
```json
{
  "dependencies": {
    "winston": "^3.10.0",
    "nest-winston": "^1.9.3",
    "@opentelemetry/api": "^1.4.1",
    "@opentelemetry/auto-instrumentations-node": "^0.39.0",
    "@opentelemetry/exporter-jaeger": "^1.17.0",
    "@opentelemetry/exporter-prometheus": "^0.41.0",
    "@opentelemetry/instrumentation": "^0.41.0",
    "@opentelemetry/resources": "^1.17.0",
    "@opentelemetry/sdk-node": "^0.41.0",
    "@opentelemetry/semantic-conventions": "^1.17.0",
    "prom-client": "^14.2.0"
  }
}
```

### 3.7 Payment Gateway
```json
{
  "dependencies": {
    "midtrans-client": "^1.3.1",
    "xendit-node": "^2.6.0"
  }
}
```

### 3.8 Utility dan Helper
```json
{
  "dependencies": {
    "joi": "^17.9.2",
    "zod": "^3.22.2",
    "dotenv": "^16.3.1",
    "dotenv-expand": "^10.0.0",
    "cross-env": "^7.0.3",
    "fs-extra": "^11.1.1",
    "moment": "^2.29.4"
  }
}
```

### 3.9 Development Dependencies
```json
{
  "devDependencies": {
    "@nestjs/cli": "^10.1.10",
    "@nestjs/schematics": "^10.0.0",
    "@nestjs/testing": "^10.0.0",
    "@types/express": "^4.17.17",
    "@types/jest": "^29.5.3",
    "@types/node": "^20.4.5",
    "@types/supertest": "^2.0.12",
    "@types/bcrypt": "^5.0.0",
    "@types/jsonwebtoken": "^9.0.2",
    "@types/lodash": "^4.14.195",
    "@types/passport-jwt": "^3.0.9",
    "@types/passport-local": "^1.0.35",
    "@types/passport-google-oauth20": "^2.0.11",
    "@types/passport-facebook": "^3.0.0",
    "@types/uuid": "^9.0.2",
    "@types/compression": "^1.7.2",
    "@types/cors": "^2.8.13",
    "@types/morgan": "^1.9.4",
    "@types/multer": "^1.4.7",
    "@types/fs-extra": "^11.0.1",
    "@typescript-eslint/eslint-plugin": "^6.2.0",
    "@typescript-eslint/parser": "^6.2.0",
    "eslint": "^8.45.0",
    "eslint-config-prettier": "^8.8.0",
    "eslint-plugin-prettier": "^5.0.0",
    "jest": "^29.6.1",
    "prettier": "^3.0.0",
    "supertest": "^6.3.3",
    "ts-jest": "^29.1.1",
    "ts-loader": "^9.4.4",
    "ts-node": "^10.9.1",
    "tsconfig-paths": "^4.2.0",
    "typescript": "^5.1.6"
  }
}
```

## 4. Konfigurasi Dasar

### 4.1 package.json
```json
{
  "name": "laundryku-backend",
  "version": "1.0.0",
  "description": "Backend for LaundryKu Management System",
  "author": "LaundryKu Team",
  "private": true,
  "license": "UNLICENSED",
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json",
    "db:generate": "prisma generate",
    "db:push": "prisma db push",
    "db:migrate": "prisma migrate dev",
    "db:studio": "prisma studio",
    "db:seed": "ts-node prisma/seed.ts",
    "db:reset": "prisma migrate reset",
    "docs:generate": "compodoc -p tsconfig.json -s",
    "docs:serve": "compodoc -s"
  }
}
```

### 4.2 .env.example
```env
# Application
NODE_ENV=development
PORT=3000
API_PREFIX=api/v1
API_VERSION=1.0

# Database
DATABASE_URL="postgresql://username:password@localhost:5432/laundryku"

# JWT
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=24h
JWT_REFRESH_SECRET=your-refresh-secret-key
JWT_REFRESH_EXPIRES_IN=7d

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
REDIS_DB=0

# Email
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USER=your-email@example.com
MAIL_PASS=your-email-password

# Cloud Storage
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_REGION=us-east-1
AWS_S3_BUCKET=laundryku-bucket

# Payment Gateway
MIDTRANS_SERVER_KEY=your-midtrans-server-key
MIDTRANS_CLIENT_KEY=your-midtrans-client-key
XENDIT_SECRET_KEY=your-xendit-secret-key

# Firebase
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY_ID=your-private-key-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=your-client-email
FIREBASE_CLIENT_ID=your-client-id
FIREBASE_AUTH_URI=https://accounts.google.com/o/oauth2/auth
FIREBASE_TOKEN_URI=https://oauth2.googleapis.com/token
FIREBASE_AUTH_PROVIDER_X509_CERT_URL=https://www.googleapis.com/oauth2/v1/certs
FIREBASE_CLIENT_X509_CERT_URL=https://www.googleapis.com/robot/v1/metadata/x509/your-client-email

# Twilio
TWILIO_ACCOUNT_SID=your-account-sid
TWILIO_AUTH_TOKEN=your-auth-token
TWILIO_PHONE_NUMBER=+1234567890

# Google OAuth
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# Facebook OAuth
FACEBOOK_APP_ID=your-facebook-app-id
FACEBOOK_APP_SECRET=your-facebook-app-secret

# Monitoring
SENTRY_DSN=your-sentry-dsn
```

## 5. Penjelasan Struktur

### 5.1 Struktur Folder
- **src/common**: Berisi komponen yang digunakan di seluruh aplikasi seperti decorators, exceptions, filters, interceptors, pipes, dan utilities.
- **src/config**: Berisi konfigurasi aplikasi yang digunakan di seluruh modul.
- **src/modules**: Berisi modul-modul fitur aplikasi, setiap modul memiliki struktur yang konsisten dengan controller, service, repository, DTO, dan entities.
- **src/database**: Berisi konfigurasi database, migrasi, seeding, dan schema Prisma.
- **src/mail**: Berisi template email dan service untuk mengirim email.
- **src/redis**: Berisi konfigurasi dan service untuk operasi Redis.
- **src/websocket**: Berisi konfigurasi WebSocket untuk real-time communication.
- **test**: Berisi file testing untuk unit tests dan e2e tests.

### 5.2 Library yang Dibutuhkan
- **Core NestJS**: Library inti untuk membangun aplikasi NestJS.
- **Database dan ORM**: Prisma sebagai ORM untuk PostgreSQL.
- **Cache dan Message Queue**: Redis untuk caching dan Bull untuk message queue.
- **Email dan Notifikasi**: NestJS Mailer untuk email, Twilio untuk SMS, dan Firebase untuk push notifications.
- **File Upload dan Storage**: Multer untuk file upload, AWS SDK untuk S3 storage, dan Sharp untuk image processing.
- **Monitoring dan Logging**: Winston untuk logging, OpenTelemetry untuk observability, dan Prometheus untuk metrics.
- **Payment Gateway**: Midtrans dan Xendit untuk pembayaran.
- **Utility dan Helper**: Joi/Zod untuk validasi, dotenv untuk environment variables, dan lainnya.

### 5.3 Konfigurasi Dasar
- **package.json**: Berisi dependencies, scripts untuk menjalankan aplikasi, testing, dan database operations.
- **.env.example**: Contoh file environment variables yang dibutuhkan aplikasi.

Dengan struktur dan library ini, backend LaundryKu Management System akan memiliki fondasi yang kuat untuk pengembangan lebih lanjut. Struktur ini mengikuti best practices NestJS dan memungkinkan skalabilitas, maintainability, dan testability yang baik.