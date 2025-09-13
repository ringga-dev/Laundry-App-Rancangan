

# Rancangan Backend LaundryKu Management System dengan Kotlin & Spring Boot 4

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
- **Framework**: Spring Boot 3.2.x dengan Kotlin
- **Runtime**: Java 17+ (Kotlin 1.9.x)
- **Database**: PostgreSQL 15+ dengan Spring Data JPA
- **Cache**: Redis 7+ dengan Spring Data Redis
- **Search**: Elasticsearch 8+ dengan Spring Data Elasticsearch
- **Message Queue**: RabbitMQ dengan Spring AMQP
- **Authentication**: JWT + OAuth 2.0
- **Documentation**: OpenAPI 3 dengan SpringDoc

## 2. Struktur Folder Backend

```
laundryku-backend/
├── src/
│   ├── main/
│   │   ├── kotlin/
│   │   │   └── com/laundryku/
│   │   │       ├── LaundryKuApplication.kt
│   │   │       ├── config/                 // Konfigurasi aplikasi
│   │   │       │   ├── AppConfig.kt
│   │   │       │   ├── DatabaseConfig.kt
│   │   │       │   ├── RedisConfig.kt
│   │   │       │   ├── SecurityConfig.kt
│   │   │       │   ├── SwaggerConfig.kt
│   │   │       │   └── WebSocketConfig.kt
│   │   │       ├── common/                // Komponen umum
│   │   │       │   ├── constants/          // Konstanta
│   │   │       │   ├── exception/         // Exception handling
│   │   │       │   ├── interceptor/       // Interceptor
│   │   │       │   ├── util/              // Utility functions
│   │   │       │   └── dto/               // DTO umum
│   │   │       ├── modules/               // Modul-modul fitur
│   │   │       │   ├── auth/              // Modul autentikasi
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   └── AuthModule.kt
│   │   │       │   ├── user/              // Modul user
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── UserModule.kt
│   │   │       │   ├── laundry/           // Modul laundry
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── LaundryModule.kt
│   │   │       │   ├── customer/          // Modul customer
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── CustomerModule.kt
│   │   │       │   ├── order/             // Modul order
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── OrderModule.kt
│   │   │       │   ├── service/           // Modul service laundry
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── ServiceModule.kt
│   │   │       │   ├── payment/           // Modul payment
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── PaymentModule.kt
│   │   │       │   ├── subscription/      // Modul subscription
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── SubscriptionModule.kt
│   │   │       │   ├── analytics/         // Modul analytics
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   └── AnalyticsModule.kt
│   │   │       │   ├── notification/      // Modul notification
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── NotificationModule.kt
│   │   │       │   ├── integration/       // Modul integrasi
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── IntegrationModule.kt
│   │   │       │   ├── inventory/         // Modul inventory
│   │   │       │   │   ├── controller/
│   │   │       │   │   ├── service/
│   │   │       │   │   ├── repository/
│   │   │       │   │   ├── dto/
│   │   │       │   │   ├── entity/
│   │   │       │   │   └── InventoryModule.kt
│   │   │       │   └── report/            // Modul report
│   │   │       │       ├── controller/
│   │   │       │       ├── service/
│   │   │       │       ├── repository/
│   │   │       │       ├── dto/
│   │   │       │       └── ReportModule.kt
│   │   │       ├── security/              // Security configuration
│   │   │       │   ├── jwt/
│   │   │       │   │   ├── JwtTokenFilter.kt
│   │   │       │   │   ├── JwtTokenProvider.kt
│   │   │       │   │   └── JwtUserDetailsService.kt
│   │   │       │   └── UserPrincipal.kt
│   │   │       └── websocket/            // WebSocket configuration
│   │   │           ├── SocketHandler.kt
│   │   │           └── SocketConfig.kt
│   │   └── resources/
│   │       ├── application.yml           // Konfigurasi aplikasi
│   │       ├── application-dev.yml      // Konfigurasi development
│   │       ├── application-prod.yml     // Konfigurasi production
│   │       ├── db/
│   │       │   └── migration/            // Database migration
│   │       └── templates/               // Template email
│   └── test/
│       └── kotlin/
│           └── com/laundryku/
│               ├── controller/
│               ├── service/
│               └── repository/
├── .env.example                        // Contoh file environment
├── .gitignore                         // File yang diabaikan Git
├── build.gradle.kts                   // Konfigurasi build Gradle
├── gradlew                             // Gradle wrapper
├── gradlew.bat                         // Gradle wrapper untuk Windows
├── settings.gradle.kts                 // Konfigurasi settings Gradle
├── README.md                           // Dokumentasi proyek
└── Dockerfile                          // Konfigurasi Docker
```

## 3. Library yang Dibutuhkan (build.gradle.kts)

```kotlin
plugins {
    id("org.springframework.boot") version "3.2.0"
    id("io.spring.dependency-management") version "1.1.0"
    kotlin("jvm") version "1.9.20"
    kotlin("plugin.spring") version "1.9.20"
    kotlin("plugin.jpa") version "1.9.20"
    kotlin("plugin.noarg") version "1.9.20"
    kotlin("plugin.allopen") version "1.9.20"
}

group = "com.laundryku"
version = "1.0.0"

java {
    sourceCompatibility = JavaVersion.VERSION_17
}

repositories {
    mavenCentral()
}

dependencies {
    // Spring Boot Starters
    implementation("org.springframework.boot:spring-boot-starter-web")
    implementation("org.springframework.boot:spring-boot-starter-data-jpa")
    implementation("org.springframework.boot:spring-boot-starter-security")
    implementation("org.springframework.boot:spring-boot-starter-validation")
    implementation("org.springframework.boot:spring-boot-starter-websocket")
    implementation("org.springframework.boot:spring-boot-starter-cache")
    implementation("org.springframework.boot:spring-boot-starter-mail")
    implementation("org.springframework.boot:spring-boot-starter-actuator")

    // Kotlin
    implementation("com.fasterxml.jackson.module:jackson-module-kotlin")
    implementation("org.jetbrains.kotlin:kotlin-reflect")
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")

    // Database
    implementation("org.postgresql:postgresql")
    implementation("org.flywaydb:flyway-core")
    implementation("com.zaxxer:HikariCP")

    // Redis
    implementation("org.springframework.boot:spring-boot-starter-data-redis")
    implementation("redis.clients:jedis")

    // JWT
    implementation("io.jsonwebtoken:jjwt-api:0.12.3")
    runtimeOnly("io.jsonwebtoken:jjwt-impl:0.12.3")
    runtimeOnly("io.jsonwebtoken:jjwt-jackson:0.12.3")

    // Swagger/OpenAPI
    implementation("org.springdoc:springdoc-openapi-starter-webmvc-ui:2.3.0")

    // Logging
    implementation("io.github.oshai:kotlin-logging-jvm:5.1.0")

    // JSON Processing
    implementation("com.fasterxml.jackson.core:jackson-databind")
    implementation("com.fasterxml.jackson.datatype:jackson-datatype-jsr310")
    implementation("com.fasterxml.jackson.module:jackson-module-kotlin")

    // Utilities
    implementation("org.apache.commons:commons-lang3:3.14.0")
    implementation("commons-codec:commons-codec:1.16.0")
    implementation("org.apache.commons:commons-collections4:4.4")

    // Date and Time
    implementation("com.github.bastienpaul:java-time-range:1.3.0")

    // Payment Gateway
    implementation("com.midtrans:java-library:1.3.1")
    implementation("com.xendit:xendit-java:2.6.0")

    // Email Template
    implementation("org.springframework.boot:spring-boot-starter-thymeleaf")

    // AWS SDK
    implementation("software.amazon.awssdk:s3:2.21.0")
    implementation("software.amazon.awssdk:ses:2.21.0")

    // Firebase
    implementation("com.google.firebase:firebase-admin:9.2.0")

    // Twilio
    implementation("com.twilio.sdk:twilio:9.14.1")

    // OAuth2
    implementation("org.springframework.boot:spring-boot-starter-oauth2-client")

    // Monitoring
    implementation("io.micrometer:micrometer-registry-prometheus")
    implementation("io.micrometer:micrometer-tracing-bridge-brave")
    implementation("io.zipkin.reporter2:zipkin-reporter-brave")

    // Test
    testImplementation("org.springframework.boot:spring-boot-starter-test")
    testImplementation("org.springframework.security:spring-security-test")
    testImplementation("org.testcontainers:junit-jupiter")
    testImplementation("org.testcontainers:postgresql")
    testImplementation("com.ninja-squad:springmockk:4.0.2")
    testImplementation("io.mockk:mockk:1.13.8")
}

tasks.withType<KotlinCompile> {
    kotlinOptions {
        freeCompilerArgs += "-Xjsr305=strict"
        jvmTarget = "17"
    }
}

tasks.withType<Test> {
    useJUnitPlatform()
}
```

## 4. Konfigurasi Dasar

### 4.1 application.yml
```yaml
spring:
  application:
    name: laundryku-backend
  profiles:
    active: dev
  jpa:
    hibernate:
      ddl-auto: none
    show-sql: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true
    database-platform: org.hibernate.dialect.PostgreSQLDialect
  flyway:
    enabled: true
    locations: classpath:db/migration
    baseline-on-migrate: true
  datasource:
    url: ${DB_URL:jdbc:postgresql://localhost:5432/laundryku}
    username: ${DB_USERNAME:postgres}
    password: ${DB_PASSWORD:password}
    driver-class-name: org.postgresql.Driver
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      idle-timeout: 30000
      max-lifetime: 1800000
      connection-timeout: 30000
  redis:
    host: ${REDIS_HOST:localhost}
    port: ${REDIS_PORT:6379}
    password: ${REDIS_PASSWORD:}
    database: ${REDIS_DB:0}
    timeout: 2000ms
    lettuce:
      pool:
        max-active: 8
        max-idle: 8
        min-idle: 0
        max-wait: -1ms
  cache:
    type: redis
    redis:
      time-to-live: 600000
      cache-null-values: false
  mail:
    host: ${MAIL_HOST:smtp.example.com}
    port: ${MAIL_PORT:587}
    username: ${MAIL_USERNAME:your-email@example.com}
    password: ${MAIL_PASSWORD:your-email-password}
    properties:
      mail:
        smtp:
          auth: true
          starttls:
            enable: true
  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 10MB
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher

server:
  port: ${SERVER_PORT:8080}
  servlet:
    context-path: /api/v1

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: always
  metrics:
    export:
      prometheus:
        enabled: true
  tracing:
    sampling:
      probability: 1.0

logging:
  level:
    com.laundryku: DEBUG
    org.springframework.security: DEBUG

springdoc:
  api-docs:
    path: /api-docs
  swagger-ui:
    path: /swagger-ui.html

app:
  jwt:
    secret: ${JWT_SECRET:mySecretKey}
    expiration: ${JWT_EXPIRATION:86400000} # 24 hours
    refresh-expiration: ${JWT_REFRESH_EXPIRATION:604800000} # 7 days
  file:
    upload-dir: ${FILE_UPLOAD_DIR:uploads}
    max-size: ${FILE_MAX_SIZE:10485760} # 10MB
  cors:
    allowed-origins: ${CORS_ALLOWED_ORIGINS:http://localhost:3000,http://localhost:8080}
    allowed-methods: ${CORS_ALLOWED_METHODS:GET,POST,PUT,DELETE,OPTIONS}
    allowed-headers: ${CORS_ALLOWED_HEADERS:*}
    allow-credentials: ${CORS_ALLOW_CREDENTIALS:true}
```

### 4.2 application-dev.yml
```yaml
spring:
  jpa:
    show-sql: true
    hibernate:
      ddl-auto: update
  h2:
    console:
      enabled: true
logging:
  level:
    com.laundryku: DEBUG
    org.springframework.security: DEBUG
    org.hibernate.SQL: DEBUG
    org.hibernate.type.descriptor.sql.BasicBinder: TRACE
```

### 4.3 application-prod.yml
```yaml
spring:
  jpa:
    show-sql: false
    hibernate:
      ddl-auto: none
logging:
  level:
    com.laundryku: INFO
    org.springframework.security: WARN
    org.hibernate.SQL: WARN
```

### 4.4 .env.example
```env
# Database
DB_URL=jdbc:postgresql://localhost:5432/laundryku
DB_USERNAME=postgres
DB_PASSWORD=password

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
REDIS_DB=0

# JWT
JWT_SECRET=mySecretKey
JWT_EXPIRATION=86400000
JWT_REFRESH_EXPIRATION=604800000

# Server
SERVER_PORT=8080

# Mail
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USERNAME=your-email@example.com
MAIL_PASSWORD=your-email-password

# File Upload
FILE_UPLOAD_DIR=uploads
FILE_MAX_SIZE=10485760

# CORS
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8080
CORS_ALLOWED_METHODS=GET,POST,PUT,DELETE,OPTIONS
CORS_ALLOWED_HEADERS=*
CORS_ALLOW_CREDENTIALS=true

# AWS
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_REGION=us-east-1
AWS_S3_BUCKET=laundryku-bucket

# Midtrans
MIDTRANS_SERVER_KEY=your-midtrans-server-key
MIDTRANS_CLIENT_KEY=your-midtrans-client-key

# Xendit
XENDIT_SECRET_KEY=your-xendit-secret-key

# Firebase
FIREBASE_SERVICE_ACCOUNT_KEY=your-firebase-service-account-key

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
```

## 5. Penjelasan Struktur

### 5.1 Struktur Folder
- **src/main/kotlin/com/laundryku**: Berisi kode sumber aplikasi.
    - **config**: Konfigurasi aplikasi seperti database, security, redis, swagger, dan websocket.
    - **common**: Komponen umum yang digunakan di seluruh aplikasi.
    - **modules**: Modul-modul fitur aplikasi, setiap modul memiliki struktur yang konsisten dengan controller, service, repository, dto, dan entity.
    - **security**: Konfigurasi keamanan seperti JWT dan user principal.
    - **websocket**: Konfigurasi WebSocket untuk real-time communication.
- **src/main/resources**: Berisi file konfigurasi dan template.
    - **application.yml**: Konfigurasi utama aplikasi.
    - **application-dev.yml**: Konfigurasi untuk environment development.
    - **application-prod.yml**: Konfigurasi untuk environment production.
    - **db/migration**: File migrasi database menggunakan Flyway.
    - **templates**: Template email menggunakan Thymeleaf.
- **src/test/kotlin/com/laundryku**: Berisi kode testing.

### 5.2 Library yang Dibutuhkan
- **Spring Boot Starters**: Starter untuk web, data jpa, security, websocket, cache, mail, dan actuator.
- **Kotlin**: Plugin dan library untuk dukungan Kotlin di Spring Boot.
- **Database**: PostgreSQL driver, Flyway untuk migrasi, dan HikariCP untuk connection pool.
- **Redis**: Spring Data Redis dan Jedis client.
- **JWT**: JJWT library untuk token management.
- **Swagger/OpenAPI**: Springdoc OpenAPI untuk dokumentasi API.
- **Logging**: Kotlin-logging untuk logging yang lebih baik di Kotlin.
- **JSON Processing**: Jackson untuk JSON processing.
- **Utilities**: Apache Commons untuk utilitas umum.
- **Date and Time**: Java-time-range untuk manipulasi tanggal.
- **Payment Gateway**: Midtrans dan Xendit untuk pembayaran.
- **Email Template**: Thymeleaf untuk template email.
- **AWS SDK**: Untuk integrasi dengan AWS S3 dan SES.
- **Firebase**: Firebase Admin SDK untuk push notifications.
- **Twilio**: Twilio SDK untuk SMS.
- **OAuth2**: Spring Security OAuth2 untuk social login.
- **Monitoring**: Micrometer untuk metrics dan tracing.

### 5.3 Konfigurasi Dasar
- **application.yml**: Konfigurasi utama aplikasi yang mencakup database, redis, mail, jwt, dan lainnya.
- **application-dev.yml**: Konfigurasi khusus untuk environment development.
- **application-prod.yml**: Konfigurasi khusus untuk environment production.
- **.env.example**: Contoh file environment variables yang dibutuhkan aplikasi.

## 6. Penjelasan Keseluruhan

Rancangan backend LaundryKu Management System dengan Kotlin dan Spring Boot 4 ini menyediakan fondasi yang kuat untuk pengembangan aplikasi enterprise. Beberapa keunggulan dari rancangan ini:

1. **Struktur Modular**: Setiap fitur diorganisir dalam modul terpisah yang memudahkan pengembangan, testing, dan maintenance.

2. **Kotlin Features**: Memanfaatkan fitur-fitur modern Kotlin seperti null safety, extension functions, dan coroutines untuk kode yang lebih ekspresif dan aman.

3. **Spring Boot 3.2.x**: Menggunakan versi terbaru Spring Boot dengan dukungan Java 17 dan fitur-fitur terbaru.

4. **Security yang Kuat**: Implementasi JWT dengan Spring Security yang komprehensif, termasuk OAuth2 untuk social login.

5. **Database Management**: Menggunakan Flyway untuk migrasi database dan Spring Data JPA untuk operasi database yang efisien.

6. **Caching**: Redis untuk caching yang meningkatkan performa aplikasi.

7. **Documentation**: OpenAPI 3 dengan SpringDoc untuk dokumentasi API yang interaktif.

8. **Monitoring**: Integrasi dengan Micrometer dan Prometheus untuk monitoring aplikasi.

9. **Testing**: Konfigurasi testing yang lengkap dengan TestContainers untuk testing database.

10. **Production Ready**: Konfigurasi yang siap untuk deployment dengan Docker dan environment management.

Dengan rancangan ini, tim pengembang dapat membangun backend yang scalable, maintainable, dan sesuai dengan best practices industri untuk aplikasi LaundryKu Management System.