

# RANCANGAN LENGKAP APLIKASI LAUNDRYKU MANAGEMENT SYSTEM
## Dengan Sistem Subscription Berbasis Tier (Basic, Pro, Premium)

---

## DAFTAR ISI
1. [Pendahuluan & Visi Produk](#1-pendahuluan--visi-produk)
2. [Arsitektur Sistem Enterprise](#2-arsitektur-sistem-enterprise)
3. [Fitur Lengkap Aplikasi](#3-fitur-lengkap-aplikasi)
4. [Business Logic & Alur Proses](#4-business-logic--alur-proses)
5. [Desain Database & Data Model](#5-desain-database--data-model)
6. [API Architecture & Endpoints](#6-api-architecture--endpoints)
7. [Security Architecture](#7-security-architecture)
8. [Technology Stack Lengkap](#8-technology-stack-lengkap)
9. [UI/UX Design Specifications](#9-uiux-design-specifications)
10. [Implementation Roadmap](#10-implementation-roadmap)
11. [Monitoring & Maintenance](#11-monitoring--maintenance)
12. [Future Enhancements & Innovation](#12-future-enhancements--innovation)

---

## 1. PENDAHULUAN & VISI PRODUK

### 1.1 Executive Summary
LaundryKu Management System adalah solusi enterprise end-to-end untuk industri laundry yang mengintegrasikan manajemen operasional, customer relationship, financial management, dan analytics dalam satu platform terpadu. Dengan arsitektur microservices yang scalable dan sistem subscription berbasis tier, aplikasi ini dirancang untuk melayani berbagai skala bisnis laundry dari UMKM hingga enterprise level.

### 1.2 Visi & Misi
**Visi**: Menjadi platform laundry management terdepan di Asia Tenggara dengan teknologi AI-driven dan sustainable practices.

**Misi**:
- Memberikan solusi teknologi yang accessible dan affordable untuk semua skala bisnis laundry
- Mendorong digitalisasi dan standardisasi industri laundry
- Menciptakan ekosistem laundry yang terintegrasi dan sustainable
- Memberdayakan UMKM laundry untuk bersaing di era digital

### 1.3 Target Market
- **Primary Target**: Laundry bisnis skala menengah (5-50 karyawan)
- **Secondary Target**: Enterprise laundry chains, hotel laundry services, hospital laundry
- **Tertiary Target**: UMKM laundry yang ingin digitalisasi

### 1.4 Value Proposition
- **All-in-One Platform**: Solusi terintegrasi dari order hingga analytics
- **Scalable Architecture**: Dapat berkembang sesuai pertumbuhan bisnis
- **AI-Powered**: Predictive analytics dan automation
- **Local Expertise**: Desain khusus untuk market Indonesia
- **Ecosystem Integration**: Koneksi dengan marketplace, payment, logistics

### 1.5 Competitive Advantage
- **Vertical Integration**: End-to-end solution tidak tersedia di kompetitor
- **Technology Leadership**: AI dan machine learning capabilities
- **Flexible Pricing**: Tiered subscription sesuai kebutuhan
- **Open Ecosystem**: API-first architecture untuk integrasi
- **Local Compliance**: Full compliance dengan regulasi Indonesia

---

## 2. ARSITEKTUR SISTEM ENTERPRISE

### 2.1 High-Level Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                    Load Balancer & CDN                          │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
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
                                │
                                ▼
┌───────────────────────────────────────────────────────────────────┐
│                  Infrastructure Layer                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌──────────────┐ │
│  │ Compute     │ │ Storage     │ │ Networking  │ │ Monitoring   │ │
│  │ (Kubernetes)│ │ (S3/EBS)    │ │ (VPC/LB)    │ │ (Prometheus) │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └──────────────┘ │
└───────────────────────────────────────────────────────────────────┘
```

### 2.2 Microservices Architecture Detail

#### 2.2.1 Core Services
**Authentication Service**
- JWT token management
- OAuth 2.0/OpenID Connect integration
- Role-based access control (RBAC)
- Multi-factor authentication
- Session management
- Audit logging

**Order Management Service**
- Order lifecycle management
- Status tracking and updates
- Order assignment and routing
- Priority queue management
- SLA monitoring
- Order analytics

**Customer Management Service**
- Customer profile management
- Subscription tier management
- Loyalty program integration
- Customer segmentation
- Communication preferences
- Feedback management

**Payment Service**
- Multi-payment gateway integration
- Subscription billing
- Invoice generation
- Refund processing
- Payment reconciliation
- Fraud detection

#### 2.2.2 Supporting Services
**Analytics Service**
- Real-time analytics processing
- Predictive modeling
- Customer behavior analysis
- Business intelligence
- Report generation
- Data visualization

**Notification Service**
- Multi-channel communication (Email, SMS, WhatsApp, Push)
- Template management
- Delivery tracking
- Campaign management
- Preference management
- Analytics tracking

**Integration Service**
- Third-party API management
- Webhook processing
- Data synchronization
- Error handling and retry
- Rate limiting
- Monitoring

**Inventory Service**
- Stock level management
- Supplier integration
- Purchase order management
- Waste tracking
- Cost analysis
- Forecasting

### 2.3 Data Flow Architecture
```
Client Apps → API Gateway → Microservices → Message Queue → Database
     ↑              ↓              ↓              ↓            ↓
     │              │              │              │            │
    CDN ←──  Load Balancer ←──Cache Layer ←── Analytics ←── Search Engine
```

### 2.4 Deployment Architecture
- **Multi-region deployment** untuk high availability
- **Kubernetes orchestration** untuk container management
- **Auto-scaling groups** untuk handle traffic spikes
- **Blue-green deployment** untuk zero-downtime updates
- **Disaster recovery** dengan cross-region replication

---

## 3. FITUR LENGKAP APLIKASI

### 3.1 Fitur Berdasarkan Subscription Tier

#### 3.1.1 Basic Tier (Rp 500.000/bulan atau Rp 5.000.000/tahun)
**Core Features:**
- 1 cabang laundry management
- Maksimal 50 pelanggan aktif
- Maksimal 2 staf users
- 100 transaksi/bulan
- Basic order management
- Simple customer database
- Basic financial reporting
- Email notifications
- Web-based admin panel

**Limitations:**
- No mobile apps
- No marketplace integration
- No advanced analytics
- No API access
- No multi-branch support

#### 3.1.2 Pro Tier (Rp 1.000.000/bulan atau Rp 10.000.000/tahun)
**All Basic Features Plus:**
- 3 cabang laundry management
- Maksimal 200 pelanggan aktif
- Maksimal 10 staf users
- 500 transaksi/bulan
- Advanced order tracking
- Customer segmentation
- Loyalty program (Basic)
- Multi-channel notifications
- Staff mobile app (Android/iOS)
- Customer mobile app
- Marketplace integration (1 channel)
- Advanced reporting & analytics
- API access (read-only)
- Inventory management
- Route optimization

#### 3.1.3 Premium Tier (Rp 2.000.000/bulan atau Rp 20.000.000/tahun)
**All Pro Features Plus:**
- Unlimited cabang laundry
- Unlimited pelanggan aktif
- Unlimited staf users
- Unlimited transaksi
- Enterprise dashboard
- AI-powered analytics
- Predictive maintenance
- Advanced loyalty program
- White-label solution
- Multi-language support
- Full API access (read/write)
- Custom integrations
- Priority support
- Training & consulting
- Franchise management tools
- Advanced automation
- Machine learning features

### 3.2 Fitur Detail per Modul

#### 3.2.1 Manajemen Bisnis Laundry
**Master Data Management**
- Multi-cabang registration dengan hierarchy management
- Detail informasi laundry (nama, alamat, koordinat GPS, jam operasional)
- Fasilitas laundry management (50+ predefined options)
- Dokumen legal management (SIUP, NPWP, izin operasional)
- Kontak manajemen dengan role-based access

**Service Management**
- Service categories (Cuci Basah, Cuci Kering, Setrika, Dry Cleaning, Express)
- Pricing management (per kg, per item, express pricing)
- Service duration configuration
- Capacity management
- Service bundling and packages
- Seasonal pricing rules

**Machine & Equipment Management**
- Machine inventory tracking
- Maintenance scheduling
- Performance monitoring
- Utilization analytics
- Cost tracking per machine
- Predictive maintenance alerts

#### 3.2.2 Sistem Pemesanan & Penjadwalan
**Order Management**
- Multi-channel booking (Web, Mobile, Phone, Walk-in, Marketplace)
- Real-time availability checking
- Dynamic pricing calculation
- Order modification and cancellation
- Priority queue management
- Bulk order processing

**Scheduling System**
- Intelligent pickup/delivery scheduling
- Route optimization
- Capacity planning
- Staff assignment
- Time slot management
- Conflict resolution

**Status Tracking**
- Real-time order status updates
- GPS tracking for delivery
- Automated status notifications
- Photo documentation at each stage
- Quality control checkpoints
- Customer confirmation system

#### 3.2.3 Manajemen Pelanggan & Subscription
**Customer Database**
- Comprehensive customer profiles
- Order history and preferences
- Communication tracking
- Payment method management
- Address book management
- Privacy and consent management

**Subscription Management**
- Tier-based subscription (Basic, Pro, Premium)
- Automated billing and invoicing
- Subscription upgrades/downgrades
- Trial period management
- Churn prediction and prevention
- Loyalty points integration

**Loyalty Program**
- Multi-tier loyalty system
- Points earning and redemption
- Membership benefits management
- Referral program
- Special offers and promotions
- Gamification elements

#### 3.2.4 Keuangan & Laporan
**Financial Management**
- Multi-currency support
- Tax calculation and reporting
- Revenue recognition
- Expense tracking
- Profit analysis
- Cash flow management

**Reporting & Analytics**
- Real-time dashboard
- Custom report builder
- Scheduled report generation
- Data export capabilities
- Visual analytics
- Benchmarking tools

**Billing & Invoicing**
- Automated invoicing
- Payment processing
- Recurring billing
- Late payment management
- Discount and coupon management
- Financial reconciliation

#### 3.2.5 Operasional & Produksi
**Production Management**
- Workflow automation
- Quality control processes
- Production tracking
- Staff productivity monitoring
- Machine utilization
- Waste management

**Inventory Management**
- Stock level monitoring
- Supplier management
- Purchase order processing
- Cost tracking
- Expiration date management
- Reorder point automation

**Staff Management**
- Staff scheduling
- Performance tracking
- Task assignment
- Time and attendance
- Training management
- Commission calculation

#### 3.2.6 Integrasi & Ekosistem
**Marketplace Integration**
- Tokopedia, Shopee, Bukalapak
- GoFood, GrabFood
- Traveloka, Tiket.com
- Custom marketplace connections
- Order synchronization
- Inventory updates

**Payment Gateway Integration**
- Midtrans, Xendit
- OVO, GoPay, DANA
- Bank transfers
- Credit cards
- E-wallets
- QRIS

**Logistics Integration**
- Gojek, Grab
- Third-party couriers
- Route optimization
- Delivery tracking
- Proof of delivery
- Rate comparison

#### 3.2.7 Mobile Applications
**Customer Mobile App**
- Order placement and tracking
- Payment processing
- Profile management
- Loyalty program access
- Push notifications
- Customer support

**Staff Mobile App**
- Order management
- Status updates
- Photo documentation
- GPS tracking
- Task management
- Communication tools

**Admin Mobile App**
- Dashboard monitoring
- Approvals and alerts
- Report viewing
- Staff management
- Communication
- Emergency notifications

#### 3.2.8 Admin Web Application
**Dashboard**
- Real-time metrics
- Performance indicators
- Alerts and notifications
- Quick actions
- Trend analysis
- Goal tracking

**Management Modules**
- Order management
- Customer management
- Staff management
- Financial management
- Reporting
- Settings and configuration

**Advanced Features**
- User permissions
- Audit trails
- Data export
- System configuration
- Integration management
- Security settings

---

## 4. BUSINESS LOGIC & ALUR PROSES

### 4.1 Order Lifecycle Management

#### 4.1.1 Order States and Transitions
```
[Draft] → [Confirmed] → [Scheduled] → [Pickup Scheduled] → [Picked Up] → 
[Received] → [Processing] → [Quality Check] → [Ready] → [Delivery Scheduled] → 
[Out for Delivery] → [Delivered] → [Completed]
                                    ↓
                              [Cancelled] ← (dari state manapun)
```

#### 4.1.2 State Transition Rules
**Draft → Confirmed**
- Trigger: Customer confirmation and payment
- Validation: Valid customer, valid service, capacity available
- Actions: Generate order ID, calculate pricing, send confirmation

**Confirmed → Scheduled**
- Trigger: Staff assignment and time slot selection
- Validation: Staff availability, time slot availability
- Actions: Schedule pickup, notify customer and staff

**Scheduled → Pickup Scheduled**
- Trigger: System auto-scheduling (24 hours before pickup)
- Validation: Order ready for pickup
- Actions: Send pickup reminder, prepare pickup logistics

**Pickup Scheduled → Picked Up**
- Trigger: Driver confirmation and photo documentation
- Validation: Order ID verification, location match
- Actions: Update status, record pickup details, start processing timer

**Picked Up → Received**
- Trigger: Laundry staff confirmation and weight measurement
- Validation: Order items match, weight recorded
- Actions: Update inventory, start production process

**Received → Processing**
- Trigger: Automatic transition after receiving
- Validation: Production capacity available
- Actions: Assign to machines, start processing timer

**Processing → Quality Check**
- Trigger: Processing completion
- Validation: Processing time completed, quality standards met
- Actions: Perform quality inspection, document results

**Quality Check → Ready**
- Trigger: Quality check passed
- Validation: All quality standards met
- Actions: Package order, update status, notify customer

**Ready → Delivery Scheduled**
- Trigger: Customer confirmation or auto-scheduling
- Validation: Delivery slot available, driver available
- Actions: Schedule delivery, notify customer and driver

**Delivery Scheduled → Out for Delivery**
- Trigger: Driver pickup from laundry
- Validation: Order ready, driver assigned
- Actions: Update status, enable GPS tracking

**Out for Delivery → Delivered**
- Trigger: Customer confirmation and signature
- Validation: Delivery location match, customer verification
- Actions: Complete delivery, process payment, send receipt

**Delivered → Completed**
- Trigger: Automatic transition (24 hours after delivery)
- Validation: No disputes or issues
- Actions: Finalize order, calculate loyalty points, send feedback request

### 4.2 Subscription Management Logic

#### 4.2.1 Subscription Tiers and Features
**Basic Tier Features:**
- 1 branch, 50 customers, 2 staff, 100 transactions/month
- Basic web dashboard, email notifications
- No mobile apps, no marketplace integration

**Pro Tier Features:**
- 3 branches, 200 customers, 10 staff, 500 transactions/month
- Mobile apps, 1 marketplace integration, advanced analytics
- API read-only access, route optimization

**Premium Tier Features:**
- Unlimited everything, white-label solution
- Full API access, custom integrations, AI features
- Priority support, training & consulting

#### 4.2.2 Subscription Lifecycle
```
[Trial] → [Active] → [Renewal] → [Expired] → [Cancelled]
    ↓         ↓         ↓           ↓           ↓
[Extended] [Upgrade] [Downgrade] [Reactivated] [Deleted]
```

#### 4.2.3 Billing Logic
**Monthly Billing**
- Billing date: Anniversary date of subscription
- Grace period: 7 days after due date
- Late fee: 10% of monthly fee after grace period
- Suspension: 14 days after due date
- Cancellation: 30 days after suspension

**Yearly Billing**
- Billing date: Anniversary date with 17% discount
- Grace period: 14 days after due date
- Late fee: 5% of yearly fee after grace period
- Suspension: 30 days after due date
- Cancellation: 60 days after suspension

### 4.3 Pricing and Discount Logic

#### 4.3.1 Base Pricing Calculation
**Pricing Components:**
- Base price per service type
- Weight multiplier (per kg)
- Express service multiplier (1.5x)
- Weekend/holiday multiplier (1.2x)
- Customer discount percentage
- Tax calculation (11% PPN)

**Dynamic Pricing Rules:**
- Peak hours (18:00-21:00): +20%
- Weekend: +15%
- Holiday season: +25%
- Low demand: -10%

**Customer-Based Pricing:**
- VIP customers: -15%
- Loyalty tier benefits: 5-20%
- Bulk orders: 10-30%
- Corporate contracts: Custom pricing

### 4.4 Loyalty Program Logic

#### 4.4.1 Points Calculation
**Base Points:** 1 point per Rp 1,000 spent
**Tier Multipliers:**
- Basic: 1x
- Silver: 1.2x
- Gold: 1.5x
- Platinum: 2x

**Service Bonuses:**
- Express service: +50 points
- Dry cleaning: +30 points
- Regular service: +10 points

#### 4.4.2 Tier Progression
**Tier Requirements:**
- Basic: 0+ points
- Silver: 1,000+ points
- Gold: 5,000+ points
- Platinum: 15,000+ points

**Tier Benefits:**
- Basic: 5% birthday discount
- Silver: 10% discount + priority service
- Gold: 15% discount + free pickup + dedicated support
- Platinum: 20% discount + all services + personal manager

### 4.5 Inventory Management Logic

#### 4.5.1 Stock Level Calculation
**Stock Components:**
- Current stock on hand
- Reserved stock for pending orders
- Incoming stock from suppliers
- Safety stock level
- Reorder point calculation

**Automated Reordering:**
- Monitor stock levels in real-time
- Generate purchase orders when stock < reorder point
- Consider supplier lead time
- Calculate optimal order quantity
- Send notifications to procurement team

### 4.6 Route Optimization Logic

#### 4.6.1 Delivery Route Calculation
**Route Optimization Factors:**
- Order locations and priorities
- Time windows for delivery
- Driver availability and capacity
- Traffic conditions and distance
- Fuel cost optimization
- Customer preferences

**Optimization Goals:**
- Minimize total distance traveled
- Minimize delivery time
- Maximize on-time deliveries
- Balance driver workload
- Optimize fuel consumption

### 4.7 Quality Control Logic

#### 4.7.1 Quality Check Process
**Quality Checkpoints:**
- Stain removal effectiveness
- Color freshness preservation
- Fabric integrity maintenance
- Odor elimination
- Ironing quality

**Scoring System:**
- Each checkpoint weighted by importance
- Overall quality score calculated
- Pass/fail threshold: 70%
- Failed items require rework
- Quality trends tracked over time

---

## 5. DESAIN DATABASE & DATA MODEL

### 5.1 Entity Relationship Diagram (High Level)
```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Users     │────▶│   Roles     │────▶│ Permissions │
└─────────────┘     └─────────────┘     └─────────────┘
       │
       ▼
┌─────────────┐     ┌──────────────┐      ┌─────────────┐
│  Customers  │────▶│ Subscriptions│────▶ │   Orders    │
└─────────────┘     └──────────────┘      └─────────────┘
       │                                    │
       ▼                                    ▼
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Addresses │────▶│ LoyaltyPoints│────▶│ OrderItems  │
└─────────────┘     └──────────────┘     └─────────────┘
                                             │
                                             ▼
                                      ┌─────────────┐
                                      │   Services  │
                                      └─────────────┘
                                             │
                                             ▼
                                      ┌─────────────┐
                                      │   Pricing   │
                                      └─────────────┘
```

### 5.2 Core Table Definitions

#### 5.2.1 User Management Tables
**Users Table**
- Primary key: UUID
- Fields: email, password_hash, first_name, last_name, phone, avatar_url, status, email_verified, phone_verified, last_login, timestamps
- Indexes: email, status, created_at
- Relationships: Many-to-many with Roles, one-to-many with Orders

**Roles Table**
- Primary key: UUID
- Fields: name, description, permissions (JSON), is_system, timestamps
- Indexes: name
- Relationships: Many-to-many with Users

**User Roles Table**
- Composite key: user_id, role_id, laundry_id
- Fields: assigned_at, assigned_by
- Relationships: Links Users to Roles with laundry context

#### 5.2.2 Laundry Management Tables
**Laundries Table**
- Primary key: UUID
- Fields: name, description, address, city, province, postal_code, country, latitude, longitude, phone, email, website, timezone, currency, operating_hours (JSON), facilities (JSON), images (JSON), documents (JSON), status, subscription_tier, subscription_dates, timestamps
- Indexes: status, subscription_tier, location (geospatial)
- Relationships: One-to-many with Customers, Orders, Services

#### 5.2.3 Customer Management Tables
**Customers Table**
- Primary key: UUID
- Fields: laundry_id, user_id, customer_type, first_name, last_name, email, phone, date_of_birth, gender, company_name, tax_id, notes, preferences (JSON), communication_preferences (JSON), loyalty_tier, loyalty_points, total_orders, total_spent, last_order_date, status, timestamps
- Indexes: laundry_id, email, phone, loyalty_tier
- Relationships: Belongs to Laundry, has many Orders, Addresses

**Customer Addresses Table**
- Primary key: UUID
- Fields: customer_id, address_type, address_line1, address_line2, city, province, postal_code, country, latitude, longitude, is_default, notes, timestamps
- Indexes: customer_id, is_default
- Relationships: Belongs to Customer

**Subscriptions Table**
- Primary key: UUID
- Fields: customer_id, laundry_id, tier, status, billing_cycle, price, start_date, end_date, next_billing_date, auto_renew, payment_method_id, timestamps
- Indexes: customer_id, status, next_billing_date
- Relationships: Belongs to Customer and Laundry

#### 5.2.4 Order Management Tables
**Orders Table**
- Primary key: UUID
- Fields: order_number (unique), laundry_id, customer_id, status, priority, order_type, pickup_address_id, delivery_address_id, scheduled_pickup_date, actual_pickup_date, scheduled_delivery_date, actual_delivery_date, weight, estimated_weight, subtotal, discount_amount, tax_amount, total_amount, paid_amount, payment_status, payment_method, special_instructions, internal_notes, assigned_staff_id, assigned_driver_id, source_channel, created_by, timestamps
- Indexes: laundry_id, customer_id, status, pickup_date, delivery_date, order_number
- Relationships: Belongs to Laundry and Customer, has many Order Items

**Order Items Table**
- Primary key: UUID
- Fields: order_id, service_id, item_name, quantity, unit_price, total_price, notes, status, timestamps
- Indexes: order_id, service_id
- Relationships: Belongs to Order and Service

**Order Status History Table**
- Primary key: UUID
- Fields: order_id, status, notes, changed_by, changed_at, location (geospatial), metadata (JSON)
- Indexes: order_id, status, changed_at
- Relationships: Belongs to Order

#### 5.2.5 Service Management Tables
**Services Table**
- Primary key: UUID
- Fields: laundry_id, name, description, category, pricing_type, base_price, express_price, estimated_duration, is_active, is_express, images (JSON), specifications (JSON), timestamps
- Indexes: laundry_id, category, is_active
- Relationships: Belongs to Laundry, has many Service Pricing

**Service Pricing Table**
- Primary key: UUID
- Fields: service_id, customer_type, quantity_type, min_quantity, max_quantity, unit_price, discount_percentage, effective_date, expiry_date, timestamps
- Indexes: service_id, effective_date, expiry_date
- Relationships: Belongs to Service

#### 5.2.6 Financial Management Tables
**Payments Table**
- Primary key: UUID
- Fields: order_id, customer_id, payment_method, payment_gateway, transaction_id, amount, currency, status, payment_date, failure_reason, metadata (JSON), timestamps
- Indexes: order_id, customer_id, status, payment_date
- Relationships: Belongs to Order and Customer

**Invoices Table**
- Primary key: UUID
- Fields: invoice_number (unique), order_id, customer_id, invoice_date, due_date, subtotal, tax_amount, discount_amount, total_amount, paid_amount, status, notes, created_by, timestamps
- Indexes: order_id, customer_id, status, invoice_date
- Relationships: Belongs to Order and Customer

#### 5.2.7 Inventory Management Tables
**Products Table**
- Primary key: UUID
- Fields: laundry_id, name, description, category, sku, barcode, unit, current_stock, reserved_stock, min_stock_level, max_stock_level, reorder_point, unit_cost, selling_price, supplier_id, is_active, expiry_tracking, batch_tracking, timestamps
- Indexes: laundry_id, category, sku, barcode
- Relationships: Belongs to Laundry, has many Inventory Transactions

**Inventory Transactions Table**
- Primary key: UUID
- Fields: product_id, transaction_type, quantity, unit_cost, total_cost, reference_id, reference_type, notes, created_by, timestamps
- Indexes: product_id, transaction_type, created_at
- Relationships: Belongs to Product

#### 5.2.8 Staff Management Tables
**Staff Schedules Table**
- Primary key: UUID
- Fields: staff_id, laundry_id, shift_date, start_time, end_time, break_duration, role, status, notes, timestamps
- Indexes: staff_id, laundry_id, shift_date
- Relationships: Belongs to User and Laundry

**Staff Performance Table**
- Primary key: UUID
- Fields: staff_id, laundry_id, date, orders_processed, items_processed, on_time_deliveries, customer_ratings, efficiency_score, notes, timestamps
- Indexes: staff_id, laundry_id, date
- Relationships: Belongs to User and Laundry

### 5.3 Database Optimization Strategies

#### 5.3.1 Indexing Strategy
- **Primary Keys**: All tables have UUID primary keys with default random generation
- **Foreign Keys**: All foreign key columns are indexed for join performance
- **Query Patterns**: Indexes created based on common query patterns
- **Composite Indexes**: For frequently queried column combinations
- **Partial Indexes**: For queries that filter on specific conditions

#### 5.3.2 Partitioning Strategy
- **Time-based Partitioning**: Orders table partitioned by month for better query performance
- **Range Partitioning**: Large tables partitioned by date ranges
- **List Partitioning**: Reference data partitioned by categories

#### 5.3.3 Materialized Views for Analytics
- **Daily Order Summary**: Aggregated daily order statistics
- **Customer Lifetime Value**: Calculated customer metrics
- **Service Performance**: Service utilization and profitability
- **Staff Performance**: Staff productivity and quality metrics

#### 5.3.4 Database Connection Pooling
- **Minimum Connections**: 2 connections per application instance
- **Maximum Connections**: 20 connections per application instance
- **Idle Timeout**: 30 seconds for idle connections
- **Connection Lifetime**: 1 hour maximum connection lifetime

---

## 6. API ARCHITECTURE & ENDPOINTS

### 6.1 API Design Principles
- **RESTful**: Follow REST principles for resource-oriented design
- **Stateless**: Each request contains all necessary information
- **Versioned**: API versioning for backward compatibility
- **Consistent**: Uniform response format and error handling
- **Secure**: Authentication, authorization, and input validation
- **Documented**: Comprehensive API documentation with OpenAPI/Swagger



# API ENDPOINTS DETAIL TABLE

## 6.3.1 Authentication Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **Login** | POST | `/api/v1/auth/login` | User authentication | **Body:**<br>`{`<br>`"email": "string",`<br>`"password": "string",`<br>`"rememberMe": "boolean"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"accessToken": "string",`<br>`"refreshToken": "string",`<br>`"user": { ... }`<br>`},`<br>`"message": "Login successful",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **401 Unauthorized**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid credentials",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | No |
| **Refresh Token** | POST | `/api/v1/auth/refresh` | Refresh access token | **Body:**<br>`{`<br>`"refreshToken": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"accessToken": "string",`<br>`"refreshToken": "string"`<br>`},`<br>`"message": "Token refreshed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **401 Unauthorized**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid refresh token",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | No |
| **Logout** | POST | `/api/v1/auth/logout` | User logout | **Body:**<br>`{`<br>`"refreshToken": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Logout successful",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid request",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Forgot Password** | POST | `/api/v1/auth/forgot-password` | Initiate password reset | **Body:**<br>`{`<br>`"email": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Reset link sent",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Email not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | No |
| **Reset Password** | POST | `/api/v1/auth/reset-password` | Complete password reset | **Body:**<br>`{`<br>`"token": "string",`<br>`"password": "string",`<br>`"confirmPassword": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Password reset successful",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid token or passwords",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | No |
| **Change Password** | POST | `/api/v1/auth/change-password` | Change password | **Body:**<br>`{`<br>`"currentPassword": "string",`<br>`"newPassword": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Password changed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Current password incorrect",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Validate Token** | GET | `/api/v1/auth/validate` | Validate current token | **Headers:**<br>`Authorization: Bearer <token>` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"valid": true,`<br>`"userId": "uuid"`<br>`},`<br>`"message": "Token valid",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **401 Unauthorized**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid token",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.2 User Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **List Users** | GET | `/api/v1/users` | List users with pagination | **Query:**<br>`page: integer`<br>`limit: integer`<br>`search: string`<br>`role: string`<br>`status: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"users": [ ... ],`<br>`"pagination": { ... }`<br>`},`<br>`"message": "Users retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Create User** | POST | `/api/v1/users` | Create new user | **Body:**<br>`{`<br>`"email": "string",`<br>`"password": "string",`<br>`"firstName": "string",`<br>`"lastName": "string",`<br>`"phone": "string",`<br>`"role": "string",`<br>`"laundryIds": ["string"]`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"user": { ... }`<br>`},`<br>`"message": "User created",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get User** | GET | `/api/v1/users/{id}` | Get user details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"user": { ... }`<br>`},`<br>`"message": "User retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "User not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update User** | PUT | `/api/v1/users/{id}` | Update user | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"firstName": "string",`<br>`"lastName": "string",`<br>`"phone": "string",`<br>`"role": "string",`<br>`"status": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"user": { ... }`<br>`},`<br>`"message": "User updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Delete User** | DELETE | `/api/v1/users/{id}` | Delete user | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "User deleted",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "User not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Activate User** | POST | `/api/v1/users/{id}/activate` | Activate user | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "User activated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "User not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Deactivate User** | POST | `/api/v1/users/{id}/deactivate` | Deactivate user | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "User deactivated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "User not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.3 Laundry Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **List Laundries** | GET | `/api/v1/laundries` | List laundries | **Query:**<br>`page: integer`<br>`limit: integer`<br>`search: string`<br>`status: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"laundries": [ ... ],`<br>`"pagination": { ... }`<br>`},`<br>`"message": "Laundries retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Create Laundry** | POST | `/api/v1/laundries` | Create new laundry | **Body:**<br>`{`<br>`"name": "string",`<br>`"address": "string",`<br>`"city": "string",`<br>`"province": "string",`<br>`"phone": "string",`<br>`"email": "string",`<br>`"operatingHours": { ... },`<br>`"facilities": ["string"]`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"laundry": { ... }`<br>`},`<br>`"message": "Laundry created",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Laundry** | GET | `/api/v1/laundries/{id}` | Get laundry details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"laundry": { ... }`<br>`},`<br>`"message": "Laundry retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Laundry not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Laundry** | PUT | `/api/v1/laundries/{id}` | Update laundry | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"name": "string",`<br>`"address": "string",`<br>`"city": "string",`<br>`"province": "string",`<br>`"phone": "string",`<br>`"email": "string",`<br>`"status": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"laundry": { ... }`<br>`},`<br>`"message": "Laundry updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Delete Laundry** | DELETE | `/api/v1/laundries/{id}` | Delete laundry | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Laundry deleted",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Laundry not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Facilities** | GET | `/api/v1/laundries/{id}/facilities` | Get laundry facilities | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"facilities": [ ... ]`<br>`},`<br>`"message": "Facilities retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Laundry not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Facilities** | POST | `/api/v1/laundries/{id}/facilities` | Update laundry facilities | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"facilities": ["string"]`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Facilities updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.4 Customer Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **List Customers** | GET | `/api/v1/customers` | List customers | **Query:**<br>`page: integer`<br>`limit: integer`<br>`search: string`<br>`laundryId: string`<br>`loyaltyTier: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"customers": [ ... ],`<br>`"pagination": { ... }`<br>`},`<br>`"message": "Customers retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Create Customer** | POST | `/api/v1/customers` | Create new customer | **Body:**<br>`{`<br>`"firstName": "string",`<br>`"lastName": "string",`<br>`"email": "string",`<br>`"phone": "string",`<br>`"laundryId": "string",`<br>`"customerType": "string",`<br>`"address": { ... }`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"customer": { ... }`<br>`},`<br>`"message": "Customer created",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Customer** | GET | `/api/v1/customers/{id}` | Get customer details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"customer": { ... }`<br>`},`<br>`"message": "Customer retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Customer not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Customer** | PUT | `/api/v1/customers/{id}` | Update customer | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"firstName": "string",`<br>`"lastName": "string",`<br>`"email": "string",`<br>`"phone": "string",`<br>`"preferences": { ... }`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"customer": { ... }`<br>`},`<br>`"message": "Customer updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Delete Customer** | DELETE | `/api/v1/customers/{id}` | Delete customer | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Customer deleted",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Customer not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get History** | GET | `/api/v1/customers/{id}/history` | Get customer order history | **Path:**<br>`id: string (UUID)`<br>**Query:**<br>`limit: integer`<br>`offset: integer` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"orders": [ ... ]`<br>`},`<br>`"message": "History retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Customer not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Preferences** | GET | `/api/v1/customers/{id}/preferences` | Get customer preferences | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"preferences": { ... }`<br>`},`<br>`"message": "Preferences retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Customer not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Preferences** | POST | `/api/v1/customers/{id}/preferences` | Update customer preferences | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"service": { ... },`<br>`"specialInstructions": ["string"]`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Preferences updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.5 Order Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **List Orders** | GET | `/api/v1/orders` | List orders | **Query:**<br>`page: integer`<br>`limit: integer`<br>`laundryId: string`<br>`customerId: string`<br>`status: string`<br>`dateFrom: string`<br>`dateTo: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"orders": [ ... ],`<br>`"pagination": { ... }`<br>`},`<br>`"message": "Orders retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Create Order** | POST | `/api/v1/orders` | Create new order | **Body:**<br>`{`<br>`"laundryId": "string",`<br>`"customerId": "string",`<br>`"serviceId": "string",`<br>`"scheduledPickupDate": "string",`<br>`"items": [ ... ],`<br>`"specialInstructions": "string"`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"order": { ... }`<br>`},`<br>`"message": "Order created",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Order** | GET | `/api/v1/orders/{id}` | Get order details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"order": { ... }`<br>`},`<br>`"message": "Order retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Order not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Order** | PUT | `/api/v1/orders/{id}` | Update order | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"scheduledPickupDate": "string",`<br>`"scheduledDeliveryDate": "string",`<br>`"priority": "string",`<br>`"specialInstructions": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"order": { ... }`<br>`},`<br>`"message": "Order updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Cancel Order** | DELETE | `/api/v1/orders/{id}` | Cancel order | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"reason": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Order cancelled",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Order not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Status** | POST | `/api/v1/orders/{id}/status` | Update order status | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"status": "string",`<br>`"notes": "string",`<br>`"location": { ... }`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Status updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid status",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get History** | GET | `/api/v1/orders/{id}/history` | Get order status history | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"history": [ ... ]`<br>`},`<br>`"message": "History retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Order not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Process Pickup** | POST | `/api/v1/orders/{id}/pickup` | Process pickup | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"items": [ ... ],`<br>`"weight": "number",`<br>`"photos": ["string"],`<br>`"paymentCollected": "boolean"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Pickup processed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Process Delivery** | POST | `/api/v1/orders/{id}/deliver` | Process delivery | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"paymentMethod": "string",`<br>`"finalAmount": "number"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Delivery processed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.6 Service Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **List Services** | GET | `/api/v1/services` | List services | **Query:**<br>`page: integer`<br>`limit: integer`<br>`laundryId: string`<br>`category: string`<br>`isActive: boolean` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"services": [ ... ],`<br>`"pagination": { ... }`<br>`},`<br>`"message": "Services retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Create Service** | POST | `/api/v1/services` | Create new service | **Body:**<br>`{`<br>`"laundryId": "string",`<br>`"name": "string",`<br>`"category": "string",`<br>`"basePrice": "number",`<br>`"estimatedDuration": "integer",`<br>`"isActive": "boolean"`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"service": { ... }`<br>`},`<br>`"message": "Service created",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Service** | GET | `/api/v1/services/{id}` | Get service details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"service": { ... }`<br>`},`<br>`"message": "Service retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Service not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Service** | PUT | `/api/v1/services/{id}` | Update service | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"name": "string",`<br>`"category": "string",`<br>`"basePrice": "number",`<br>`"isActive": "boolean"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"service": { ... }`<br>`},`<br>`"message": "Service updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Delete Service** | DELETE | `/api/v1/services/{id}` | Delete service | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Service deleted",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Service not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Pricing** | GET | `/api/v1/services/{id}/pricing` | Get service pricing | **Path:**<br>`id: string (UUID)`<br>**Query:**<br>`dateFrom: string`<br>`dateTo: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"pricing": [ ... ]`<br>`},`<br>`"message": "Pricing retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Service not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Update Pricing** | POST | `/api/v1/services/{id}/pricing` | Update service pricing | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"pricing": [ ... ]`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Pricing updated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Validation failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.7 Payment Management Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **Process Payment** | POST | `/api/v1/payments` | Process payment | **Body:**<br>`{`<br>`"orderId": "string",`<br>`"paymentMethod": "string",`<br>`"amount": "number",`<br>`"currency": "string",`<br>`"metadata": { ... }`<br>`}` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"payment": { ... }`<br>`},`<br>`"message": "Payment processed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Payment failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Get Payment** | GET | `/api/v1/payments/{id}` | Get payment details | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"payment": { ... }`<br>`},`<br>`"message": "Payment retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Payment not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Process Refund** | POST | `/api/v1/payments/{id}/refund` | Process refund | **Path:**<br>`id: string (UUID)`<br>**Body:**<br>`{`<br>`"amount": "number",`<br>`"reason": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "Refund processed",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Refund failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Check Status** | GET | `/api/v1/payments/{id}/status` | Check payment status | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"status": "string",`<br>`"gatewayStatus": "string"`<br>`},`<br>`"message": "Status retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Payment not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.8 Reporting & Analytics Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **Daily Summary** | GET | `/api/v1/reports/daily-summary` | Daily summary report | **Query:**<br>`laundryId: string`<br>`date: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"summary": { ... }`<br>`},`<br>`"message": "Report generated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Monthly Summary** | GET | `/api/v1/reports/monthly-summary` | Monthly summary report | **Query:**<br>`laundryId: string`<br>`year: integer`<br>`month: integer` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"summary": { ... }`<br>`},`<br>`"message": "Report generated",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Customer Analytics** | GET | `/api/v1/reports/customer-analytics` | Customer analytics | **Query:**<br>`laundryId: string`<br>`dateFrom: string`<br>`dateTo: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"analytics": { ... }`<br>`},`<br>`"message": "Analytics retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Service Performance** | GET | `/api/v1/reports/service-performance` | Service performance | **Query:**<br>`laundryId: string`<br>`dateFrom: string`<br>`dateTo: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"performance": { ... }`<br>`},`<br>`"message": "Performance retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Financial Summary** | GET | `/api/v1/reports/financial-summary` | Financial summary | **Query:**<br>`laundryId: string`<br>`dateFrom: string`<br>`dateTo: string` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"summary": { ... }`<br>`},`<br>`"message": "Summary retrieved",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **403 Forbidden**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Insufficient permissions",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Generate Custom Report** | POST | `/api/v1/reports/generate` | Generate custom report | **Body:**<br>`{`<br>`"laundryId: "string",`<br>`"reportType": "string",`<br>`"filters": { ... },`<br>`"columns": ["string"],`<br>`"format": "string"`<br>`}` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"reportId": "string",`<br>`"downloadUrl": "string"`<br>`},`<br>`"message": "Report generation started",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Invalid parameters",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.3.9 WebSocket Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **Order Updates** | WebSocket | `/ws/orders` | Real-time order updates | **Headers:**<br>`Authorization: Bearer <token>` | **Message:**<br>`{`<br>`"type": "order_status_update",`<br>`"data": { ... }`<br>`}` | **Error:**<br>`{`<br>`"type": "error",`<br>`"message": "Authentication failed"`<br>`}` | Yes |
| **Notifications** | WebSocket | `/ws/notifications` | Real-time notifications | **Headers:**<br>`Authorization: Bearer <token>` | **Message:**<br>`{`<br>`"type": "notification",`<br>`"data": { ... }`<br>`}` | **Error:**<br>`{`<br>`"type": "error",`<br>`"message": "Authentication failed"`<br>`}` | Yes |
| **Analytics** | WebSocket | `/ws/analytics` | Real-time analytics data | **Headers:**<br>`Authorization: Bearer <token>` | **Message:**<br>`{`<br>`"type": "analytics_update",`<br>`"data": { ... }`<br>`}` | **Error:**<br>`{`<br>`"type": "error",`<br>`"message": "Authentication failed"`<br>`}` | Yes |

## 6.3.10 File Upload Endpoints

| Endpoint | Method | URL | Description | Request Parameters | Success Response | Error Response | Auth Required |
|----------|--------|-----|-------------|-------------------|-----------------|---------------|---------------|
| **Upload File** | POST | `/api/v1/upload` | Upload file | **Body:**<br>`multipart/form-data`<br>`file: file`<br>`type: string`<br>`entityId: string` | **201 Created**<br>`{`<br>`"success": true,`<br>`"data": {`<br>`"fileId": "string",`<br>`"url": "string"`<br>`},`<br>`"message": "File uploaded",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **400 Bad Request**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "Upload failed",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Download File** | GET | `/api/v1/files/{id}` | Download file | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`File content` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "File not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |
| **Delete File** | DELETE | `/api/v1/files/{id}` | Delete file | **Path:**<br>`id: string (UUID)` | **200 OK**<br>`{`<br>`"success": true,`<br>`"data": null,`<br>`"message": "File deleted",`<br>`"errors": [],`<br>`"meta": { ... }`<br>`}` | **404 Not Found**<br>`{`<br>`"success": false,`<br>`"data": null,`<br>`"message": "File not found",`<br>`"errors": [ ... ],`<br>`"meta": { ... }`<br>`}` | Yes |

## 6.4 API Security Features

| Feature | Description | Implementation |
|---------|-------------|------------------|
| **JWT Authentication** | Stateless authentication with expiry | Bearer token in Authorization header |
| **Role-Based Access Control** | Granular permissions based on user roles | Permission checks in API gateway and services |
| **API Key Authentication** | For third-party integrations | API key in headers or query parameters |
| **OAuth 2.0 Support** | Social login and enterprise SSO | OAuth 2.0 flows with token exchange |
| **Multi-Factor Authentication** | Additional security layer | SMS, Email, Authenticator App |
| **Rate Limiting** | Prevent abuse and ensure fair usage | Redis-based rate limiting with configurable limits |
| **Per-User Rate Limiting** | Individual user limits | User-specific rate limit keys |
| **Per-IP Rate Limiting** | IP-based rate limiting | IP-based rate limit keys |
| **Endpoint-Specific Limits** | Custom limits per endpoint | Configurable per endpoint |
| **Burst Handling** | Handle temporary traffic spikes | Token bucket algorithm |
| **Rate Limit Headers** | Inform clients about limits | `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset` |
| **Request Body Validation** | Validate incoming data | Schema validation with detailed error messages |
| **Parameter Validation** | Validate path and query parameters | Type checking and format validation |
| **File Upload Validation** | Secure file handling | Type, size, and content validation |
| **SQL Injection Prevention** | Protect database queries | Parameterized queries and ORM |
| **XSS Protection** | Prevent cross-site scripting | Output encoding and input sanitization |
| **API Usage Analytics** | Monitor API usage patterns | Request logging and metrics collection |
| **Error Tracking** | Monitor and alert on errors | Error aggregation and alerting |
| **Performance Monitoring** | Track API performance | Response time and throughput metrics |
| **Security Event Logging** | Log security-related events | Audit trail for authentication and authorization |
| **Audit Trail** | Track sensitive operations | Immutable logs for compliance |
| **CORS Configuration** | Control cross-origin requests | Configurable CORS policies |
| **HTTPS Enforcement** | Encrypt all communications | TLS 1.3 with strong ciphers |
| **Request Signing** | Verify request integrity | HMAC signatures for sensitive operations |
| **Webhook Security** | Secure webhook endpoints | HMAC signature validation |



# 6.4 API SECURITY FEATURES DETAIL

## 6.4.1 Authentication & Authorization

| Feature | Description | Implementation | Configuration | Example Usage |
|---------|-------------|----------------|---------------|----------------|
| **JWT-based Authentication** | Stateless authentication using JSON Web Tokens with configurable expiry time | - JWT generation with user claims<br>- Token validation middleware<br>- Refresh token rotation<br>- Secure token storage | ```json<br>{<br>  "jwt": {<br>    "secret": "your-secret-key",<br>    "expiresIn": "24h",<br>    "refreshExpiresIn": "7d"<br>  }<br>}``` | **Request Header:**<br>`Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...`<br><br>**Token Payload:**<br>`{<br>  "sub": "user-uuid",<br>  "roles": ["admin"],<br>  "laundryId": "laundry-uuid",<br>  "iat": 1640995200,<br>  "exp": 1641081600<br>}` |
| **Role-based Access Control (RBAC)** | Granular permission system based on user roles and resource access | - Role definition with permissions<br>- Permission middleware<br>- Resource-level authorization<br>- Hierarchical role structure | ```json<br>{<br>  "roles": {<br>    "admin": ["*"],<br>    "manager": ["orders:*", "customers:*"],<br>    "staff": ["orders:read", "orders:update:status"]<br>  }<br>}``` | **Permission Check:**<br>`if (user.hasPermission('orders:create')) {<br>  // Allow order creation<br>}`<br><br>**Route Protection:**<br>`@Roles('admin', 'manager')<br>@UseGuards(RolesGuard)<br>createOrder() { ... }` |
| **API Key Authentication** | Authentication method for third-party integrations and automated systems | - API key generation and management<br>- Key validation middleware<br>- Key rotation and revocation<br>- Usage tracking and limits | ```json<br>{<br>  "apiKey": {<br>    "prefix": "lk_",<br>    "length": 32,<br>    "rateLimit": 1000,<br>    "permissions": ["orders:read", "orders:create"]<br>  }<br>}``` | **Request Header:**<br>`X-API-Key: lk_a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`<br><br>**API Key Object:**<br>`{<br>  "id": "uuid",<br>  "key": "lk_a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6",<br>  "permissions": ["orders:read", "orders:create"],<br>  "rateLimit": 1000,<br>  "createdAt": "2024-01-01T00:00:00Z",<br>  "expiresAt": "2025-01-01T00:00:00Z"<br>}` |
| **OAuth 2.0 Support** | Support for social login and enterprise single sign-on (SSO) | - OAuth 2.0 provider integration<br>- Token exchange mechanism<br>- User profile mapping<br>- Session management | ```json<br>{<br>  "oauth": {<br>    "providers": {<br>      "google": {<br>        "clientId": "google-client-id",<br>        "clientSecret": "google-client-secret",<br>        "scope": ["email", "profile"]<br>      },<br>      "microsoft": {<br>        "clientId": "microsoft-client-id",<br>        "clientSecret": "microsoft-client-secret",<br>        "tenantId": "microsoft-tenant-id"<br>      }<br>    }<br>  }<br>}``` | **OAuth Flow:**<br>`1. Redirect to provider:<br>GET /api/v1/auth/google`<br><br>2. Callback with code:<br>GET /api/v1/auth/google/callback?code=authorization_code`<br><br>3. Token exchange response:<br>`{<br>  "accessToken": "oauth-access-token",<br>  "refreshToken": "oauth-refresh-token",<br>  "user": { ... }<br>}` |
| **Multi-factor Authentication** | Additional security layer requiring multiple verification methods | - MFA setup and management<br>- Time-based One-Time Password (TOTP)<br>- SMS and email verification<br>- Backup codes generation | ```json<br>{<br>  "mfa": {<br>    "enabled": true,<br>    "methods": ["totp", "sms", "email"],<br>    "backupCodesCount": 10,<br>    "totp": {<br>      "issuer": "LaundryKu",<br>      "algorithm": "SHA1",<br>      "digits": 6,<br>      "period": 30<br>    }<br>  }<br>}``` | **MFA Setup:**<br>`POST /api/v1/auth/mfa/setup`<br>`{<br>  "method": "totp",<br>  "password": "user-password"<br>}`<br><br>**Response:**<br>`{<br>  "secret": "totp-secret",<br>  "qrCodeUrl": "otpauth://totp/LaundryKu:user?secret=secret&issuer=LaundryKu",<br>  "backupCodes": ["code1", "code2", ...]<br>}`<br><br>**MFA Verification:**<br>`POST /api/v1/auth/mfa/verify`<br>`{<br>  "token": "123456",<br>  "backupCode": "optional-backup-code"<br>}` |

## 6.4.2 Rate Limiting

| Feature | Description | Implementation | Configuration | Example Usage |
|---------|-------------|----------------|---------------|----------------|
| **Per-user Rate Limiting** | Limit API requests based on authenticated user identity | - User-specific rate limit keys<br>- Token-based identification<br>- Configurable limits per user tier | ```json<br>{<br>  "rateLimiting": {<br>    "user": {<br>      "basic": { "requests": 100, "window": "15m" },<br>      "pro": { "requests": 500, "window": "15m" },<br>      "premium": { "requests": 2000, "window": "15m" }<br>    }<br>  }<br>}``` | **Rate Limit Headers:**<br>`X-RateLimit-Limit: 100`<br>`X-RateLimit-Remaining: 95`<br>`X-RateLimit-Reset: 1640995800`<br><br>**Rate Limit Exceeded Response:**<br>`{<br>  "success": false,<br>  "message": "Rate limit exceeded",<br>  "errors": [{<br>    "field": "rateLimit",<br>    "message": "Too many requests. Please try again later."<br>  }],<br>  "meta": {<br>    "retryAfter": 60<br>  }<br>}` |
| **Per-IP Rate Limiting** | Limit API requests based on client IP address | - IP-based rate limit keys<br>- Geolocation-aware limits<br>- VPN/proxy detection | ```json<br>{<br>  "rateLimiting": {<br>    "ip": {<br>      "default": { "requests": 1000, "window": "1h" },<br>      "trusted": { "requests": 5000, "window": "1h" }<br>    }<br>  }<br>}``` | **IP-based Rate Limit:**<br>`// Rate limit key: "ip:192.168.1.1"`<br>`// Limit: 1000 requests per hour`<br><br>**Implementation:**<br>`const ipRateLimit = new RateLimit({<br>  keyGenerator: (req) => req.ip,<br>  limit: 1000,<br>  windowMs: 60 * 60 * 1000, // 1 hour<br>  message: "Too many requests from this IP"<br>});` |
| **Endpoint-specific Rate Limits** | Custom rate limits for specific API endpoints based on sensitivity and resource usage | - Endpoint-specific configurations<br>- Different limits for different HTTP methods<br>- Dynamic limit adjustment based on system load | ```json<br>{<br>  "rateLimiting": {<br>    "endpoints": {<br>      "POST /api/v1/auth/login": { "requests": 5, "window": "15m" },<br>      "POST /api/v1/orders": { "requests": 100, "window": "1h" },<br>      "GET /api/v1/reports": { "requests": 10, "window": "1h" }<br>    }<br>  }<br>}``` | **Endpoint-specific Configuration:**<br>`const orderCreationLimit = new RateLimit({<br>  keyGenerator: (req) => `${req.user.id}:create-order`,<br>  limit: 100,<br>  windowMs: 60 * 60 * 1000, // 1 hour<br>  message: "Too many order creation attempts"<br>});`<br><br>**Usage:**<br>`router.post('/orders', orderCreationLimit, createOrderHandler);` |
| **Burst Handling Capabilities** | Allow temporary bursts of requests while maintaining overall rate limits | - Token bucket algorithm<br>- Burst size configuration<br>- Gradual refill rate | ```json<br>{<br>  "rateLimiting": {<br>    "algorithm": "tokenBucket",<br>    "burst": {<br>      "size": 50,<br>      "refillRate": 10,<br>      "refillInterval": "1s"<br>    }<br>  }<br>}``` | **Token Bucket Algorithm:**<br>`// Configuration: 50 tokens burst, refill 10 tokens per second`<br>`// User can make 50 requests immediately, then 10 per second`<br><br>**Implementation:**<br>`class TokenBucket {<br>  constructor(capacity, refillRate) {<br>    this.capacity = capacity;<br>    this.tokens = capacity;<br>    this.refillRate = refillRate;<br>    this.lastRefill = Date.now();<br>  }<br><br>  consume() {<br>    this.refill();<br>    if (this.tokens >= 1) {<br>      this.tokens -= 1;<br>      return true;<br>    }<br>    return false;<br>  }<br><br>  refill() {<br>    const now = Date.now();<br>    const elapsed = (now - this.lastRefill) / 1000;<br>    this.tokens = Math.min(this.capacity, this.tokens + elapsed * this.refillRate);<br>    this.lastRefill = now;<br>  }<br>}` |
| **Rate Limit Headers in Responses** | Inform clients about their current rate limit status via HTTP headers | - Standard rate limit headers<br>- Custom headers for additional information<br>- Graceful degradation information | ```json<br>{<br>  "rateLimiting": {<br>    "headers": {<br>      "enabled": true,<br>      "format": "standard",<br>      "includeResetTime": true,<br>      "includePolicy": true<br>    }<br>  }<br>}``` | **Response Headers:**<br>`HTTP/1.1 200 OK<br>X-RateLimit-Limit: 100<br>X-RateLimit-Remaining: 87<br>X-RateLimit-Reset: 1640995800<br>X-RateLimit-Policy: fixed-window<br>Retry-After: 60`<br><br>**Implementation:**<br>`app.use((req, res, next) => {<br>  res.set('X-RateLimit-Limit', req.rateLimit.limit);<br>  res.set('X-RateLimit-Remaining', req.rateLimit.remaining);<br>  res.set('X-RateLimit-Reset', req.rateLimit.resetTime);<br>  next();<br>});` |

## 6.4.3 Input Validation

| Feature | Description | Implementation | Configuration | Example Usage |
|---------|-------------|----------------|---------------|----------------|
| **Request Body Validation** | Validate incoming request body data against predefined schemas | - Schema validation middleware<br>- Type checking and coercion<br>- Custom validation rules<br>- Detailed error messages | ```json<br>{<br>  "validation": {<br>    "schemas": {<br>      "createOrder": {<br>        "required": ["laundryId", "customerId", "serviceId"],<br>        "properties": {<br>          "laundryId": { "type": "string", "format": "uuid" },<br>          "customerId": { "type": "string", "format": "uuid" },<br>          "serviceId": { "type": "string", "format": "uuid" },<br>          "scheduledPickupDate": { "type": "string", "format": "date-time" },<br>          "specialInstructions": { "type": "string", "maxLength": 500 }<br>        }<br>      }<br>    }<br>  }<br>}``` | **Validation Middleware:**<br>`const validateOrder = (req, res, next) => {<br>  const { error } = orderSchema.validate(req.body);<br>  if (error) {<br>    return res.status(400).json({<br>      success: false,<br>      message: "Validation failed",<br>      errors: error.details.map(detail => ({<br>        field: detail.path.join('.'),<br>        message: detail.message<br>      }))<br>    });<br>  }<br>  next();<br>};`<br><br>**Usage:**<br>`router.post('/orders', validateOrder, createOrderHandler);` |
| **Parameter Validation** | Validate path parameters, query parameters, and headers | - Parameter extraction middleware<br>- Type checking and format validation<br>- Range and enum validation<br>- Default value assignment | ```json<br>{<br>  "validation": {<br>    "parameters": {<br>      "userId": {<br>        "in": "path",<br>        "required": true,<br>        "type": "string",<br>        "format": "uuid"<br>      },<br>      "page": {<br>        "in": "query",<br>        "required": false,<br>        "type": "integer",<br>        "minimum": 1,<br>        "default": 1<br>      },<br>      "limit": {<br>        "in": "query",<br>        "required": false,<br>        "type": "integer",<br>        "minimum": 1,<br>        "maximum": 100,<br>        "default": 20<br>      }<br>    }<br>  }<br>}``` | **Parameter Validation:**<br>`const validateParams = (schema) => {<br>  return (req, res, next) => {<br>    const { error } = schema.validate({<br>      params: req.params,<br>      query: req.query<br>    });<br>    if (error) {<br>      return res.status(400).json({<br>        success: false,<br>        message: "Parameter validation failed",<br>        errors: error.details<br>      });<br>    }<br>    next();<br>  };<br>};`<br><br>**Usage:**<br>`router.get('/users/:userId', validateParams(userParamsSchema), getUserHandler);` |
| **File Upload Validation** | Secure validation of uploaded files to prevent malicious content | - File type validation<br>- File size limits<br>- Content scanning<br>- Virus scanning integration | ```json<br>{<br>  "validation": {<br>    "fileUpload": {<br>      "maxSize": 10485760, // 10MB<br>      "allowedTypes": ["image/jpeg", "image/png", "application/pdf"],<br>      "allowedExtensions": [".jpg", ".jpeg", ".png", ".pdf"],<br>      "virusScan": true,<br>      "contentValidation": true<br>    }<br>  }<br>}``` | **File Upload Validation:**<br>`const validateFile = (req, res, next) => {<br>  if (!req.file) {<br>    return res.status(400).json({<br>      success: false,<br>      message: "No file uploaded"<br>    });<br>  }<br><br>  // Check file size<br>  if (req.file.size > config.maxFileSize) {<br>    return res.status(400).json({<br>      success: false,<br>      message: "File too large"<br>    });<br>  }<br><br>  // Check file type<br>  if (!config.allowedTypes.includes(req.file.mimetype)) {<br>    return res.status(400).json({<br>      success: false,<br>      message: "File type not allowed"<br>    });<br>  }<br><br>  // Virus scan (async)<br>  scanForViruses(req.file.path)<br>    .then(() => next())<br>    .catch(() => {<br>      res.status(400).json({<br>        success: false,<br>        message: "File failed virus scan"<br>      });<br>    });<br>};` |
| **SQL Injection Prevention** | Protect database queries from SQL injection attacks | - Parameterized queries<br>- ORM with safe query building<br>- Input sanitization<br>- Query result limiting | ```json<br>{<br>  "security": {<br>    "sqlInjection": {<br>    "parameterizedQueries": true,<br>    "orm": "prisma",<br>    "queryTimeout": 5000,<br>    "maxResultLimit": 1000<br>    }<br>  }<br>}``` | **Safe Query with ORM:**<br>`// Using Prisma ORM with parameterized queries<br>const users = await prisma.user.findMany({<br>  where: {<br>    email: req.body.email, // Automatically parameterized<br>    role: req.body.role<br>  },<br>  take: 10, // Limit results<br>  skip: (page - 1) * pageSize<br>});`<br><br>**Raw Query with Parameters:**<br>`// Using parameterized raw query<br>const users = await prisma.$queryRaw`<br>  SELECT * FROM users <br>  WHERE email = ${email} AND role = ${role}<br>  LIMIT ${limit} OFFSET ${offset}<br>`;` |
| **XSS Protection** | Prevent Cross-Site Scripting attacks by sanitizing user input | - Output encoding<br>- Input sanitization<br>- Content Security Policy (CSP)<br>- HTML escaping | ```json<br>{<br>  "security": {<br>    "xss": {<br>      "outputEncoding": true,<br>      "inputSanitization": true,<br>      "csp": {<br>        "enabled": true,<br>        "directives": {<br>          "defaultSrc": ["'self'"],<br>          "scriptSrc": ["'self'"],<br>          "styleSrc": ["'self'", "'unsafe-inline'"],<br>          "imgSrc": ["'self'", "data:", "https:"],<br>          "connectSrc": ["'self'"]<br>        }<br>      }<br>    }<br>  }<br>}``` | **Output Encoding:**<br>`// Encode user-generated content before rendering<br>const encodedContent = encode(userInput.content);`<br><br>**Input Sanitization:**<br>`// Sanitize HTML input<br>const clean = sanitizeHtml(dirtyHtml, {<br>  allowedTags: ['b', 'i', 'u', 'strong', 'em'],<br>  allowedAttributes: {}<br>});`<br><br>**Content Security Policy Header:**<br>`Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; connect-src 'self'` |

## 6.4.4 Monitoring & Logging

| Feature | Description | Implementation | Configuration | Example Usage |
|---------|-------------|----------------|---------------|----------------|
| **API Usage Analytics** | Track and analyze API usage patterns and trends | - Request logging with metadata<br>- Usage aggregation and analysis<br>- Real-time dashboard<br>- Historical trend analysis | ```json<br>{<br>  "monitoring": {<br>    "analytics": {<br>      "enabled": true,<br>      "metrics": ["requests", "responseTime", "errorRate"],<br>      "dimensions": ["endpoint", "method", "status", "userAgent", "ip"],<br>      "aggregation": ["count", "avg", "sum", "p95", "p99"],<br>      "retention": "90d"<br>    }<br>  }<br>}``` | **Analytics Collection:**<br>`// Middleware to collect analytics data<br>const analyticsMiddleware = (req, res, next) => {<br>  const startTime = Date.now();<br><br>  res.on('finish', () => {<br>    const duration = Date.now() - startTime;<br>    const analyticsData = {<br>      endpoint: req.path,<br>      method: req.method,<br>      statusCode: res.statusCode,<br>      responseTime: duration,<br>      userAgent: req.get('User-Agent'),<br>      ip: req.ip,<br>      userId: req.user?.id,<br>      timestamp: new Date().toISOString()<br>    };<br><br>    // Send to analytics service<br>    analyticsService.record(analyticsData);<br>  });<br><br>  next();<br>};` |
| **Error Tracking** | Monitor, aggregate, and alert on application errors | - Error capture and classification<br>- Error aggregation and grouping<br>- Alerting on error spikes<br>- Error context and stack traces | ```json<br>{<br>  "monitoring": {<br>    "errorTracking": {<br>      "enabled": true,<br>      "captureUnhandled": true,<br>      "captureUncaught": true,<br>      "grouping": true,<br>      "contexts": ["request", "user", "environment"],<br>      "alertThreshold": {<br>        "count": 10,<br>        "window": "5m"<br>      }<br>    }<br>  }<br>}``` | **Error Tracking Implementation:**<br>`// Error tracking middleware<br>const errorHandler = (err, req, res, next) => {<br>  // Log error with context<br>  errorTracker.captureException(err, {<br>    request: {<br>      url: req.url,<br>      method: req.method,<br>      headers: req.headers,<br>      body: req.body<br>    },<br>    user: req.user<br>  });<br><br>  // Send error response<br>  res.status(500).json({<br>    success: false,<br>    message: "Internal server error",<br>    errorId: err.id // For customer support reference<br>  });<br>};`<br><br>**Manual Error Capture:**<br>`try {<br>  // Risky operation<br>} catch (err) {<br>  errorTracker.captureException(err, {<br>    operation: "payment.processing",<br>    orderId: req.body.orderId<br>  });<br>  throw err;<br>}` |
| **Performance Monitoring** | Track API performance metrics and identify bottlenecks | - Response time tracking<br>- Database query monitoring<br>- External service call tracking<br>- Performance threshold alerting | ```json<br>{<br>  "monitoring": {<br>    "performance": {<br>      "enabled": true,<br>      "metrics": ["responseTime", "dbQueryTime", "externalCallTime"],<br>      "thresholds": {<br>        "responseTime": {<br>          "warning": 1000, // 1s<br>          "critical": 5000 // 5s<br>        },<br>        "dbQueryTime": {<br>          "warning": 100, // 100ms<br>          "critical": 500 // 500ms<br>        }<br>      },<br>      "profiling": {<br>        "enabled": true,<br>        "sampleRate": 0.1 // 10% of requests<br>      }<br>    }<br>  }<br>}``` | **Performance Monitoring:**<br>`// Performance monitoring middleware<br>const performanceMiddleware = (req, res, next) => {<br>  const startTime = Date.now();<br>  const metrics = {<br>    dbQueries: [],<br>    externalCalls: []<br>  };<br><br>  // Track database queries<br>  const originalQuery = prisma.$queryRaw;<br>  prisma.$queryRaw = (...args) => {<br>    const queryStart = Date.now();<br>    return originalQuery.apply(prisma, args)<br>      .then(result => {<br>        metrics.dbQueries.push({<br>          query: args[0],<br>          duration: Date.now() - queryStart<br>        });<br>        return result;<br>      });<br>  };<br><br>  res.on('finish', () => {<br>    const totalResponseTime = Date.now() - startTime;<br>    const totalDbTime = metrics.dbQueries.reduce((sum, q) => sum + q.duration, 0);<br>    const totalExternalTime = metrics.externalCalls.reduce((sum, c) => sum + c.duration, 0);<br><br>    // Record performance metrics<br>    performanceService.record({<br>      endpoint: req.path,<br>      method: req.method,<br>      responseTime: totalResponseTime,<br>      dbTime: totalDbTime,<br>      externalTime: totalExternalTime,<br>      dbQueryCount: metrics.dbQueries.length,<br>      externalCallCount: metrics.externalCalls.length<br>    });<br>  });<br><br>  next();<br>};` |
| **Security Event Logging** | Log security-related events for audit and compliance | - Security event classification<br>- Immutable audit logs<br>- Real-time security monitoring<br>- Compliance reporting | ```json<br>{<br>  "monitoring": {<br>    "security": {<br>      "eventLogging": {<br>        "enabled": true,<br>        "events": ["login", "logout", "permission_denied", "data_access", "config_change"],<br>        "retention": "365d",<br>        "immutable": true,<br>        "integrity": "checksum"<br>      },<br>      "monitoring": {<br>        "failedLoginAttempts": {<br>          "threshold": 5,<br>          "window": "15m",<br>          "action": "lockout"<br>        },<br>        "unusualAccess": {<br>          "enabled": true,<br>          "baseline": "30d"<br>        }<br>      }<br>    }<br>  }<br>}``` | **Security Event Logging:**<br>`// Security event logging<br>const logSecurityEvent = (eventType, details, user) => {<br>  const event = {<br>    id: generateUUID(),<br>    timestamp: new Date().toISOString(),<br>    eventType,<br>    userId: user?.id,<br>    userRole: user?.role,<br>    ip: user?.lastLoginIp,<br>    userAgent: user?.lastLoginUserAgent,<br>    details,<br>    checksum: generateChecksum(eventType + JSON.stringify(details))<br>  };<br><br>  // Store in immutable log<br>  securityLogger.log(event);<br><br>  // Check for suspicious patterns<br>  if (eventType === 'login_failed') {<br>    checkForSuspiciousActivity(user?.id, details.ip);<br>  }<br>};`<br><br>**Usage in Authentication:**<br>`// After failed login attempt<br>logSecurityEvent('login_failed', {<br>  email: req.body.email,<br>  reason: 'invalid_credentials'<br>});` |
| **Audit Trail for Sensitive Operations** | Maintain a comprehensive audit trail for sensitive operations and data access | - Operation logging with before/after state<br>- Data change tracking<br>- User activity monitoring<br>- Compliance reporting | ```json<br>{<br>  "monitoring": {<br>    "audit": {<br>      "enabled": true,<br>      "operations": ["create", "update", "delete", "read_sensitive"],<br>      "entities": ["user", "customer", "order", "payment"],<br>      "sensitiveFields": ["password", "credit_card", "personal_identification"],<br>      "retention": "7y",<br>  }<br>  }<br>}``` | **Audit Trail Implementation:**<br>`// Audit middleware for sensitive operations<br>const auditMiddleware = (operation, entity) => {<br>  return (req, res, next) => {<br>    const originalMethod = res[operation];<br>    let beforeState = null;<br><br>    // Capture before state for update operations<br>    if (operation === 'update') {<br>      beforeState = await getCurrentState(entity, req.params.id);<br>    }<br><br>    res[operation] = async function(data) {<br>      try {<br>        const result = await originalMethod.call(this, data);<br>        <br>        // Log audit event<br>        await auditService.log({<br>          operation,<br>          entity,<br>          entityId: req.params.id || result.id,<br>          userId: req.user.id,<br>          timestamp: new Date().toISOString(),<br>          beforeState,<br>          afterState: operation === 'delete' ? null : result,<br>          metadata: {<br>            ip: req.ip,<br>            userAgent: req.get('User-Agent'),<br>            endpoint: req.path<br>          }<br>        });<br><br>        return result;<br>      } catch (error) {<br>        // Log failed operation<br>        await auditService.log({<br>          operation,<br>          entity,<br>          entityId: req.params.id,<br>          userId: req.user.id,<br>          timestamp: new Date().toISOString(),<br>          beforeState,<br>          afterState: null,<br>          error: error.message,<br>          metadata: {<br>            ip: req.ip,<br>            userAgent: req.get('User-Agent'),<br>            endpoint: req.path<br>          }<br>        });<br><br>        throw error;<br>      }<br>    };<br><br>    next();<br>  };<br>};`<br><br>**Usage:**<br>`router.put('/customers/:id', auditMiddleware('update', 'customer'), updateCustomerHandler);` |

---

## 7. SECURITY ARCHITECTURE

### 7.1 Security Overview
LaundryKu Management System mengimplementasikan security model berlapis (defense-in-depth) dengan pendekatan Zero Trust Architecture. Setiap lapisan memiliki kontrol keamanan yang komprehensif untuk melindungi data, sistem, dan pengguna.

### 7.2 Authentication & Authorization

#### 7.2.1 Authentication Methods
- **JWT (JSON Web Tokens)**: Stateless authentication dengan expiry time
- **OAuth 2.0/OpenID Connect**: Untuk social login dan enterprise SSO
- **Multi-Factor Authentication (MFA)**: SMS, Email, Authenticator App
- **Biometric Authentication**: Fingerprint, Face ID untuk mobile apps
- **API Keys**: Untuk third-party integrations

#### 7.2.2 Authorization Model
**Role-Based Access Control (RBAC) dengan Attribute-Based Access Control (ABAC)**

**Role Definitions:**
- **Super Admin**: Full system access, all permissions
- **Laundry Owner**: Full access to assigned laundry(s)
- **Manager**: Operational management, reporting access
- **Staff**: Order management, limited customer access
- **Driver**: Order status updates, location tracking
- **Customer**: Self-service, own data access

**Permission Categories:**
- Order Management (create, read, update, delete)
- Customer Management (create, read, update, delete)
- Financial Management (read, write, approve)
- System Configuration (read, write)
- Reporting (read, create, export)

#### 7.2.3 Session Management
- JWT token with configurable expiry (default: 24 hours)
- Refresh token rotation for extended sessions
- Session invalidation on logout or password change
- Concurrent session limits per user
- Session activity monitoring

### 7.3 Data Security

#### 7.3.1 Encryption Strategy
**Data at Rest:**
- Database encryption using AES-256
- File storage encryption
- Backup encryption
- Full disk encryption for servers

**Data in Transit:**
- TLS 1.3 for all communications
- Certificate pinning for mobile apps
- Mutual TLS (mTLS) for service-to-service communication

**Key Management:**
- Hardware Security Modules (HSM) for production
- Key rotation every 90 days
- Separation of duties for key management
- Audit logging for all key operations

#### 7.3.2 Data Classification
**Highly Confidential:**
- Customer PII (Personally Identifiable Information)
- Payment information
- Authentication credentials
- Encryption keys

**Confidential:**
- Financial records
- Business intelligence
- Internal communications
- Customer preferences

**Internal:**
- Operational data
- Performance metrics
- System logs
- User activity logs

**Public:**
- Marketing materials
- Product documentation
- Public website content

#### 7.3.3 Data Masking
- Dynamic data masking for sensitive database columns
- Field-level encryption for sensitive fields
- Tokenization for payment data
- Anonymization for analytics and reporting

### 7.4 Network Security

#### 7.4.1 Network Architecture
- **Public Subnet**: Load balancers, API gateway
- **Private Subnet**: Application servers, databases
- **Database Subnet**: Database servers, backup systems
- **Management Subnet**: Management tools, monitoring

#### 7.4.2 Firewall Configuration
**Inbound Rules:**
- HTTPS (443) from anywhere
- SSH (22) from bastion hosts only
- Database ports from application subnet only

**Outbound Rules:**
- HTTPS to external services
- Database connections to database subnet
- Monitoring to monitoring services

**Service-to-Service:**
- Auth Service → All services
- Order Service → Customer Service
- Payment Service → External payment gateways

#### 7.4.3 DDoS Protection
- Cloudflare WAF for web application protection
- Rate limiting at edge
- Bot detection and mitigation
- Traffic anomaly detection
- Automatic attack mitigation

### 7.5 Application Security

#### 7.5.1 Input Validation
- Comprehensive request validation
- Parameterized queries to prevent SQL injection
- Output encoding to prevent XSS
- File type validation for uploads
- Size limits for all inputs

#### 7.5.2 Security Headers
- Strict-Transport-Security (HSTS)
- Content-Security-Policy (CSP)
- X-Content-Type-Options
- X-Frame-Options
- X-XSS-Protection

#### 7.5.3 Error Handling
- Generic error messages for users
- Detailed error logging for debugging
- No sensitive information in error responses
- Proper HTTP status codes
- Error rate monitoring

### 7.6 API Security

#### 7.6.1 API Gateway Security
- Authentication and authorization
- Rate limiting and throttling
- Request/response transformation
- API versioning
- Monitoring and analytics

#### 7.6.2 API Security Features
- JWT validation and introspection
- OAuth 2.0 token validation
- API key management
- IP whitelisting/blacklisting
- Request signing for sensitive operations

#### 7.6.3 Webhook Security
- HMAC signatures for webhook validation
- IP whitelisting for webhook endpoints
- Request replay protection
- Webhook failure handling

### 7.7 Infrastructure Security

#### 7.7.1 Container Security
- Minimal base images
- Regular security scanning
- Read-only filesystems where possible
- Non-root user execution
- Resource limits and quotas

#### 7.7.2 Kubernetes Security
- Pod Security Policies
- Network Policies
- RBAC for cluster access
- Secrets management
- Image security scanning

#### 7.7.3 Infrastructure as Code Security
- Terraform security scanning
- Infrastructure configuration validation
- Secret management in IaC
- Environment separation
- Change management procedures

### 7.8 Monitoring & Detection

#### 7.8.1 Security Monitoring
- Real-time security event monitoring
- Intrusion detection system
- File integrity monitoring
- Network traffic analysis
- User behavior analytics

#### 7.8.2 Logging and Audit
- Comprehensive audit trails
- Immutable log storage
- Log aggregation and analysis
- Security event correlation
- Compliance reporting

#### 7.8.3 Incident Response
- Incident response team
- Defined escalation procedures
- Communication protocols
- Forensic analysis capabilities
- Post-incident reviews

### 7.9 Compliance & Governance

#### 7.9.1 Regulatory Compliance
- PDPR (Personal Data Protection Regulation) Indonesia
- GDPR for international customers
- Payment card industry (PCI) standards
- Data localization requirements
- Industry-specific regulations

#### 7.9.2 Security Policies
- Access Control Policy
- Data Protection Policy
- Incident Response Policy
- Acceptable Use Policy
- Security Awareness Training

#### 7.9.3 Risk Management
- Regular security assessments
- Penetration testing
- Vulnerability scanning
- Risk assessment and mitigation
- Business continuity planning

---

## 8. TECHNOLOGY STACK LENGKAP

### 8.1 Frontend Technology Stack

#### 8.1.1 Admin Web Application
**Core Technologies:**
- **Framework**: Next.js 14+ with TypeScript
    - Server-side rendering (SSR) and static site generation (SSG)
    - API routes for backend functionality
    - Built-in optimizations and performance features

- **UI Library**: Material-UI (MUI) 5+ with Emotion
    - Comprehensive component library
    - Theme customization
    - Accessibility features

- **State Management**: Redux Toolkit with RTK Query
    - Predictable state container
    - Caching and invalidation
    - Code generation for API slices

**Development Tools:**
- **Build Tool**: Vite for fast development builds
- **Package Manager**: npm or yarn
- **Testing**: Jest + React Testing Library + Cypress
- **Code Quality**: ESLint + Prettier + Husky
- **Type Checking**: TypeScript strict mode

**Specialized Libraries:**
- **Charts & Visualization**: Chart.js dengan React wrapper
- **Forms**: React Hook Form dengan Zod validation
- **Date Handling**: date-fns
- **Internationalization**: next-i18next
- **Real-time Updates**: Socket.io Client

#### 8.1.2 Staff Mobile Application
**Native Development (Recommended):**
- **iOS**: Swift 5+ dengan SwiftUI
    - Modern declarative UI framework
    - Native performance and integration
    - Apple ecosystem features

- **Android**: Kotlin dengan Jetpack Compose
    - Modern Android UI toolkit
    - Coroutines for async programming
    - Material Design 3 components

**Cross-platform Alternative:**
- **Framework**: React Native 0.72+ dengan TypeScript
    - Code sharing between platforms
    - Large ecosystem and community
    - Native module support

**Core Libraries:**
- **Navigation**: React Navigation 6+
- **State Management**: Redux Toolkit atau Zustand
- **Networking**: Axios dengan interceptors
- **Storage**: AsyncStorage + SecureStore
- **Maps**: React Native Maps
- **Camera**: React Native Vision Camera
- **Push Notifications**: @react-native-firebase/messaging

#### 8.1.3 Customer Mobile Application
**Technology Options:**
- **Option 1 (Premium Tier)**: Native development (SwiftUI + Jetpack Compose)
- **Option 2 (Pro/Basic Tier)**: React Native atau Flutter

**React Native Stack:**
- Framework: React Native 0.72+
- Language: TypeScript
- Navigation: React Navigation 6
- State: Redux Toolkit + Persist
- UI: React Native Paper
- Networking: Axios + Redux Toolkit Query
- Storage: AsyncStorage + MMKV
- Maps: React Native Maps
- Payments: React Native IAP
- Push: @react-native-firebase/messaging
- Camera: React Native Vision Camera
- Biometrics: React Native Biometrics
- Localization: react-native-localize

**Flutter Stack:**
- Framework: Flutter 3.16+
- Language: Dart 3.2+
- State: BLoC + Provider
- UI: Material Design 3 + Cupertino
- Navigation: GoRouter 2.0
- Networking: Dio
- Storage: Hive + Secure Storage
- Maps: google_maps_flutter
- Payments: in_app_purchase
- Push: firebase_messaging
- Camera: camera
- Biometrics: local_auth
- Localization: flutter_intl

### 8.2 Backend Technology Stack

#### 8.2.1 Primary Backend
**Node.js with NestJS:**
- Framework: NestJS 10+
- Runtime: Node.js 18+
- Language: TypeScript 5+

**Core Modules:**
- @nestjs/core
- @nestjs/common
- @nestjs/platform-express
- @nestjs/config
- @nestjs/jwt
- @nestjs/passport
- @nestjs/throttler
- @nestjs/swagger

**Database:**
- ORM: Prisma 5+
- Database: PostgreSQL 15+
- Cache: Redis 7+

**Security:**
- Authentication: Passport.js
- Authorization: CASL
- Encryption: bcrypt + crypto
- Validation: class-validator

**Testing:**
- Unit: Jest
- E2E: Supertest
- Coverage: Istanbul

**Monitoring:**
- Logging: Winston
- Metrics: Prometheus
- Tracing: OpenTelemetry

#### 8.2.2 Alternative Backend (Python)
**FastAPI Stack:**
- Framework: FastAPI 0.100+
- Runtime: Python 3.11+
- Language: Python

**Core Dependencies:**
- fastapi
- uvicorn
- pydantic
- sqlalchemy
- alembic
- redis
- celery

**Database:**
- ORM: SQLAlchemy 2.0
- Database: PostgreSQL 15+
- Cache: Redis 7+

**Security:**
- Authentication: OAuth2 with Password Flow
- Authorization: CASL Python
- Encryption: passlib + cryptography
- Validation: Pydantic

**Testing:**
- Unit: pytest
- E2E: httpx
- Coverage: pytest-cov

**Monitoring:**
- Logging: structlog
- Metrics: prometheus-client
- Tracing: OpenTelemetry

### 8.3 Database Technology Stack

#### 8.3.1 Primary Database (PostgreSQL)
**Configuration:**
- Version: PostgreSQL 15+
- Extensions: PostGIS, TimescaleDB, pgcrypto, uuid-ossp, pg_stat_statements
- Connection Pooling: PgBouncer
- Backup: pgBackRest
- Monitoring: pgAdmin + Prometheus Exporter

**Schema Design:**
- UUID primary keys
- JSONB for flexible data
- Partitioning for large tables
- Indexing strategy for performance
- Foreign key constraints for integrity

#### 8.3.2 Cache Layer (Redis)
**Configuration:**
- Version: Redis 7+
- Architecture: Cluster mode for high availability
- Memory: 64GB per node (scalable)
- Persistence: RDB + AOF
- Security: AUTH + TLS encryption
- Monitoring: Redis Exporter + RedisInsight

**Use Cases:**
- Session storage
- Rate limiting
- Query result caching
- Real-time data
- Pub/Sub messaging
- Leaderboards

#### 8.3.3 Search Engine (Elasticsearch)
**Configuration:**
- Version: Elasticsearch 8+
- Architecture: Cluster with 3+ nodes
- Security: Built-in security with TLS
- Monitoring: Elastic Stack (ELK)
- Indexing: Daily indices with ILM

**Use Cases:**
- Full-text search
- Analytics and aggregations
- Log aggregation
- Monitoring dashboards
- Machine learning features

#### 8.3.4 Time-Series Database (InfluxDB)
**Configuration:**
- Version: InfluxDB 2.0+
- Architecture: Cluster with high availability
- Storage: TSI engine for efficient time-series
- Security: Authentication and authorization
- Monitoring: Built-in monitoring and alerting

**Use Cases:**
- Metrics and monitoring
- IoT data
- Performance metrics
- Business analytics
- Real-time dashboards

### 8.4 Infrastructure & DevOps Stack

#### 8.4.1 Cloud Infrastructure (AWS)
**Core Services:**
- **Compute**: EKS (Elastic Kubernetes Service), EC2 instances, Fargate
- **Storage**: S3, EBS, EFS, Glacier
- **Networking**: VPC, ALB, NLB, CloudFront, Route 53
- **Database**: RDS, ElastiCache, OpenSearch, Timestream
- **Security**: IAM, KMS, Secrets Manager, WAF, Shield

#### 8.4.2 Container Orchestration
**Kubernetes Stack:**
- Orchestration: Kubernetes 1.28+
- Distribution: Amazon EKS
- Networking: Calico CNI
- Ingress: Nginx Ingress Controller + ALB Ingress Controller
- Storage: EBS CSI Driver + EFS CSI Driver
- Monitoring: Prometheus Operator + Grafana
- Logging: Fluentd + Elasticsearch + Kibana
- Security: Pod Security Policies + Network Policies
- CI/CD: ArgoCD for GitOps deployments

#### 8.4.3 CI/CD Pipeline
**GitHub Actions Workflow:**
- Automated testing on every push
- Security scanning with Snyk and Trivy
- Docker image building and pushing to ECR
- Automated deployment to EKS on main branch
- Rollback capabilities
- Environment-specific deployments

#### 8.4.4 Infrastructure as Code
**Terraform Configuration:**
- AWS provider configuration
- VPC with public/private subnets
- EKS cluster configuration
- Managed node groups
- Security groups and network ACLs
- IAM roles and policies
- S3 buckets and DynamoDB tables

### 8.5 Monitoring & Observability Stack

#### 8.5.1 Monitoring Stack
**Prometheus + Grafana:**
- Prometheus for metrics collection
- Grafana for visualization and dashboards
- Alertmanager for alerting
- Exporters for various services
- Pre-configured dashboards for application metrics

#### 8.5.2 Logging Stack
**ELK Stack:**
- Elasticsearch for log storage and search
- Logstash for log processing and enrichment
- Kibana for log visualization and analysis
- Filebeat for log collection
- Centralized log management

#### 8.5.3 Distributed Tracing
**OpenTelemetry Stack:**
- OpenTelemetry Collector for telemetry collection
- Jaeger for distributed tracing
- Application instrumentation with OpenTelemetry SDK
- Performance analysis and optimization
- Root cause analysis for issues

### 8.6 Security Stack

#### 8.6.1 Security Tools
**Static Application Security Testing (SAST):**
- SonarQube for code quality and security
- Snyk for vulnerability scanning
- CodeQL for semantic code analysis

**Dynamic Application Security Testing (DAST):**
- OWASP ZAP for web application scanning
- Burp Suite for penetration testing
- Nessus for network vulnerability scanning

**Container Security:**
- Trivy for container image scanning
- Clair for vulnerability analysis
- Falco for runtime security monitoring

#### 8.6.2 Identity and Access Management
**Authentication:**
- Auth0 or Keycloak for identity management
- Multi-factor authentication
- Social login integration
- Single sign-on (SSO)

**Authorization:**
- Open Policy Agent (OPA) for policy decisions
- Role-based access control (RBAC)
- Attribute-based access control (ABAC)
- Fine-grained permissions

**Secrets Management:**
- HashiCorp Vault for secrets storage
- AWS Secrets Manager for AWS-specific secrets
- Automatic secret rotation
- Audit logging for secret access

### 8.7 Development Environment Stack

#### 8.7.1 Local Development
**Docker Compose Setup:**
- Containerized local development environment
- PostgreSQL database
- Redis cache
- Application services
- Development tools and utilities

#### 8.7.2 Development Tools
**VS Code Configuration:**
- TypeScript and React extensions
- Prettier and ESLint integration
- Docker and Kubernetes tools
- Git integration and version control
- Debugging and testing tools

### 8.8 Testing Stack

#### 8.8.1 Testing Framework
**JavaScript/TypeScript:**
- Unit Testing: Jest with comprehensive test coverage
- Integration Testing: Supertest with Testcontainers
- E2E Testing: Cypress for end-to-end testing
- Performance Testing: k6 for load and stress testing

**Python:**
- Unit Testing: pytest with mocking capabilities
- Integration Testing: httpx for HTTP testing
- E2E Testing: Playwright for browser automation
- Performance Testing: Locust for load testing

#### 8.8.2 Testing Configuration
**Test Environment:**
- Dedicated test databases
- Mock external services
- Test data management
- Parallel test execution
- Test result reporting

### 8.9 Documentation Stack

#### 8.9.1 API Documentation
**OpenAPI/Swagger:**
- Automatic generation from code annotations
- Interactive API documentation with Swagger UI
- Client SDK generation
- API testing integration
- Version management

#### 8.9.2 Project Documentation
**Architecture Documentation:**
- C4 Model diagrams with PlantUML
- Architecture Decision Records (ADRs)
- System design documents
- API specification documents

**Developer Documentation:**
- MkDocs for static site generation
- Markdown for documentation format
- Diagrams with Mermaid.js
- Code examples and tutorials

**User Documentation:**
- Docusaurus for user guides
- Video tutorials with screen recordings
- Interactive walkthroughs
- FAQ and troubleshooting guides

---

## 9. UI/UX DESIGN SPECIFICATIONS

### 9.1 Design System & Guidelines

#### 9.1.1 Design Philosophy
**Core Principles:**
- **User-Centric**: Setiap keputusan desain didasarkan pada kebutuhan dan perilaku pengguna
- **Accessibility**: Desain yang dapat diakses oleh semua pengguna (WCAG 2.1 AA compliant)
- **Consistency**: Pengalaman yang konsisten di semua platform dan perangkat
- **Efficiency**: Meminimalkan langkah dan waktu untuk menyelesaikan tugas
- **Clarity**: Informasi yang jelas dan mudah dipahami

#### 9.1.2 Design Tokens
**Color Palette:**
- Primary Colors: Blue gradient (#0ea5e9 to #0369a1)
- Secondary Colors: Neutral grays (#71717a to #18181b)
- Status Colors: Green (#22c55e), Amber (#f59e0b), Red (#ef4444)
- Background Colors: Light grays (#f8fafc to #f1f5f9)

**Typography:**
- Font Family: Inter for body, JetBrains Mono for code
- Font Sizes: 12px to 36px with responsive scaling
- Font Weights: 400 (Regular), 500 (Medium), 600 (Semibold), 700 (Bold)
- Line Heights: 1.25 (tight), 1.5 (normal), 1.75 (relaxed)

**Spacing System:**
- Base Unit: 4px (0.25rem)
- Scale: 0, 4, 8, 12, 16, 24, 32, 48, 64, 96, 128px
- Responsive spacing for different screen sizes

**Border Radius:**
- Small: 4px
- Medium: 8px
- Large: 12px
- Extra Large: 16px
- Full: 9999px (for circles)

**Shadows:**
- Subtle: 0 1px 2px rgba(0,0,0,0.05)
- Medium: 0 4px 6px rgba(0,0,0,0.1)
- Large: 0 10px 15px rgba(0,0,0,0.1)
- Extra Large: 0 20px 25px rgba(0,0,0,0.1)

#### 9.1.3 Component Library
**Core Components:**
- Buttons (Primary, Secondary, Outline, Ghost, Danger)
- Inputs (Text, Email, Password, Number, Select, Textarea)
- Cards (Basic, Elevated, Interactive)
- Modals (Dialog, Form, Confirmation)
- Navigation (Header, Sidebar, Breadcrumbs)
- Tables (Basic, Sortable, Selectable)
- Forms (Form groups, Validation, Error handling)
- Charts (Line, Bar, Pie, Area)
- Lists (Basic, Interactive, Virtualized)

### 9.2 Admin Web Application Design

#### 9.2.1 Layout Structure
**Main Layout:**
- Fixed header with navigation and user controls
- Collapsible sidebar with main navigation
- Main content area with breadcrumbs
- Optional footer with quick links

**Navigation Structure:**
- Primary Navigation: Dashboard, Orders, Customers, Services, Analytics, Settings
- Secondary Navigation: Contextual sub-menus
- Quick Actions: Floating action buttons for common tasks
- Breadcrumbs: Location indicator and navigation

#### 9.2.2 Dashboard Design
**Dashboard Sections:**
- **Key Metrics**: Revenue, Orders, Customers, Satisfaction rate
- **Charts**: Revenue trend, Order volume, Customer growth
- **Recent Activity**: Recent orders, customer feedback, system alerts
- **Quick Actions**: Create order, Add customer, Generate report

**Dashboard Cards:**
- Metric cards with trend indicators
- Chart cards with interactive controls
- Activity feed with real-time updates
- Quick action cards with clear CTAs

#### 9.2.3 Forms Design
**Form Principles:**
- Progressive disclosure for complex forms
- Clear labeling and instructions
- Real-time validation feedback
- Save progress functionality
- Mobile-responsive layout

**Form Types:**
- Order creation form with service selection
- Customer registration with address management
- Service configuration with pricing setup
- User management with role assignment

#### 9.2.4 Data Tables
**Table Features:**
- Sorting and filtering capabilities
- Column customization and reordering
- Pagination with infinite scroll option
- Row selection and bulk actions
- Export functionality (CSV, Excel, PDF)

**Table Types:**
- Orders table with status indicators
- Customers table with loyalty tier badges
- Services table with pricing information
- Users table with role indicators

### 9.3 Mobile Application Design

#### 9.3.1 Customer Mobile App Design
**App Structure:**
- Bottom navigation with 4-5 main sections
- Tab-based navigation for content sections
- Swipe gestures for navigation
- Pull-to-refresh functionality
- Floating action buttons for primary actions

**Main Sections:**
- **Home**: Quick actions, recent orders, promotions
- **Orders**: Order list, tracking, history
- **Services**: Service catalog, pricing, booking
- **Profile**: Account settings, preferences, loyalty

**Key Features:**
- Real-time order tracking with map integration
- Push notifications for order updates
- In-app chat support
- Digital wallet integration
- QR code scanning for order pickup

#### 9.3.2 Staff Mobile App Design
**App Structure:**
- Task-oriented navigation
- Priority-based task organization
- Quick access to common functions
- Offline capability for field operations
- Camera integration for documentation

**Main Sections:**
- **Dashboard**: Today's tasks, performance metrics
- **Orders**: Order assignment, status updates
- **Schedule**: Work schedule, time tracking
- **Tools**: Scanner, calculator, reference materials

**Key Features:**
- Order status updates with photo documentation
- GPS tracking for delivery optimization
- Digital signature capture
- Barcode/QR code scanning
- Offline data synchronization

### 9.4 Accessibility Guidelines

#### 9.4.1 Visual Accessibility
- Color contrast ratio of at least 4.5:1 for normal text
- Sufficient color contrast for interactive elements
- Clear visual hierarchy with proper spacing
- Responsive text sizing
- High contrast mode support

#### 9.4.2 Motor Accessibility
- Large touch targets (minimum 44x44px)
- Keyboard navigation support
- Sufficient time limits for interactions
- Error prevention and recovery
- Gesture alternatives

#### 9.4.3 Cognitive Accessibility
- Clear and simple language
- Consistent navigation patterns
- Progressive disclosure of information
- Error prevention and clear feedback
- Help and documentation availability

#### 9.4.4 Screen Reader Support
- Proper ARIA labels and roles
- Semantic HTML structure
- Alternative text for images
- Screen reader testing
- Keyboard-only navigation

### 9.5 Responsive Design

#### 9.5.1 Breakpoint Strategy
- **Mobile**: 320px - 768px
- **Tablet**: 768px - 1024px
- **Desktop**: 1024px - 1440px
- **Large Desktop**: 1440px+

#### 9.5.2 Responsive Patterns
- **Mobile-First**: Design for mobile first, then enhance for larger screens
- **Fluid Layouts**: Use relative units and flexible grids
- **Progressive Enhancement**: Start with basic functionality, add features for capable devices
- **Touch-Friendly**: Large touch targets and gesture support

#### 9.5.3 Device Considerations
- **Mobile**: Optimized for touch, offline capability, location services
- **Tablet**: Split-screen layouts, enhanced interactions
- **Desktop**: Complex layouts, keyboard shortcuts, multiple windows

### 9.6 Interaction Design

#### 9.6.1 Interaction Patterns
- **Direct Manipulation**: Drag and drop, swipe gestures
- **Progressive Disclosure**: Expandable sections, accordions
- **Inline Editing**: Click to edit, save/cancel actions
- **Contextual Actions**: Hover states, right-click menus
- **Feedback Loops**: Loading states, success/error messages

#### 9.6.2 Animation Guidelines
- **Purposeful**: Animations should serve a purpose
- **Subtle**: Avoid distracting or excessive animations
- **Performant**: 60fps animations with hardware acceleration
- **Accessible**: Respect user preferences for reduced motion
- **Consistent**: Follow platform animation patterns

#### 9.6.3 Error Handling
- **Prevention**: Input validation, confirmations for destructive actions
- **Clear Messaging**: Specific error messages with suggested solutions
- **Recovery**: Easy ways to correct errors and retry actions
- **Non-blocking**: Errors shouldn't prevent users from continuing their work
- **Learning**: Help users understand and avoid future errors

---

## 10. IMPLEMENTATION ROADMAP

### 10.1 Project Timeline Overview

#### 10.1.1 Total Duration: 12 Months
- **Phase 1**: MVP Development (Months 1-3)
- **Phase 2**: Core Features (Months 4-6)
- **Phase 3**: Advanced Features (Months 7-9)
- **Phase 4**: Enterprise Features (Months 10-12)

### 10.2 Phase 1: MVP Development (Months 1-3)

#### 10.2.1 Objectives
- Develop minimum viable product with core functionality
- Validate product-market fit
- Establish technical foundation
- Onboard initial beta customers

#### 10.2.2 Key Deliverables
**Month 1: Foundation**
- Project setup and architecture design
- Database schema design
- Authentication system
- Basic user management
- API framework setup

**Month 2: Core Features**
- Order management system
- Customer management
- Basic service catalog
- Payment integration (single gateway)
- Admin dashboard basics

**Month 3: Mobile & Testing**
- Customer mobile app (MVP version)
- Staff mobile app (basic functionality)
- Testing and quality assurance
- Beta customer onboarding
- Performance optimization

#### 10.2.3 Success Criteria
- 5+ beta customers successfully onboarded
- Core order flow working end-to-end
- Mobile apps functional for basic operations
- Payment processing working reliably
- Performance benchmarks met (response time < 2s)

### 10.3 Phase 2: Core Features (Months 4-6)

#### 10.3.1 Objectives
- Build out core business features
- Enhance mobile applications
- Implement basic analytics
- Expand integration capabilities

#### 10.3.2 Key Deliverables
**Month 4: Business Logic**
- Advanced order management
- Loyalty program implementation
- Subscription management system
- Inventory management basics
- Reporting system foundation

**Month 5: Mobile Enhancement**
- Full-featured customer mobile app
- Enhanced staff mobile app
- Push notification system
- Real-time order tracking
- Offline capability

**Month 6: Integration & Analytics**
- Multi-payment gateway integration
- Basic analytics dashboard
- API for third-party integrations
- Advanced reporting features
- System monitoring setup

#### 10.3.3 Success Criteria
- 20+ active customers using Pro tier
- Mobile apps with 4+ star ratings
- Payment processing with 99.9% uptime
- Basic analytics providing business insights
- Integration with 2+ marketplaces

### 10.4 Phase 3: Advanced Features (Months 7-9)

#### 10.4.1 Objectives
- Implement advanced business features
- AI and machine learning capabilities
- Enterprise-grade security
- Scalability improvements

#### 10.4.2 Key Deliverables
**Month 7: AI & Automation**
- Predictive analytics implementation
- Route optimization algorithms
- Automated scheduling system
- Quality control automation
- Customer segmentation AI

**Month 8: Enterprise Features**
- Multi-branch management
- Advanced user permissions
- Audit trail system
- Advanced security features
- Compliance tools

**Month 9: Performance & Scale**
- System performance optimization
- Scalability improvements
- Advanced monitoring
- Disaster recovery implementation
- Load testing and optimization

#### 10.4.3 Success Criteria
- 50+ active customers across all tiers
- AI features providing measurable business value
- System handling 10x growth without degradation
- Enterprise customers successfully onboarded
- Security audit passed with no critical findings

### 10.5 Phase 4: Enterprise Features (Months 10-12)

#### 10.5.1 Objectives
- Complete enterprise feature set
- White-label solution
- Advanced integrations
- Market expansion preparation

#### 10.5.2 Key Deliverables
**Month 10: White-Label & Customization**
- White-label solution implementation
- Custom branding capabilities
- Advanced customization options
- Template system for UI customization
- Multi-language support

**Month 11: Advanced Integrations**
- Full API ecosystem
- Advanced third-party integrations
- Webhook system
- Developer portal
- SDK for third-party developers

**Month 12: Market Expansion**
- Internationalization features
- Multi-currency support
- Market-specific adaptations
- Go-to-market strategy
- Customer success program

#### 10.5.3 Success Criteria
- 100+ active customers including enterprise clients
- White-label solution deployed for 5+ clients
- API ecosystem with 10+ third-party integrations
- System ready for international expansion
- Customer satisfaction score > 90%

### 10.6 Resource Planning

#### 10.6.1 Team Structure
**Core Development Team:**
- 1 Project Manager
- 1 Tech Lead/Architect
- 4 Full-Stack Developers
- 2 Mobile Developers (iOS/Android)
- 1 UI/UX Designer
- 2 QA Engineers
- 1 DevOps Engineer

**Support Team:**
- 1 Product Manager
- 1 Customer Success Manager
- 1 Technical Support Engineer
- 1 Marketing Specialist

#### 10.6.2 Skill Requirements
**Technical Skills:**
- Backend: Node.js/NestJS, PostgreSQL, Redis, Kubernetes
- Frontend: React, Next.js, TypeScript, Material-UI
- Mobile: React Native, Swift, Kotlin
- DevOps: AWS, Docker, Kubernetes, Terraform
- Testing: Jest, Cypress, performance testing

**Domain Knowledge:**
- Laundry industry operations
- Subscription business models
- Payment processing
- Logistics and delivery management
- Customer relationship management

#### 10.6.3 Infrastructure Requirements
**Development Environment:**
- Development servers
- Staging environment
- Testing environment
- CI/CD pipeline
- Code repository and project management tools

**Production Environment:**
- Cloud infrastructure (AWS)
- Database clusters
- Application servers
- CDN and caching
- Monitoring and logging
- Backup and disaster recovery

### 10.7 Risk Management

#### 10.7.1 Technical Risks
**Risk: Performance Issues**
- **Mitigation**: Regular load testing, performance monitoring, optimization sprints
- **Contingency**: Auto-scaling, caching strategies, database optimization

**Risk: Security Vulnerabilities**
- **Mitigation**: Regular security audits, penetration testing, secure coding practices
- **Contingency**: Incident response plan, security monitoring, quick patch deployment

**Risk: Integration Failures**
- **Mitigation**: Thorough testing, fallback mechanisms, circuit breakers
- **Contingency**: Manual processes, alternative integrations, vendor support

#### 10.7.2 Business Risks
**Risk: Market Adoption**
- **Mitigation**: Beta testing program, customer feedback loops, iterative improvements
- **Contingency**: Pivot strategy, alternative markets, pricing adjustments

**Risk: Competition**
- **Mitigation**: Continuous innovation, unique value proposition, customer loyalty
- **Contingency**: Differentiation strategy, partnerships, acquisition opportunities

**Risk: Resource Constraints**
- **Mitigation**: Phased development, prioritization, outsourcing non-core tasks
- **Contingency**: Additional funding, team expansion, timeline adjustments

#### 10.7.3 Project Risks
**Risk: Timeline Delays**
- **Mitigation**: Agile methodology, regular progress tracking, buffer time allocation
- **Contingency**: Feature prioritization, scope reduction, additional resources

**Risk: Budget Overruns**
- **Mitigation**: Detailed budgeting, regular financial reviews, cost optimization
- **Contingency**: Additional funding, scope reduction, phased delivery

**Risk: Quality Issues**
- **Mitigation**: Comprehensive testing, code reviews, quality gates
- **Contingency**: Bug fixing sprints, customer communication, compensation

### 10.8 Quality Assurance

#### 10.8.1 Testing Strategy
**Testing Types:**
- Unit Testing: Individual component testing
- Integration Testing: Service interaction testing
- End-to-End Testing: Complete user flow testing
- Performance Testing: Load and stress testing
- Security Testing: Vulnerability assessment
- Usability Testing: User experience validation

**Testing Environment:**
- Development: Local testing with mocked services
- Staging: Production-like environment with real data
- Production: Canary deployments and monitoring

#### 10.8.2 Quality Gates
**Code Quality:**
- Code coverage minimum 80%
- Static analysis passing
- Code review approval
- Security scan passing
- Performance benchmarks met

**Release Quality:**
- All automated tests passing
- Manual testing completed
- Performance tests passed
- Security audit passed
- Stakeholder approval

#### 10.8.3 Continuous Improvement
**Feedback Loops:**
- Customer feedback collection
- User analytics monitoring
- Performance metrics tracking
- Error rate monitoring
- Support ticket analysis

**Improvement Process:**
- Regular retrospectives
- Performance optimization sprints
- User experience improvements
- Feature prioritization based on feedback
- Technical debt management

---

## 11. MONITORING & MAINTENANCE

### 11.1 Monitoring Strategy

#### 11.1.1 Monitoring Objectives
- Ensure system availability and performance
- Detect and resolve issues proactively
- Optimize resource utilization
- Maintain security and compliance
- Support business decision-making

#### 11.1.2 Monitoring Categories
**Infrastructure Monitoring:**
- Server health and resource utilization
- Network performance and connectivity
- Database performance and capacity
- Storage utilization and performance
- Container orchestration health

**Application Monitoring:**
- Application performance and response times
- Error rates and exception tracking
- Transaction monitoring and tracing
- User experience metrics
- Business logic monitoring

**Business Monitoring:**
- Key performance indicators (KPIs)
- Revenue and transaction metrics
- Customer acquisition and retention
- Service utilization and capacity
- Business process efficiency

#### 11.1.3 Monitoring Tools Stack
**Infrastructure Monitoring:**
- Prometheus for metrics collection
- Grafana for visualization and dashboards
- Alertmanager for alerting and notifications
- Node Exporter for system metrics
- cAdvisor for container metrics

**Application Monitoring:**
- Application Performance Monitoring (APM) tools
- Distributed tracing with Jaeger
- Real user monitoring (RUM)
- Error tracking with Sentry
- Log aggregation with ELK Stack

**Business Monitoring:**
- Custom business metrics dashboards
- Customer analytics platforms
- Revenue and transaction tracking
- Customer behavior analysis
- Business intelligence tools

### 11.2 Alert Management

#### 11.2.1 Alert Strategy
**Alert Principles:**
- Actionable alerts with clear remediation steps
- Appropriate severity levels and prioritization
- Minimal false positives and noise
- Timely notification and escalation
- Continuous alert optimization

#### 11.2.2 Alert Categories
**Critical Alerts:**
- System downtime or service unavailability
- Security breaches or vulnerabilities
- Data loss or corruption
- Payment processing failures
- Database performance issues

**Warning Alerts:**
- High resource utilization
- Performance degradation
- Error rate increases
- Integration failures
- Capacity approaching limits

**Informational Alerts:**
- Scheduled maintenance
- System updates
- Performance trends
- Business metrics changes
- User activity patterns

#### 11.2.3 Alert Configuration
**Alert Rules:**
- CPU utilization > 80% for 5 minutes
- Memory utilization > 90% for 5 minutes
- Error rate > 5% for 5 minutes
- Response time > 2 seconds for 5 minutes
- Database connections > 80% of pool

**Notification Channels:**
- Email alerts for different severity levels
- SMS alerts for critical issues
- Slack integration for team notifications
- PagerDuty for on-call rotations
- Webhook integrations for custom systems

### 11.3 Log Management

#### 11.3.1 Logging Strategy
**Log Categories:**
- Application logs (debug, info, warn, error)
- Access logs and audit trails
- Security logs and authentication events
- Performance logs and metrics
- Business logic and transaction logs

**Log Standards:**
- Structured logging with JSON format
- Consistent timestamp and timezone
- Request correlation IDs
- User and session information
- Environment and context data

#### 11.3.2 Log Management System
**Log Collection:**
- Fluentd or Filebeat for log collection
- Centralized log aggregation
- Real-time log processing
- Log parsing and enrichment
- Log retention and archiving

**Log Analysis:**
- Elasticsearch for log storage and search
- Kibana for log visualization
- Log-based alerting and monitoring
- Pattern detection and anomaly detection
- Compliance reporting and auditing

### 11.4 Performance Monitoring

#### 11.4.1 Performance Metrics
**Application Performance:**
- Response times (p50, p90, p95, p99)
- Throughput and request rates
- Error rates and failure patterns
- Resource utilization per request
- Database query performance

**Infrastructure Performance:**
- CPU, memory, disk, network utilization
- Database performance and query times
- Cache hit rates and efficiency
- Network latency and throughput
- Storage I/O performance

**Business Performance:**
- Order processing times
- Customer onboarding times
- Payment processing times
- Report generation times
- API response times

#### 11.4.2 Performance Optimization
**Optimization Strategies:**
- Database query optimization and indexing
- Application code profiling and optimization
- Caching strategies and implementation
- Load balancing and horizontal scaling
- Content delivery and edge computing

**Performance Testing:**
- Load testing with realistic user loads
- Stress testing to find breaking points
- Endurance testing for long-term stability
- Spike testing for traffic bursts
- Scalability testing for growth projections

### 11.5 Security Monitoring

#### 11.5.1 Security Monitoring Objectives
- Detect security threats and vulnerabilities
- Monitor compliance with security policies
- Track security incidents and responses
- Maintain audit trails for compliance
- Support forensic analysis and investigation

#### 11.5.2 Security Monitoring Areas
**Access Monitoring:**
- Authentication attempts and failures
- Authorization decisions and violations
- Privileged access and administrative actions
- Session management and token usage
- Multi-factor authentication events

**Network Security:**
- Firewall and intrusion detection alerts
- DDoS attack detection and mitigation
- Malware and virus detection
- Network traffic anomalies
- SSL/TLS certificate monitoring

**Application Security:**
- OWASP Top 10 vulnerability detection
- SQL injection and XSS attempts
- Input validation failures
- Authentication bypass attempts
- Data exfiltration attempts

#### 11.5.3 Security Incident Response
**Incident Response Process:**
- Detection and identification
- Containment and eradication
- Recovery and restoration
- Post-incident analysis
- Prevention and improvement

**Incident Response Tools:**
- SIEM (Security Information and Event Management)
- Incident response platforms
- Forensic analysis tools
- Threat intelligence feeds
- Vulnerability scanners

### 11.6 Backup and Disaster Recovery

#### 11.6.1 Backup Strategy
**Backup Types:**
- Full database backups daily
- Incremental backups hourly
- Configuration backups weekly
- File system backups daily
- Application backups weekly

**Backup Storage:**
- Local storage for quick recovery
- Cloud storage for geographic redundancy
- Off-site storage for disaster recovery
- Encrypted storage for security
- Versioned backups for point-in-time recovery

#### 11.6.2 Disaster Recovery Plan
**Recovery Objectives:**
- RTO (Recovery Time Objective): 4 hours for critical systems
- RPO (Recovery Point Objective): 15 minutes data loss maximum
- RCO (Recovery Capacity Objective): Full system recovery
- RLO (Recovery Level Objective): Minimum functionality recovery
- RSO (Recovery Service Objective): Service level agreements

**Recovery Strategies:**
- High availability with automatic failover
- Geographic redundancy across regions
- Data replication and synchronization
- Backup and restoration procedures
- Disaster recovery testing and validation

### 11.7 Maintenance Procedures

#### 11.7.1 Routine Maintenance
**Daily Maintenance:**
- Log review and analysis
- Performance metrics monitoring
- Security alert review
- Backup verification
- System health checks

**Weekly Maintenance:**
- System updates and patching
- Performance optimization
- Database maintenance
- Security scanning
- Capacity planning

**Monthly Maintenance:**
- Comprehensive system review
- Performance benchmarking
- Security audit preparation
- Backup testing and validation
- Disaster recovery testing

#### 11.7.2 Update Management
**Update Categories:**
- Security patches and updates
- Operating system updates
- Application updates and upgrades
- Database updates and patches
- Third-party library updates

**Update Process:**
- Update assessment and planning
- Testing in staging environment
- Scheduled maintenance windows
- Rollback procedures and testing
- Post-update verification and monitoring

#### 11.7.3 Capacity Management
**Capacity Planning:**
- Resource utilization monitoring
- Growth trend analysis
- Capacity forecasting
- Resource optimization
- Cost optimization

**Scaling Strategies:**
- Vertical scaling for resource-intensive applications
- Horizontal scaling for high-availability applications
- Auto-scaling for variable workloads
- Geographic scaling for global availability
- Cost-effective scaling for budget optimization

---

## 12. FUTURE ENHANCEMENTS & INNOVATION

### 12.1 Technology Roadmap

#### 12.1.1 Short-term Enhancements (12-18 months)
**AI and Machine Learning:**
- Predictive order volume forecasting
- Customer churn prediction and prevention
- Dynamic pricing optimization
- Quality control automation with computer vision
- Route optimization with machine learning

**Mobile Enhancements:**
- Augmented reality for garment visualization
- Voice-activated ordering and status updates
- Advanced biometric authentication
- Offline mode enhancements
- Real-time language translation

**Integration Expansion:**
- Additional marketplace integrations
- Expanded payment gateway support
- Logistics partner integrations
- Accounting software integrations
- ERP system integrations

#### 12.1.2 Medium-term Enhancements (18-36 months)
**Advanced AI Features:**
- Natural language processing for customer service
- Computer vision for stain detection and removal
- Predictive maintenance for equipment
- Customer behavior prediction
- Automated inventory management

**Blockchain Integration:**
- Supply chain transparency and tracking
- Smart contracts for service agreements
- Cryptocurrency payment options
- Loyalty program tokenization
- Secure data sharing with partners

**IoT Integration:**
- Smart washing machine integration
- Environmental monitoring sensors
- Automated chemical dispensing systems
- Real-time equipment monitoring
- Energy consumption optimization

#### 12.1.3 Long-term Vision (36+ months)
**Quantum Computing:**
- Complex optimization problems
- Advanced machine learning models
- Cryptographic security enhancements
- Large-scale data processing
- Real-time simulation and modeling

**Advanced Robotics:**
- Automated sorting and folding systems
- Robotic delivery systems
- Quality inspection robots
- Inventory management robots
- Customer service robots

**Sustainability Features:**
- Carbon footprint tracking and reduction
- Water usage optimization
- Energy consumption monitoring
- Waste reduction systems
- Sustainable practices certification

### 12.2 Market Expansion Strategy

#### 12.2.1 Geographic Expansion
**Southeast Asia Market:**
- Indonesia (current market)
- Malaysia and Singapore expansion
- Thailand and Vietnam market entry
- Philippines market development
- Regional headquarters establishment

**International Expansion:**
- Asia Pacific region expansion
- European market entry
- North American market development
- Global partnership strategy
- International compliance and localization

#### 12.2.2 Vertical Expansion
**Related Services:**
- Dry cleaning specialization
- Garment repair and alteration services
- Uniform rental and management
- Event and special occasion services
- Corporate and institutional services

**Industry Expansion:**
- Hotel and hospitality industry
- Healthcare and medical services
- Food and beverage industry
- Manufacturing and industrial services
- Educational institution services

#### 12.2.3 Business Model Evolution
**Platform Evolution:**
- Marketplace model expansion
- Service provider network
- Franchise opportunities
- White-label solutions
- API platform and ecosystem

**Revenue Streams:**
- Subscription-based revenue
- Transaction fees and commissions
- Marketplace fees
- Advertising and promotion revenue
- Data and analytics services

### 12.3 Innovation Pipeline

#### 12.3.1 Research and Development
**R&D Focus Areas:**
- Artificial intelligence and machine learning
- Internet of Things (IoT) integration
- Blockchain and distributed ledger technology
- Quantum computing applications
- Sustainable and green technology

**Innovation Process:**
- Idea generation and collection
- Feasibility analysis and validation
- Prototype development and testing
- Pilot programs and customer feedback
- Full-scale implementation and deployment

#### 12.3.2 Emerging Technologies
**5G Technology:**
- Enhanced mobile connectivity
- Real-time video streaming for quality control
- IoT device connectivity
- Enhanced customer experiences
- Improved operational efficiency

**Edge Computing:**
- Localized data processing
- Reduced latency for real-time applications
- Improved privacy and security
- Bandwidth optimization
- Offline capability enhancement

**Augmented and Virtual Reality:**
- Virtual laundry facility tours
- AR-based garment care instructions
- VR training for staff
- Enhanced customer experiences
- Remote assistance and support

#### 12.3.3 Sustainability Initiatives
**Environmental Sustainability:**
- Water conservation technologies
- Energy-efficient equipment
- Eco-friendly detergents and chemicals
- Waste reduction and recycling
- Carbon footprint tracking and reduction

**Social Sustainability:**
- Fair labor practices
- Community engagement programs
- Education and training initiatives
- Accessibility and inclusion
- Local economic development

**Economic Sustainability:**
- Cost optimization for customers
- Affordable pricing models
- Small business support
- Job creation and employment
- Economic growth and development

### 12.4 Competitive Strategy

#### 12.4.1 Competitive Advantages
**Technology Leadership:**
- AI and machine learning capabilities
- Advanced automation features
- Innovative mobile applications
- Cutting-edge security features
- Scalable and flexible architecture

**Market Positioning:**
- Premium service quality
- Comprehensive feature set
- Excellent customer support
- Strong brand reputation
- Industry expertise and knowledge

**Ecosystem Strength:**
- Extensive integration capabilities
- Partner network and alliances
- Developer community and ecosystem
- API-first approach
- Open platform architecture

#### 12.4.2 Differentiation Strategy
**Product Differentiation:**
- Unique features and capabilities
- Superior user experience
- Advanced analytics and insights
- Comprehensive integration options
- Customization and flexibility

**Service Differentiation:**
- Exceptional customer support
- Training and consulting services
- Implementation and onboarding support
- Continuous improvement and updates
- Proactive account management

**Business Model Differentiation:**
- Flexible pricing and subscription options
- Value-added services and features
- Partnership and collaboration opportunities
- Revenue sharing models
- Community and ecosystem benefits

#### 12.4.3 Innovation Strategy
**Continuous Innovation:**
- Regular product updates and enhancements
- Customer-driven feature development
- Technology trend monitoring and adoption
- Research and development investment
- Innovation culture and processes

**Disruptive Innovation:**
- New business models and approaches
- Revolutionary technology applications
- Market disruption opportunities
- Industry transformation initiatives
- Breakthrough product features

**Open Innovation:**
- Partner collaboration and co-creation
- Developer ecosystem and community
- Open-source contributions and initiatives
- Customer innovation and feedback
- Industry standards and best practices

### 12.5 Risk Management and Future Planning

#### 12.5.1 Future Risks and Challenges
**Technological Risks:**
- Rapid technology changes and obsolescence
- Cybersecurity threats and vulnerabilities
- Data privacy and compliance challenges
- Integration complexity and compatibility
- Performance and scalability issues

**Market Risks:**
- Increased competition and market saturation
- Changing customer expectations and demands
- Economic downturns and budget constraints
- Regulatory changes and compliance requirements
- Technology adoption barriers

**Operational Risks:**
- System failures and downtime
- Data loss and corruption
- Security breaches and incidents
- Resource constraints and limitations
- Quality and reliability issues

#### 12.5.2 Risk Mitigation Strategies
**Technology Risk Mitigation:**
- Continuous technology monitoring and assessment
- Regular security audits and updates
- Scalable and flexible architecture design
- Comprehensive testing and quality assurance
- Disaster recovery and business continuity planning

**Market Risk Mitigation:**
- Market research and customer feedback
- Competitive analysis and positioning
- Diversification and expansion strategies
- Customer relationship management
- Value proposition enhancement

**Operational Risk Mitigation:**
- Robust infrastructure and systems
- Comprehensive monitoring and alerting
- Redundancy and failover mechanisms
- Skilled and experienced team
- Processes and procedures documentation

#### 12.5.3 Success Metrics and KPIs
**Business Success Metrics:**
- Revenue growth and profitability
- Customer acquisition and retention
- Market share and competitive position
- Customer satisfaction and loyalty
- Brand recognition and reputation

**Technology Success Metrics:**
- System performance and reliability
- Security and compliance status
- Innovation and feature delivery
- Scalability and flexibility
- Technical debt management

**Operational Success Metrics:**
- Operational efficiency and productivity
- Quality and service levels
- Resource utilization and optimization
- Team performance and satisfaction
- Process improvement and optimization

---

## KESIMPULAN

Rancangan lengkap Aplikasi LaundryKu Management System ini menyediakan kerangka kerja komprehensif untuk pengembangan solusi enterprise laundry management yang scalable dan inovatif. Dengan arsitektur microservices yang modern, fitur-fitur lengkap berbasis subscription tier, dan pendekatan user-centric, sistem ini dirancang untuk mentransformasi industri laundry di Indonesia dan Asia Tenggara.

Rancangan ini mencakup semua aspek penting dari perencanaan teknis hingga strategi bisnis, dengan fokus pada kualitas, keamanan, dan kemampuan untuk berkembang sesuai kebutuhan pasar. Dengan implementasi yang tepat dan manajemen yang efektif, LaundryKu berpotensi menjadi pemimpin pasar dalam solusi teknologi untuk industri laundry.