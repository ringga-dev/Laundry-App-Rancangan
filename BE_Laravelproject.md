

# Rancangan Backend LaundryKu Management System dengan Laravel 10

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
- **Framework**: Laravel 10.x
- **Runtime**: PHP 8.2+
- **Database**: PostgreSQL 15+ dengan Eloquent ORM
- **Cache**: Redis 7+ dengan Predis
- **Search**: Elasticsearch 8+ dengan Laravel Scout
- **Message Queue**: RabbitMQ dengan Laravel Queue
- **Authentication**: JWT + OAuth 2.0
- **Documentation**: OpenAPI 3 dengan L5 Swagger

## 2. Struktur Folder Backend

```
laundryku-backend/
├── app/
│   ├── Console/
│   │   ├── Commands/
│   │   │   ├── GenerateReport.php
│   │   │   ├── ProcessQueue.php
│   │   │   └── SyncIntegration.php
│   │   └── Kernel.php
│   ├── Exceptions/
│   │   ├── Handler.php
│   │   ├── CustomException.php
│   │   └── ValidationException.php
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Api/
│   │   │   │   ├── AuthController.php
│   │   │   │   ├── UserController.php
│   │   │   │   ├── LaundryController.php
│   │   │   │   ├── CustomerController.php
│   │   │   │   ├── OrderController.php
│   │   │   │   ├── ServiceController.php
│   │   │   │   ├── PaymentController.php
│   │   │   │   ├── SubscriptionController.php
│   │   │   │   ├── AnalyticsController.php
│   │   │   │   ├── NotificationController.php
│   │   │   │   ├── IntegrationController.php
│   │   │   │   ├── InventoryController.php
│   │   │   │   └── ReportController.php
│   │   │   └── Controller.php
│   │   ├── Middleware/
│   │   │   ├── ApiAuthMiddleware.php
│   │   │   ├── RoleMiddleware.php
│   │   │   ├── ThrottleRequests.php
│   │   │   ├── CorsMiddleware.php
│   │   │   └── JsonMiddleware.php
│   │   ├── Requests/
│   │   │   ├── Auth/
│   │   │   │   ├── LoginRequest.php
│   │   │   │   ├── RegisterRequest.php
│   │   │   │   └── RefreshTokenRequest.php
│   │   │   ├── User/
│   │   │   │   ├── CreateUserRequest.php
│   │   │   │   ├── UpdateUserRequest.php
│   │   │   │   └── DeleteUserRequest.php
│   │   │   ├── Laundry/
│   │   │   │   ├── CreateLaundryRequest.php
│   │   │   │   ├── UpdateLaundryRequest.php
│   │   │   │   └── DeleteLaundryRequest.php
│   │   │   ├── Customer/
│   │   │   │   ├── CreateCustomerRequest.php
│   │   │   │   ├── UpdateCustomerRequest.php
│   │   │   │   └── DeleteCustomerRequest.php
│   │   │   ├── Order/
│   │   │   │   ├── CreateOrderRequest.php
│   │   │   │   ├── UpdateOrderRequest.php
│   │   │   │   └── DeleteOrderRequest.php
│   │   │   ├── Service/
│   │   │   │   ├── CreateServiceRequest.php
│   │   │   │   ├── UpdateServiceRequest.php
│   │   │   │   └── DeleteServiceRequest.php
│   │   │   ├── Payment/
│   │   │   │   ├── CreatePaymentRequest.php
│   │   │   │   ├── ProcessPaymentRequest.php
│   │   │   │   └── CallbackPaymentRequest.php
│   │   │   ├── Subscription/
│   │   │   │   ├── CreateSubscriptionRequest.php
│   │   │   │   ├── UpdateSubscriptionRequest.php
│   │   │   │   └── CancelSubscriptionRequest.php
│   │   │   ├── Analytics/
│   │   │   │   ├── GetAnalyticsRequest.php
│   │   │   │   └── GenerateReportRequest.php
│   │   │   ├── Notification/
│   │   │   │   ├── SendNotificationRequest.php
│   │   │   │   └── MarkNotificationRequest.php
│   │   │   ├── Integration/
│   │   │   │   ├── CreateIntegrationRequest.php
│   │   │   │   ├── UpdateIntegrationRequest.php
│   │   │   │   └── TestIntegrationRequest.php
│   │   │   ├── Inventory/
│   │   │   │   ├── CreateInventoryRequest.php
│   │   │   │   ├── UpdateInventoryRequest.php
│   │   │   │   └── DeleteInventoryRequest.php
│   │   │   └── Report/
│   │   │       ├── GenerateReportRequest.php
│   │   │       └── DownloadReportRequest.php
│   │   ├── Resources/
│   │   │   ├── Auth/
│   │   │   │   ├── LoginResource.php
│   │   │   │   ├── RegisterResource.php
│   │   │   │   └── UserResource.php
│   │   │   ├── User/
│   │   │   │   ├── UserResource.php
│   │   │   │   └── UserCollection.php
│   │   │   ├── Laundry/
│   │   │   │   ├── LaundryResource.php
│   │   │   │   └── LaundryCollection.php
│   │   │   ├── Customer/
│   │   │   │   ├── CustomerResource.php
│   │   │   │   └── CustomerCollection.php
│   │   │   ├── Order/
│   │   │   │   ├── OrderResource.php
│   │   │   │   └── OrderCollection.php
│   │   │   ├── Service/
│   │   │   │   ├── ServiceResource.php
│   │   │   │   └── ServiceCollection.php
│   │   │   ├── Payment/
│   │   │   │   ├── PaymentResource.php
│   │   │   │   └── PaymentCollection.php
│   │   │   ├── Subscription/
│   │   │   │   ├── SubscriptionResource.php
│   │   │   │   └── SubscriptionCollection.php
│   │   │   ├── Analytics/
│   │   │   │   ├── AnalyticsResource.php
│   │   │   │   └── ReportResource.php
│   │   │   ├── Notification/
│   │   │   │   ├── NotificationResource.php
│   │   │   │   └── NotificationCollection.php
│   │   │   ├── Integration/
│   │   │   │   ├── IntegrationResource.php
│   │   │   │   └── IntegrationCollection.php
│   │   │   ├── Inventory/
│   │   │   │   ├── InventoryResource.php
│   │   │   │   └── InventoryCollection.php
│   │   │   └── Report/
│   │   │       ├── ReportResource.php
│   │   │       └── ReportCollection.php
│   │   └── Traits/
│   │       ├── ApiResponse.php
│   │       └── FileUpload.php
│   ├── Models/
│   │   ├── User.php
│   │   ├── Laundry.php
│   │   ├── Customer.php
│   │   ├── Order.php
│   │   ├── OrderItem.php
│   │   ├── Service.php
│   │   ├── Payment.php
│   │   ├── Subscription.php
│   │   ├── Notification.php
│   │   ├── Integration.php
│   │   ├── Inventory.php
│   │   ├── Report.php
│   │   └── Role.php
│   ├── Providers/
│   │   ├── AppServiceProvider.php
│   │   ├── AuthServiceProvider.php
│   │   ├── BroadcastServiceProvider.php
│   │   ├── EventServiceProvider.php
│   │   ├── RouteServiceProvider.php
│   │   └── RepositoryServiceProvider.php
│   ├── Services/
│   │   ├── AuthService.php
│   │   ├── UserService.php
│   │   ├── LaundryService.php
│   │   ├── CustomerService.php
│   │   ├── OrderService.php
│   │   ├── ServiceService.php
│   │   ├── PaymentService.php
│   │   ├── SubscriptionService.php
│   │   ├── AnalyticsService.php
│   │   ├── NotificationService.php
│   │   ├── IntegrationService.php
│   │   ├── InventoryService.php
│   │   ├── ReportService.php
│   │   └── FileUploadService.php
│   ├── Repositories/
│   │   ├── Interfaces/
│   │   │   ├── UserRepositoryInterface.php
│   │   │   ├── LaundryRepositoryInterface.php
│   │   │   ├── CustomerRepositoryInterface.php
│   │   │   ├── OrderRepositoryInterface.php
│   │   │   ├── ServiceRepositoryInterface.php
│   │   │   ├── PaymentRepositoryInterface.php
│   │   │   ├── SubscriptionRepositoryInterface.php
│   │   │   ├── NotificationRepositoryInterface.php
│   │   │   ├── IntegrationRepositoryInterface.php
│   │   │   ├── InventoryRepositoryInterface.php
│   │   │   └── ReportRepositoryInterface.php
│   │   ├── Eloquent/
│   │   │   ├── BaseRepository.php
│   │   │   ├── UserRepository.php
│   │   │   ├── LaundryRepository.php
│   │   │   ├── CustomerRepository.php
│   │   │   ├── OrderRepository.php
│   │   │   ├── ServiceRepository.php
│   │   │   ├── PaymentRepository.php
│   │   │   ├── SubscriptionRepository.php
│   │   │   ├── NotificationRepository.php
│   │   │   ├── IntegrationRepository.php
│   │   │   ├── InventoryRepository.php
│   │   │   └── ReportRepository.php
│   │   └── Cache/
│   │       ├── BaseCacheRepository.php
│   │       ├── UserCacheRepository.php
│   │       ├── LaundryCacheRepository.php
│   │       ├── CustomerCacheRepository.php
│   │       ├── OrderCacheRepository.php
│   │       ├── ServiceCacheRepository.php
│   │       ├── PaymentCacheRepository.php
│   │       ├── SubscriptionCacheRepository.php
│   │       ├── NotificationCacheRepository.php
│   │       ├── IntegrationCacheRepository.php
│   │       ├── InventoryCacheRepository.php
│   │       └── ReportCacheRepository.php
│   ├── Events/
│   │   ├── OrderCreated.php
│   │   ├── OrderUpdated.php
│   │   ├── OrderCancelled.php
│   │   ├── PaymentProcessed.php
│   │   ├── UserRegistered.php
│   │   ├── SubscriptionCreated.php
│   │   └── NotificationSent.php
│   ├── Listeners/
│   │   ├── SendOrderConfirmation.php
│   │   ├── SendPaymentReceipt.php
│   │   ├── SendWelcomeEmail.php
│   │   ├── ProcessSubscriptionPayment.php
│   │   └── LogActivity.php
│   ├── Jobs/
│   │   ├── ProcessPayment.php
│   │   ├── SendEmail.php
│   │   ├── SendNotification.php
│   │   ├── GenerateReport.php
│   │   ├── SyncIntegration.php
│   │   └── ProcessQueue.php
│   ├── Mail/
│   │   ├── OrderConfirmation.php
│   │   ├── PaymentReceipt.php
│   │   ├── WelcomeEmail.php
│   │   ├── SubscriptionRenewal.php
│   │   └── PasswordReset.php
│   ├── Notifications/
│   │   ├── OrderNotification.php
│   │   ├── PaymentNotification.php
│   │   ├── AccountNotification.php
│   │   └── SystemNotification.php
│   └── Helpers/
│       ├── ApiResponseHelper.php
│       ├── FileHelper.php
│       ├── DateHelper.php
│       └── ValidationHelper.php
├── bootstrap/
│   ├── app.php
│   └── providers.php
├── config/
│   ├── app.php
│   ├── auth.php
│   ├── broadcasting.php
│   ├── cache.php
│   ├── cors.php
│   ├── database.php
│   ├── filesystems.php
│   ├── logging.php
│   ├── mail.php
│   ├── queue.php
│   ├── services.php
│   ├── session.php
│   ├── trustedproxy.php
│   └── view.php
├── database/
│   ├── factories/
│   │   ├── UserFactory.php
│   │   ├── LaundryFactory.php
│   │   ├── CustomerFactory.php
│   │   ├── OrderFactory.php
│   │   ├── ServiceFactory.php
│   │   ├── PaymentFactory.php
│   │   ├── SubscriptionFactory.php
│   │   ├── NotificationFactory.php
│   │   ├── IntegrationFactory.php
│   │   ├── InventoryFactory.php
│   │   └── ReportFactory.php
│   ├── migrations/
│   │   ├── 2024_01_01_000000_create_users_table.php
│   │   ├── 2024_01_01_000001_create_roles_table.php
│   │   ├── 2024_01_01_000002_create_laundries_table.php
│   │   ├── 2024_01_01_000003_create_customers_table.php
│   │   ├── 2024_01_01_000004_create_orders_table.php
│   │   ├── 2024_01_01_000005_create_order_items_table.php
│   │   ├── 2024_01_01_000006_create_services_table.php
│   │   ├── 2024_01_01_000007_create_payments_table.php
│   │   ├── 2024_01_01_000008_create_subscriptions_table.php
│   │   ├── 2024_01_01_000009_create_notifications_table.php
│   │   ├── 2024_01_01_000010_create_integrations_table.php
│   │   ├── 2024_01_01_000011_create_inventory_table.php
│   │   ├── 2024_01_01_000012_create_reports_table.php
│   │   └── 2024_01_01_000013_create_user_role_table.php
│   └── seeders/
│       ├── DatabaseSeeder.php
│       ├── RoleSeeder.php
│       ├── UserSeeder.php
│       ├── LaundrySeeder.php
│       ├── ServiceSeeder.php
│       └── CustomerSeeder.php
├── public/
│   ├── index.php
│   └── .htaccess
├── resources/
│   ├── lang/
│   │   └── en/
│   │       ├── auth.php
│   │       ├── pagination.php
│   │       ├── passwords.php
│   │       └── validation.php
│   └── views/
│       ├── emails/
│       │   ├── order-confirmation.blade.php
│       │   ├── payment-receipt.blade.php
│       │   ├── welcome.blade.php
│       │   ├── subscription-renewal.blade.php
│       │   └── password-reset.blade.php
│       └── notifications/
│           ├── order.blade.php
│           ├── payment.blade.php
│           ├── account.blade.php
│           └── system.blade.php
├── routes/
│   ├── api.php
│   ├── channels.php
│   ├── console.php
│   └── web.php
├── storage/
│   ├── app/
│   ├── framework/
│   └── logs/
├── tests/
│   ├── Feature/
│   │   ├── AuthTest.php
│   │   ├── UserTest.php
│   │   ├── LaundryTest.php
│   │   ├── CustomerTest.php
│   │   ├── OrderTest.php
│   │   ├── ServiceTest.php
│   │   ├── PaymentTest.php
│   │   ├── SubscriptionTest.php
│   │   ├── AnalyticsTest.php
│   │   ├── NotificationTest.php
│   │   ├── IntegrationTest.php
│   │   ├── InventoryTest.php
│   │   └── ReportTest.php
│   ├── Unit/
│   │   ├── AuthServiceTest.php
│   │   ├── UserServiceTest.php
│   │   ├── LaundryServiceTest.php
│   │   ├── CustomerServiceTest.php
│   │   ├── OrderServiceTest.php
│   │   ├── ServiceServiceTest.php
│   │   ├── PaymentServiceTest.php
│   │   ├── SubscriptionServiceTest.php
│   │   ├── AnalyticsServiceTest.php
│   │   ├── NotificationServiceTest.php
│   │   ├── IntegrationServiceTest.php
│   │   ├── InventoryServiceTest.php
│   │   └── ReportServiceTest.php
│   └── CreatesApplication.php
├── .env.example
├── artisan
├── composer.json
├── package.json
├── phpunit.xml
└── README.md
```

## 3. Library yang Dibutuhkan (composer.json)

```json
{
    "name": "laundryku/laundryku-backend",
    "type": "project",
    "description": "Backend for LaundryKu Management System",
    "keywords": ["laravel", "laundry", "management", "system"],
    "license": "MIT",
    "require": {
        "php": "^8.2",
        "guzzlehttp/guzzle": "^7.8",
        "laravel/framework": "^10.10",
        "laravel/sanctum": "^3.3",
        "laravel/tinker": "^2.8",
        "tymon/jwt-auth": "^2.0",
        "spatie/laravel-permission": "^6.1",
        "spatie/laravel-activitylog": "^4.7",
        "spatie/laravel-medialibrary": "^10.7",
        "predis/predis": "^2.2",
        "laravel/horizon": "^5.21",
        "laravel/scout": "^10.2",
        "elasticsearch/elasticsearch": "^8.10",
        "midtrans/midtrans-php": "^2.5",
        "xendit/xendit-php": "^3.3",
        "laravel-notification-channels/fcm": "^3.0",
        "laravel-notification-channels/twilio": "^4.0",
        "maatwebsite/excel": "^3.1",
        "barryvdh/laravel-snappy": "^0.4.8",
        "w0nk0/laravel-eloquent-filter": "^1.0",
        "fruitcake/laravel-cors": "^3.0",
        "darkaonline/l5-swagger": "^8.3",
        "intervention/image": "^2.7",
        "nesbot/carbon": "^2.71",
        "vlucas/phpdotenv": "^5.5",
        "doctrine/dbal": "^3.7",
        "fakerphp/faker": "^1.23",
        "league/flysystem-aws-s3-v3": "^3.0",
        "league/flysystem-ftp": "^3.0",
        "league/flysystem-sftp-v3": "^3.0",
        "guzzlehttp/psr7": "^2.6",
        "symfony/http-client": "^6.4",
        "symfony/mailgun-mailer": "^6.4",
        "symfony/postmark-mailer": "^6.4",
        "symfony/amazon-mailer": "^6.4",
        "aws/aws-sdk-php": "^3.283",
        "pusher/pusher-php-server": "^7.2",
        "abraham/twitteroauth": "^5.0",
        "google/apiclient": "^2.15",
        "facebook/graph-sdk": "^5.15",
        "twilio/sdk": "^7.12",
        "firebase/php-jwt": "^6.10"
    },
    "require-dev": {
        "fakerphp/faker": "^1.23",
        "laravel/pint": "^1.13",
        "laravel/sail": "^1.25",
        "mockery/mockery": "^1.6",
        "nunomaduro/collision": "^7.9",
        "phpunit/phpunit": "^10.4",
        "spatie/laravel-ignition": "^2.3",
        "laravel/telescope": "^4.17",
        "brianium/paratest": "^7.3",
        "barryvdh/laravel-debugbar": "^3.9",
        "barryvdh/laravel-ide-helper": "^2.13",
        "roave/security-advisories": "dev-latest",
        "phpstan/phpstan": "^1.10",
        "squizlabs/php_codesniffer": "^3.8"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app/",
            "Database\\Factories\\": "database/factories/",
            "Database\\Seeders\\": "database/seeders/"
        },
        "files": [
            "app/Helpers/ApiResponseHelper.php",
            "app/Helpers/FileHelper.php",
            "app/Helpers/DateHelper.php",
            "app/Helpers/ValidationHelper.php"
        ]
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "post-autoload-dump": [
            "Illuminate\\Foundation\\ComposerScripts::postAutoloadDump",
            "@php artisan package:discover --ansi",
            "@php artisan vendor:publish --tag=laravel-assets --ansi --force"
        ],
        "post-update-cmd": [
            "@php artisan vendor:publish --tag=laravel-assets --ansi --force"
        ],
        "post-root-package-install": [
            "@php -r \"file_exists('.env') || copy('.env.example', '.env');\""
        ],
        "post-create-project-cmd": [
            "@php artisan key:generate --ansi"
        ],
        "test": "vendor/bin/paratest",
        "test-coverage": "vendor/bin/phpunit --coverage-html coverage",
        "lint": "vendor/bin/pint",
        "cs-check": "vendor/bin/phpcs --standard=PSR12 app",
        "cs-fix": "vendor/bin/phpcbf --standard=PSR12 app",
        "analyze": "vendor/bin/phpstan analyse app",
        "ide-helper": "php artisan ide-helper:generate && php artisan ide-helper:meta"
    },
    "extra": {
        "laravel": {
            "dont-discover": []
        }
    },
    "config": {
        "optimize-autoloader": true,
        "preferred-install": "dist",
        "sort-packages": true,
        "allow-plugins": {
            "pestphp/pest-plugin": true,
            "php-http/discovery": true
        }
    },
    "minimum-stability": "stable",
    "prefer-stable": true
}
```

## 4. Konfigurasi Dasar

### 4.1 .env.example
```env
APP_NAME=LaundryKu
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8000

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=laundryku
DB_USERNAME=postgres
DB_PASSWORD=password

BROADCAST_DRIVER=log
CACHE_DRIVER=redis
FILESYSTEM_DRIVER=s3
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_CLUSTER="${PUSHER_APP_CLUSTER}"

JWT_SECRET=
JWT_TTL=1440
JWT_REFRESH_TTL=20160
JWT_ALGORITHM=HS256

ELASTICSEARCH_HOST=localhost
ELASTICSEARCH_PORT=9200
ELASTICSEARCH_SCHEME=http
ELASTICSEARCH_USER=
ELASTICSEARCH_PASS=

MIDTRANS_SERVER_KEY=
MIDTRANS_CLIENT_KEY=
MIDTRANS_SANDBOX=true

XENDIT_SECRET_KEY=

FCM_SERVER_KEY=
FCM_SENDER_ID=

TWILIO_SID=
TWILIO_TOKEN=
TWILIO_FROM=

GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

FACEBOOK_CLIENT_ID=
FACEBOOK_CLIENT_SECRET=

FILE_UPLOAD_PATH=uploads
FILE_MAX_SIZE=10240

CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8000
CORS_ALLOWED_METHODS=GET,POST,PUT,DELETE,OPTIONS
CORS_ALLOWED_HEADERS=*
CORS_ALLOW_CREDENTIALS=true
```

### 4.2 config/app.php (Konfigurasi Penting)
```php
return [
    'name' => env('APP_NAME', 'LaundryKu'),
    'env' => env('APP_ENV', 'production'),
    'debug' => (bool) env('APP_DEBUG', false),
    'url' => env('APP_URL', 'http://localhost'),
    'asset_url' => env('ASSET_URL'),
    'timezone' => 'Asia/Jakarta',
    'locale' => 'id',
    'fallback_locale' => 'en',
    'faker_locale' => 'id_ID',
    'key' => env('APP_KEY'),
    'cipher' => 'AES-256-CBC',
    'maintenance' => [
        'driver' => 'file',
    ],
    'providers' => [
        // Laravel default providers
        App\Providers\AppServiceProvider::class,
        App\Providers\AuthServiceProvider::class,
        App\Providers\BroadcastServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,
        App\Providers\RepositoryServiceProvider::class,
    ],
    'aliases' => [
        // Laravel default aliases
        'ApiResponse' => App\Helpers\ApiResponseHelper::class,
        'FileHelper' => App\Helpers\FileHelper::class,
        'DateHelper' => App\Helpers\DateHelper::class,
        'ValidationHelper' => App\Helpers\ValidationHelper::class,
    ],
];
```

### 4.3 config/auth.php
```php
return [
    'defaults' => [
        'guard' => 'api',
        'passwords' => 'users',
    ],
    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],
        'api' => [
            'driver' => 'jwt',
            'provider' => 'users',
            'hash' => false,
        ],
    ],
    'providers' => [
        'users' => [
            'driver' => 'eloquent',
            'model' => App\Models\User::class,
        ],
    ],
    'passwords' => [
        'users' => [
            'provider' => 'users',
            'table' => 'password_resets',
            'expire' => 60,
            'throttle' => 60,
        ],
    ],
];
```

### 4.4 config/database.php
```php
return [
    'default' => env('DB_CONNECTION', 'mysql'),
    'connections' => [
        'pgsql' => [
            'driver' => 'pgsql',
            'url' => env('DATABASE_URL'),
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '5432'),
            'database' => env('DB_DATABASE', 'forge'),
            'username' => env('DB_USERNAME', 'forge'),
            'password' => env('DB_PASSWORD', ''),
            'charset' => 'utf8',
            'prefix' => '',
            'prefix_indexes' => true,
            'schema' => 'public',
            'sslmode' => 'prefer',
        ],
        'redis' => [
            'client' => env('REDIS_CLIENT', 'predis'),
            'options' => [
                'cluster' => env('REDIS_CLUSTER', 'redis'),
                'prefix' => env('REDIS_PREFIX', Str::slug(env('APP_NAME', 'laravel'), '_').'_database_'),
            ],
            'default' => [
                'url' => env('REDIS_URL'),
                'host' => env('REDIS_HOST', '127.0.0.1'),
                'username' => env('REDIS_USERNAME'),
                'password' => env('REDIS_PASSWORD'),
                'port' => env('REDIS_PORT', '6379'),
                'database' => env('REDIS_DB', '0'),
            ],
            'cache' => [
                'url' => env('REDIS_URL'),
                'host' => env('REDIS_HOST', '127.0.0.1'),
                'username' => env('REDIS_USERNAME'),
                'password' => env('REDIS_PASSWORD'),
                'port' => env('REDIS_PORT', '6379'),
                'database' => env('REDIS_CACHE_DB', '1'),
            ],
        ],
    ],
    'migrations' => 'migrations',
    'redis' => [
        'client' => env('REDIS_CLIENT', 'predis'),
        'options' => [
            'cluster' => env('REDIS_CLUSTER', 'redis'),
            'prefix' => env('REDIS_PREFIX', Str::slug(env('APP_NAME', 'laravel'), '_').'_database_'),
        ],
    ],
];
```

## 5. Penjelasan Struktur

### 5.1 Struktur Folder
- **app/**: Berisi seluruh logika aplikasi
    - **Console/**: Perintah artisan kustom
    - **Exceptions/**: Exception handling kustom
    - **Http/**: Komponen HTTP (Controller, Middleware, Request, Resource)
    - **Models/**: Model Eloquent
    - **Providers/**: Service providers
    - **Services/**: Business logic layer
    - **Repositories/**: Data access layer dengan pattern Repository
    - **Events/**: Event definitions
    - **Listeners/**: Event listeners
    - **Jobs/**: Queue jobs
    - **Mail/**: Email templates
    - **Notifications/**: Notification classes
    - **Helpers/**: Helper functions
- **bootstrap/**: Bootstrap file aplikasi
- **config/**: File konfigurasi aplikasi
- **database/**: Migrations, seeders, dan factories
- **public/**: File publik dan entry point
- **resources/**: Views, lang, dan assets
- **routes/**: Route definitions
- **storage/**: File storage
- **tests/**: Unit dan feature tests

### 5.2 Library yang Dibutuhkan
- **Laravel Core**: Framework utama dengan fitur-fitur modern
- **Authentication**: JWT Auth untuk API authentication
- **Authorization**: Spatie Permission untuk role-based access control
- **Logging**: Spatie Activity Log untuk audit trail
- **Media Management**: Spatie Media Library untuk file handling
- **Cache**: Redis untuk caching dengan Predis client
- **Queue**: Laravel Horizon untuk queue monitoring
- **Search**: Elasticsearch dengan Laravel Scout
- **Payment**: Midtrans dan Xendit untuk payment gateway
- **Notification**: FCM dan Twilio untuk push notification dan SMS
- **Export/Import**: Laravel Excel untuk file handling
- **PDF Generation**: Snappy untuk PDF generation
- **CORS**: Laravel CORS untuk cross-origin request handling
- **API Documentation**: L5 Swagger untuk dokumentasi API
- **Image Processing**: Intervention Image untuk manipulasi gambar
- **File Storage**: AWS S3, FTP, dan SFTP support
- **Social Login**: OAuth integrasi untuk Google dan Facebook
- **Email**: Multiple mailer support (Mailgun, Postmark, Amazon SES)
- **Push Notification**: Pusher untuk real-time notification
- **Development Tools**: Pint, PHP CS, PHPStan untuk code quality

### 5.3 Konfigurasi Dasar
- **.env.example**: Template untuk environment variables
- **config/app.php**: Konfigurasi aplikasi utama
- **config/auth.php**: Konfigurasi authentication dan authorization
- **config/database.php**: Konfigurasi database dan Redis
- **config/services.php**: Konfigurasi layanan eksternal

## 6. Penjelasan Keseluruhan

Rancangan backend LaundryKu Management System dengan Laravel 10 ini menyediakan fondasi yang kuat untuk pengembangan aplikasi enterprise. Beberapa keunggulan dari rancangan ini:

1. **Struktur Modular**: Organisasi kode yang terstruktur dengan separation of concerns antara Controller, Service, Repository, dan Model.

2. **Laravel 10 Features**: Memanfaatkan fitur-fitur terbaru Laravel seperti improved type hints, native type declarations, dan performance improvements.

3. **Authentication & Authorization**: Implementasi JWT untuk API authentication dan Spatie Permission untuk role-based access control yang fleksibel.

4. **Database Management**: PostgreSQL sebagai database utama dengan Redis untuk caching dan Elasticsearch untuk search functionality.

5. **Queue System**: Laravel Queue dengan Redis dan Horizon untuk background job processing dan monitoring.

6. **File Management**: Spatie Media Library untuk handling file uploads dengan support untuk multiple storage (S3, FTP, SFTP).

7. **Payment Integration**: Integrasi dengan Midtrans dan Xendit untuk payment processing.

8. **Notification System**: Multi-channel notification (email, SMS, push notification) dengan Laravel Notification.

9. **API Documentation**: L5 Swagger untuk dokumentasi API yang interaktif dan mudah diakses.

10. **Testing**: Struktur testing yang lengkap dengan PHPUnit dan Paratest untuk parallel testing.

11. **Development Tools**: Tooling untuk code quality (Pint, PHP CS, PHPStan) dan debugging (Telescope, Debugbar).

12. **Production Ready**: Konfigurasi yang siap untuk production dengan environment management dan security best practices.

Dengan rancangan ini, tim pengembang dapat membangun backend yang scalable, maintainable, dan sesuai dengan best practices industri untuk aplikasi LaundryKu Management System.