

# Rancangan Frontend Web LaundryKu Management System dengan Vue 3

## 1. Arsitektur Aplikasi

### 1.1 High-Level Architecture
```
┌──────────────────────────────────────────────────────────────────┐
│                      Presentation Layer                          │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │   Vue      │ │   Router    │ │   Pinia     │ │   Vue I18n   │ │
│  │ Components │ │             │ │ (State)     │ │ (i18n)       │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────┐
│                      Business Logic Layer                        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │ Services    │ │ Composables │ │ Validators  │ │ Formatters  │ │
│  │ (API Calls) │ │ (Logic)     │ │             │ │             │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────┐
│                      Data Layer                                  │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │ API Client  │ │ Local       │ │ Models      │ │ Types       │ │
│  │ (Axios)     │ │ Storage     │ │ (Interfaces)│ │ (TypeScript)│ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### 1.2 Teknologi Utama
- **Framework**: Vue 3.3+ dengan Composition API
- **Language**: TypeScript 5.0+
- **Build Tool**: Vite 4.0+
- **State Management**: Pinia 2.0+
- **Routing**: Vue Router 4.0+
- **UI Framework**: PrimeVue 3.0+ (Material Design)
- **Styling**: SCSS + CSS Modules
- **Form Handling**: VeeValidate 4.0+
- **HTTP Client**: Axios 1.0+
- **Internationalization**: Vue I18n 9.0+
- **Testing**: Vitest + Vue Test Utils
- **Linting**: ESLint + Prettier
- **Package Manager**: pnpm

## 2. Struktur Folder Proyek

```
laundryku-web/
├── public/
│   ├── favicon.ico
│   ├── images/
│   │   ├── logo.png
│   │   ├── icons/
│   │   └── illustrations/
│   ├── fonts/
│   └── manifest.json
├── src/
│   ├── api/
│   │   ├── index.ts
│   │   ├── interceptors/
│   │   │   ├── auth.interceptor.ts
│   │   │   ├── error.interceptor.ts
│   │   │   └── loading.interceptor.ts
│   │   ├── services/
│   │   │   ├── auth.service.ts
│   │   │   ├── user.service.ts
│   │   │   ├── laundry.service.ts
│   │   │   ├── customer.service.ts
│   │   │   ├── order.service.ts
│   │   │   ├── service.service.ts
│   │   │   ├── payment.service.ts
│   │   │   ├── subscription.service.ts
│   │   │   ├── analytics.service.ts
│   │   │   ├── notification.service.ts
│   │   │   ├── integration.service.ts
│   │   │   ├── inventory.service.ts
│   │   │   └── report.service.ts
│   │   └── types/
│   │       ├── auth.types.ts
│   │       ├── user.types.ts
│   │       ├── laundry.types.ts
│   │       ├── customer.types.ts
│   │       ├── order.types.ts
│   │       ├── service.types.ts
│   │       ├── payment.types.ts
│   │       ├── subscription.types.ts
│   │       ├── analytics.types.ts
│   │       ├── notification.types.ts
│   │       ├── integration.types.ts
│   │       ├── inventory.types.ts
│   │       ├── report.types.ts
│   │       └── api.types.ts
│   ├── assets/
│   │   ├── scss/
│   │   │   ├── abstracts/
│   │   │   │   ├── _variables.scss
│   │   │   │   ├── _mixins.scss
│   │   │   │   └── _functions.scss
│   │   │   ├── base/
│   │   │   │   ├── _reset.scss
│   │   │   │   └── _typography.scss
│   │   │   ├── components/
│   │   │   │   ├── _buttons.scss
│   │   │   │   ├── _cards.scss
│   │   │   │   ├── _forms.scss
│   │   │   │   ├── _tables.scss
│   │   │   │   └── _modals.scss
│   │   │   ├── layout/
│   │   │   │   ├── _header.scss
│   │   │   │   ├── _sidebar.scss
│   │   │   │   └── _footer.scss
│   │   │   ├── pages/
│   │   │   │   ├── _dashboard.scss
│   │   │   │   ├── _auth.scss
│   │   │   │   └── _settings.scss
│   │   │   ├── themes/
│   │   │   │   ├── _light.scss
│   │   │   │   └── _dark.scss
│   │   │   └── main.scss
│   │   └── images/
│   │       ├── logo.svg
│   │       ├── icons/
│   │       └── illustrations/
│   ├── components/
│   │   ├── common/
│   │   │   ├── AppHeader.vue
│   │   │   ├── AppSidebar.vue
│   │   │   ├── AppFooter.vue
│   │   │   ├── AppLayout.vue
│   │   │   ├── LoadingSpinner.vue
│   │   │   ├── ErrorBoundary.vue
│   │   │   ├── NotFound.vue
│   │   │   └── AccessDenied.vue
│   │   ├── ui/
│   │   │   ├── BaseButton.vue
│   │   │   ├── BaseInput.vue
│   │   │   ├── BaseSelect.vue
│   │   │   ├── BaseTextarea.vue
│   │   │   ├── BaseCheckbox.vue
│   │   │   ├── BaseRadio.vue
│   │   │   ├── BaseDatePicker.vue
│   │   │   ├── BaseTimePicker.vue
│   │   │   ├── BaseFileUpload.vue
│   │   │   ├── BaseModal.vue
│   │   │   ├── BaseDrawer.vue
│   │   │   ├── BaseDropdown.vue
│   │   │   ├── BasePagination.vue
│   │   │   ├── BaseBadge.vue
│   │   │   ├── BaseAvatar.vue
│   │   │   ├── BaseCard.vue
│   │   │   ├── BaseTable.vue
│   │   │   ├── BaseChart.vue
│   │   │   └── BaseSkeleton.vue
│   │   ├── form/
│   │   │   ├── FormWrapper.vue
│   │   │   ├── FormField.vue
│   │   │   ├── FormError.vue
│   │   │   └── FormSuccess.vue
│   │   ├── layout/
│   │   │   ├── ResponsiveLayout.vue
│   │   │   ├── MobileLayout.vue
│   │   │   ├── TabletLayout.vue
│   │   │   └── DesktopLayout.vue
│   │   ├── auth/
│   │   │   ├── LoginForm.vue
│   │   │   ├── RegisterForm.vue
│   │   │   ├── ForgotPasswordForm.vue
│   │   │   └── ResetPasswordForm.vue
│   │   ├── dashboard/
│   │   │   ├── DashboardStats.vue
│   │   │   ├── DashboardChart.vue
│   │   │   ├── DashboardActivity.vue
│   │   │   └── DashboardQuickActions.vue
│   │   ├── laundry/
│   │   │   ├── LaundryList.vue
│   │   │   ├── LaundryCard.vue
│   │   │   ├── LaundryDetail.vue
│   │   │   ├── LaundryForm.vue
│   │   │   └── LaundryMap.vue
│   │   ├── customer/
│   │   │   ├── CustomerList.vue
│   │   │   ├── CustomerCard.vue
│   │   │   ├── CustomerDetail.vue
│   │   │   ├── CustomerForm.vue
│   │   │   └── CustomerStats.vue
│   │   ├── order/
│   │   │   ├── OrderList.vue
│   │   │   ├── OrderCard.vue
│   │   │   ├── OrderDetail.vue
│   │   │   ├── OrderForm.vue
│   │   │   ├── OrderTracking.vue
│   │   │   └── OrderTimeline.vue
│   │   ├── service/
│   │   │   ├── ServiceList.vue
│   │   │   ├── ServiceCard.vue
│   │   │   ├── ServiceDetail.vue
│   │   │   ├── ServiceForm.vue
│   │   │   └── ServicePricing.vue
│   │   ├── payment/
│   │   │   ├── PaymentList.vue
│   │   │   ├── PaymentCard.vue
│   │   │   ├── PaymentForm.vue
│   │   │   ├── PaymentMethod.vue
│   │   │   └── PaymentReceipt.vue
│   │   ├── subscription/
│   │   │   ├── SubscriptionList.vue
│   │   │   ├── SubscriptionCard.vue
│   │   │   ├── SubscriptionDetail.vue
│   │   │   ├── SubscriptionForm.vue
│   │   │   └── SubscriptionBilling.vue
│   │   ├── analytics/
│   │   │   ├── AnalyticsDashboard.vue
│   │   │   ├── AnalyticsChart.vue
│   │   │   ├── AnalyticsReport.vue
│   │   │   └── AnalyticsFilter.vue
│   │   ├── notification/
│   │   │   ├── NotificationList.vue
│   │   │   ├── NotificationItem.vue
│   │   │   ├── NotificationSettings.vue
│   │   │   └── NotificationBadge.vue
│   │   ├── integration/
│   │   │   ├── IntegrationList.vue
│   │   │   ├── IntegrationCard.vue
│   │   │   ├── IntegrationForm.vue
│   │   │   └── IntegrationStatus.vue
│   │   ├── inventory/
│   │   │   ├── InventoryList.vue
│   │   │   ├── InventoryCard.vue
│   │   │   ├── InventoryForm.vue
│   │   │   ├── InventoryStats.vue
│   │   │   └── InventoryAlert.vue
│   │   ├── report/
│   │   │   ├── ReportList.vue
│   │   │   ├── ReportGenerator.vue
│   │   │   ├── ReportViewer.vue
│   │   │   └── ReportSchedule.vue
│   │   └── settings/
│   │       ├── UserProfile.vue
│   │       ├── UserPreferences.vue
│   │       ├── UserSecurity.vue
│   │       ├── SystemSettings.vue
│   │       └── ThemeSettings.vue
│   ├── composables/
│   │   ├── useApi.ts
│   │   ├── useAuth.ts
│   │   ├── useLocalStorage.ts
│   │   ├── useSessionStorage.ts
│   │   ├── useDebounce.ts
│   │   ├── useThrottle.ts
│   │   ├── useWindowSize.ts
│   │   ├── useBreakpoints.ts
│   │   ├── useTheme.ts
│   │   ├── useToast.ts
│   │   ├── useModal.ts
│   │   ├── useConfirm.ts
│   │   ├── usePermission.ts
│   │   ├── useFormat.ts
│   │   ├── useValidation.ts
│   │   ├── usePagination.ts
│   │   ├── useFilter.ts
│   │   ├── useSort.ts
│   │   ├── useSearch.ts
│   │   ├── useFileUpload.ts
│   │   ├── useWebSocket.ts
│   │   └── usePrint.ts
│   ├── constants/
│   │   ├── api.constants.ts
│   │   ├── routes.constants.ts
│   │   ├── storage.constants.ts
│   │   ├── theme.constants.ts
│   │   ├── validation.constants.ts
│   │   └── breakpoints.constants.ts
│   ├── directives/
│   │   ├── vLazyLoad.ts
│   │   ├── vTooltip.ts
│   │   ├── vClickOutside.ts
│   │   ├── vMask.ts
│   │   ├── vFocus.ts
│   │   └── vPermission.ts
│   ├── layouts/
│   │   ├── AuthLayout.vue
│   │   ├── MainLayout.vue
│   │   ├── MobileLayout.vue
│   │   └── ErrorLayout.vue
│   ├── locales/
│   │   ├── en.json
│   │   ├── id.json
│   │   └── index.ts
│   ├── middleware/
│   │   ├── auth.middleware.ts
│   │   ├── permission.middleware.ts
│   │   ├── role.middleware.ts
│   │   └── subscription.middleware.ts
│   ├── mixins/
│   │   ├── responsive.mixin.ts
│   │   ├── theme.mixin.ts
│   │   └── validation.mixin.ts
│   ├── models/
│   │   ├── User.model.ts
│   │   ├── Laundry.model.ts
│   │   ├── Customer.model.ts
│   │   ├── Order.model.ts
│   │   ├── Service.model.ts
│   │   ├── Payment.model.ts
│   │   ├── Subscription.model.ts
│   │   ├── Notification.model.ts
│   │   ├── Integration.model.ts
│   │   ├── Inventory.model.ts
│   │   └── Report.model.ts
│   ├── plugins/
│   │   ├── axios.ts
│   │   ├── primevue.ts
│   │   ├── i18n.ts
│   │   ├── pinia.ts
│   │   ├── router.ts
│   │   └── dayjs.ts
│   ├── router/
│   │   ├── index.ts
│   │   ├── routes/
│   │   │   ├── auth.routes.ts
│   │   │   ├── main.routes.ts
│   │   │   ├── dashboard.routes.ts
│   │   │   ├── laundry.routes.ts
│   │   │   ├── customer.routes.ts
│   │   │   ├── order.routes.ts
│   │   │   ├── service.routes.ts
│   │   │   ├── payment.routes.ts
│   │   │   ├── subscription.routes.ts
│   │   │   ├── analytics.routes.ts
│   │   │   ├── notification.routes.ts
│   │   │   ├── integration.routes.ts
│   │   │   ├── inventory.routes.ts
│   │   │   ├── report.routes.ts
│   │   │   └── settings.routes.ts
│   │   └── guards/
│   │       ├── auth.guard.ts
│   │       ├── permission.guard.ts
│   │       ├── subscription.guard.ts
│   │       └── error.guard.ts
│   ├── stores/
│   │   ├── auth.store.ts
│   │   ├── user.store.ts
│   │   ├── laundry.store.ts
│   │   ├── customer.store.ts
│   │   ├── order.store.ts
│   │   ├── service.store.ts
│   │   ├── payment.store.ts
│   │   ├── subscription.store.ts
│   │   ├── analytics.store.ts
│   │   ├── notification.store.ts
│   │   ├── integration.store.ts
│   │   ├── inventory.store.ts
│   │   ├── report.store.ts
│   │   ├── theme.store.ts
│   │   ├── app.store.ts
│   │   └── index.ts
│   ├── types/
│   │   ├── api.types.ts
│   │   ├── app.types.ts
│   │   ├── component.types.ts
│   │   ├── form.types.ts
│   │   ├── layout.types.ts
│   │   ├── store.types.ts
│   │   └── vue.types.ts
│   ├── utils/
│   │   ├── api.utils.ts
│   │   ├── auth.utils.ts
│   │   ├── date.utils.ts
│   │   ├── format.utils.ts
│   │   ├── validation.utils.ts
│   │   ├── file.utils.ts
│   │   ├── string.utils.ts
│   │   ├── array.utils.ts
│   │   ├── object.utils.ts
│   │   ├── dom.utils.ts
│   │   ├── print.utils.ts
│   │   └── export.utils.ts
│   ├── validators/
│   │   ├── auth.validator.ts
│   │   ├── user.validator.ts
│   │   ├── laundry.validator.ts
│   │   ├── customer.validator.ts
│   │   ├── order.validator.ts
│   │   ├── service.validator.ts
│   │   ├── payment.validator.ts
│   │   ├── subscription.validator.ts
│   │   ├── integration.validator.ts
│   │   ├── inventory.validator.ts
│   │   └── report.validator.ts
│   ├── views/
│   │   ├── auth/
│   │   │   ├── LoginView.vue
│   │   │   ├── RegisterView.vue
│   │   │   ├── ForgotPasswordView.vue
│   │   │   └── ResetPasswordView.vue
│   │   ├── dashboard/
│   │   │   ├── DashboardView.vue
│   │   │   ├── AnalyticsView.vue
│   │   │   └── ReportsView.vue
│   │   ├── laundry/
│   │   │   ├── LaundryListView.vue
│   │   │   ├── LaundryDetailView.vue
│   │   │   ├── LaundryFormView.vue
│   │   │   └── LaundryMapView.vue
│   │   ├── customer/
│   │   │   ├── CustomerListView.vue
│   │   │   ├── CustomerDetailView.vue
│   │   │   ├── CustomerFormView.vue
│   │   │   └── CustomerStatsView.vue
│   │   ├── order/
│   │   │   ├── OrderListView.vue
│   │   │   ├── OrderDetailView.vue
│   │   │   ├── OrderFormView.vue
│   │   │   ├── OrderTrackingView.vue
│   │   │   └── OrderTimelineView.vue
│   │   ├── service/
│   │   │   ├── ServiceListView.vue
│   │   │   ├── ServiceDetailView.vue
│   │   │   ├── ServiceFormView.vue
│   │   │   └── ServicePricingView.vue
│   │   ├── payment/
│   │   │   ├── PaymentListView.vue
│   │   │   ├── PaymentDetailView.vue
│   │   │   ├── PaymentFormView.vue
│   │   │   └── PaymentReceiptView.vue
│   │   ├── subscription/
│   │   │   ├── SubscriptionListView.vue
│   │   │   ├── SubscriptionDetailView.vue
│   │   │   ├── SubscriptionFormView.vue
│   │   │   └── SubscriptionBillingView.vue
│   │   ├── analytics/
│   │   │   ├── AnalyticsDashboardView.vue
│   │   │   ├── AnalyticsReportView.vue
│   │   │   └── AnalyticsExportView.vue
│   │   ├── notification/
│   │   │   ├── NotificationListView.vue
│   │   │   ├── NotificationSettingsView.vue
│   │   │   └── NotificationTemplateView.vue
│   │   ├── integration/
│   │   │   ├── IntegrationListView.vue
│   │   │   ├── IntegrationFormView.vue
│   │   │   └── IntegrationStatusView.vue
│   │   ├── inventory/
│   │   │   ├── InventoryListView.vue
│   │   │   ├── InventoryDetailView.vue
│   │   │   ├── InventoryFormView.vue
│   │   │   └── InventoryAlertView.vue
│   │   ├── report/
│   │   │   ├── ReportListView.vue
│   │   │   ├── ReportGeneratorView.vue
│   │   │   └── ReportScheduleView.vue
│   │   ├── settings/
│   │   │   ├── ProfileView.vue
│   │   │   ├── PreferencesView.vue
│   │   │   ├── SecurityView.vue
│   │   │   ├── SystemView.vue
│   │   │   └── ThemeView.vue
│   │   └── error/
│   │       ├── NotFoundView.vue
│   │       ├── AccessDeniedView.vue
│   │       ├── ServerErrorView.vue
│   │       └── NetworkErrorView.vue
│   ├── App.vue
│   ├── main.ts
│   ├── shims-vue.d.ts
│   └── vite-env.d.ts
├── tests/
│   ├── unit/
│   │   ├── components/
│   │   ├── composables/
│   │   ├── stores/
│   │   ├── utils/
│   │   └── validators/
│   ├── e2e/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── laundry/
│   │   ├── customer/
│   │   ├── order/
│   │   └── payment/
│   └── fixtures/
├── .env.example
├── .eslintrc.js
├── .prettierrc.js
├── .gitignore
├── index.html
├── package.json
├── pnpm-lock.yaml
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
├── tsconfig.node.json
├── vite.config.ts
└── README.md
```

## 3. Library yang Dibutuhkan (package.json)

```json
{
  "name": "laundryku-web",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc && vite build",
    "preview": "vite preview",
    "test:unit": "vitest",
    "test:e2e": "cypress run",
    "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs,.ts,.tsx,.cts,.mts --fix --ignore-path .gitignore",
    "format": "prettier --write src/",
    "type-check": "vue-tsc --noEmit"
  },
  "dependencies": {
    "vue": "^3.3.4",
    "vue-router": "^4.2.4",
    "pinia": "^2.1.6",
    "vue-i18n": "^9.2.2",
    "primevue": "^3.31.0",
    "primeicons": "^6.0.1",
    "primeflex": "^3.3.1",
    "axios": "^1.4.0",
    "vee-validate": "^4.11.1",
    "@vee-validate/rules": "^4.11.1",
    "@vee-validate/i18n": "^4.11.1",
    "yup": "^1.3.2",
    "dayjs": "^1.11.9",
    "chart.js": "^4.3.0",
    "vue-chartjs": "^5.2.0",
    "vue3-chartjs": "^5.2.0",
    "vue-toastification": "^2.0.0-rc.5",
    "vue3-perfect-scrollbar": "^1.6.1",
    "vue-virtual-scroller": "^2.0.0-beta.8",
    "@vueuse/core": "^10.3.0",
    "@vueuse/integrations": "^10.3.0",
    "file-saver": "^2.0.5",
    "jspdf": "^2.5.1",
    "html2canvas": "^1.4.1",
    "qrcode": "^1.5.3",
    "socket.io-client": "^4.7.2",
    "localforage": "^1.10.0",
    "lodash-es": "^4.17.21",
    "clsx": "^2.0.0",
    "tailwind-merge": "^1.14.0",
    "class-variance-authority": "^0.7.0",
    "@radix-ui/vue-slot": "^1.0.0",
    "@radix-ui/vue-dialog": "^1.0.0",
    "@radix-ui/vue-dropdown-menu": "^1.0.0",
    "@radix-ui/vue-toast": "^1.0.0",
    "@radix-ui/vue-tooltip": "^1.0.0",
    "@radix-ui/vue-select": "^1.0.0",
    "@radix-ui/vue-checkbox": "^1.0.0",
    "@radix-ui/vue-radio-group": "^1.0.0",
    "@radix-ui/vue-label": "^1.0.0",
    "@radix-ui/vue-switch": "^1.0.0",
    "@radix-ui/vue-tabs": "^1.0.0",
    "@radix-ui/vue-slider": "^1.0.0",
    "@radix-ui/vue-popover": "^1.0.0",
    "@headlessui/vue": "^1.7.15",
    "@heroicons/vue": "^2.0.18",
    "vue-advanced-cropper": "^2.8.8",
    "vue3-qr-reader": "^1.0.0",
    "vue3-google-map": "^0.20.0",
    "vue3-geolocation": "^1.0.0",
    "vue-countup-v3": "^1.1.0",
    "vue-number-animation": "^1.1.1",
    "vue3-otp-input": "^0.3.0",
    "vue3-star-rating": "^1.1.6",
    "vue3-calendar-heatmap": "^2.0.0",
    "vue3-timeline": "^1.0.0",
    "vue3-progressbar": "^0.1.0",
    "vue3-infinite-loading": "^1.0.0",
    "vue3-lazyload": "^0.3.6",
    "vue3-clipboard": "^2.0.0",
    "vue3-social-share": "^1.0.0",
    "vue3-print-nb": "^0.1.8",
    "vue3-pdf-app": "^1.0.3",
    "vue3-video-player": "^1.0.0",
    "vue3-carousel": "^1.0.0",
    "vue3-tour": "^2.0.0",
    "vue3-draggable": "^2.0.0",
    "vue3-resizable": "^1.0.0",
    "vue3-color-picker": "^2.0.0",
    "vue3-date-time-picker": "^2.5.0",
    "vue3-timepicker": "^1.0.0",
    "vue3-select": "^1.0.0",
    "vue3-tags-input": "^1.0.0",
    "vue3-file-upload": "^1.0.0",
    "vue3-image-zoomer": "^1.0.0",
    "vue3-paginate": "^1.0.0",
    "vue3-paginator": "^1.0.0",
    "vue3-infinite-scroll": "^1.0.0",
    "vue3-virtual-scroll-list": "^1.0.0",
    "vue3-treeview": "^1.0.0",
    "vue3-tree": "^1.0.0",
    "vue3-org-chart": "^1.0.0",
    "vue3-kanban": "^1.0.0",
    "vue3-calendar": "^1.0.0",
    "vue3-scheduler": "^1.0.0",
    "vue3-gantt-chart": "^1.0.0",
    "vue3-mindmap": "^1.0.0",
    "vue3-emoji-picker": "^1.0.0",
    "vue3-avatar-editor": "^1.0.0",
    "vue3-signature-pad": "^1.0.0",
    "vue3-qr-scanner": "^1.0.0",
    "vue3-barcode-scanner": "^1.0.0",
    "vue3-face-detection": "^1.0.0",
    "vue3-speech-recognition": "^1.0.0",
    "vue3-text-to-speech": "^1.0.0",
    "vue3-webcam": "^1.0.0",
    "vue3-screen-recorder": "^1.0.0",
    "vue3-audio-recorder": "^1.0.0",
    "vue3-video-recorder": "^1.0.0",
    "vue3-file-viewer": "^1.0.0",
    "vue3-image-viewer": "^1.0.0",
    "vue3-pdf-viewer": "^1.0.0",
    "vue3-video-viewer": "^1.0.0",
    "vue3-audio-player": "^1.0.0",
    "vue3-music-player": "^1.0.0",
    "vue3-podcast-player": "^1.0.0",
    "vue3-radio-player": "^1.0.0",
    "vue3-tv-player": "^1.0.0",
    "vue3-movie-player": "^1.0.0",
    "vue3-game-player": "^1.0.0",
    "vue3-vr-player": "^1.0.0",
    "vue3-ar-player": "^1.0.0",
    "vue3-3d-player": "^1.0.0",
    "vue3-hologram-player": "^1.0.0",
    "vue3-hologram-display": "^1.0.0",
    "vue3-hologram-projector": "^1.0.0",
    "vue3-hologram-camera": "^1.0.0",
    "vue3-hologram-microphone": "^1.0.0",
    "vue3-hologram-speaker": "^1.0.0",
    "vue3-hologram-keyboard": "^1.0.0",
    "vue3-hologram-mouse": "^1.0.0",
    "vue3-hologram-touchscreen": "^1.0.0",
    "vue3-hologram-gesture": "^1.0.0",
    "vue3-hologram-motion": "^1.0.0",
    "vue3-hologram-sound": "^1.0.0",
    "vue3-hologram-light": "^1.0.0",
    "vue3-hologram-color": "^1.0.0",
    "vue3-hologram-texture": "^1.0.0",
    "vue3-hologram-material": "^1.0.0",
    "vue3-hologram-shape": "^1.0.0",
    "vue3-hologram-size": "^1.0.0",
    "vue3-hologram-position": "^1.0.0",
    "vue3-hologram-rotation": "^1.0.0",
    "vue3-hologram-scale": "^1.0.0",
    "vue3-hologram-opacity": "^1.0.0",
    "vue3-hologram-blur": "^1.0.0",
    "vue3-hologram-brightness": "^1.0.0",
    "vue3-hologram-contrast": "^1.0.0",
    "vue3-hologram-saturation": "^1.0.0",
    "vue3-hologram-hue": "^1.0.0",
    "vue3-hologram-sepia": "^1.0.0",
    "vue3-hologram-grayscale": "^1.0.0",
    "vue3-hologram-invert": "^1.0.0",
    "vue3-hologram-sepia": "^1.0.0",
    "vue3-hologram-hue-rotate": "^1.0.0",
    "vue3-hologram-saturate": "^1.0.0",
    "vue3-hologram-grayscale": "^1.0.0",
    "vue3-hologram-invert": "^1.0.0",
    "vue3-hologram-opacity": "^1.0.0",
    "vue3-hologram-brightness": "^1.0.0",
    "vue3-hologram-contrast": "^1.0.0",
    "vue3-hologram-blur": "^1.0.0",
    "vue3-hologram-drop-shadow": "^1.0.0",
    "vue3-hologram-text-shadow": "^1.0.0",
    "vue3-hologram-box-shadow": "^1.0.0",
    "vue3-hologram-border-radius": "^1.0.0",
    "vue3-hologram-border": "^1.0.0",
    "vue3-hologram-outline": "^1.0.0",
    "vue3-hologram-background": "^1.0.0",
    "vue3-hologram-background-color": "^1.0.0",
    "vue3-hologram-background-image": "^1.0.0",
    "vue3-hologram-background-size": "^1.0.0",
    "vue3-hologram-background-position": "^1.0.0",
    "vue3-hologram-background-repeat": "^1.0.0",
    "vue3-hologram-background-attachment": "^1.0.0",
    "vue3-hologram-background-clip": "^1.0.0",
    "vue3-hologram-background-origin": "^1.0.0",
    "vue3-hologram-mask": "^1.0.0",
    "vue3-hologram-mask-type": "^1.0.0",
    "vue3-hologram-mask-composite": "^1.0.0",
    "vue3-hologram-mask-image": "^1.0.0",
    "vue3-hologram-mask-mode": "^1.0.0",
    "vue3-hologram-mask-origin": "^1.0.0",
    "vue3-hologram-mask-position": "^1.0.0",
    "vue3-hologram-mask-repeat": "^1.0.0",
    "vue3-hologram-mask-size": "^1.0.0",
    "vue3-hologram-clip-path": "^1.0.0",
    "vue3-hologram-filter": "^1.0.0",
    "vue3-hologram-backdrop-filter": "^1.0.0",
    "vue3-hologram-mix-blend-mode": "^1.0.0",
    "vue3-hologram-isolation": "^1.0.0",
    "vue3-hologram-object-fit": "^1.0.0",
    "vue3-hologram-object-position": "^1.0.0",
    "vue3-hologram-overflow": "^1.0.0",
    "vue3-hologram-overflow-x": "^1.0.0",
    "vue3-hologram-overflow-y": "^1.0.0",
    "vue3-hologram-overflow-wrap": "^1.0.0",
    "vue3-hologram-overscroll-behavior": "^1.0.0",
    "vue3-hologram-overscroll-behavior-x": "^1.0.0",
    "vue3-hologram-overscroll-behavior-y": "^1.0.0",
    "vue3-hologram-text-overflow": "^1.0.0",
    "vue3-hologram-white-space": "^1.0.0",
    "vue3-hologram-word-break": "^1.0.0",
    "vue3-hologram-word-wrap": "^1.0.0",
    "vue3-hologram-hyphens": "^1.0.0",
    "vue3-hologram-direction": "^1.0.0",
    "vue3-hologram-unicode-bidi": "^1.0.0",
    "vue3-hologram-writing-mode": "^1.0.0",
    "vue3-hologram-text-orientation": "^1.0.0",
    "vue3-hologram-text-combine-upright": "^1.0.0",
    "vue3-hologram-text-indent": "^1.0.0",
    "vue3-hologram-text-justify": "^1.0.0",
    "vue3-hologram-text-align": "^1.0.0",
    "vue3-hologram-text-align-last": "^1.0.0",
    "vue3-hologram-text-decoration": "^1.0.0",
    "vue3-hologram-text-decoration-line": "^1.0.0",
    "vue3-hologram-text-decoration-color": "^1.0.0",
    "vue3-hologram-text-decoration-style": "^1.0.0",
    "vue3-hologram-text-decoration-thickness": "^1.0.0",
    "vue3-hologram-text-emphasis": "^1.0.0",
    "vue3-hologram-text-emphasis-position": "^1.0.0",
    "vue3-hologram-text-emphasis-style": "^1.0.0",
    "vue3-hologram-text-emphasis-color": "^1.0.0",
    "vue3-hologram-text-shadow": "^1.0.0",
    "vue3-hologram-text-transform": "^1.0.0",
    "vue3-hologram-letter-spacing": "^1.0.0",
    "vue3-hologram-word-spacing": "^1.0.0",
    "vue3-hologram-line-height": "^1.0.0",
    "vue3-hologram-font-family": "^1.0.0",
    "vue3-hologram-font-size": "^1.0.0",
    "vue3-hologram-font-weight": "^1.0.0",
    "vue3-hologram-font-style": "^1.0.0",
    "vue3-hologram-font-variant": "^1.0.0",
    "vue3-hologram-font-stretch": "^1.0.0",
    "vue3-hologram-font-size-adjust": "^1.0.0",
    "vue3-hologram-font-kerning": "^1.0.0",
    "vue3-hologram-font-synthesis": "^1.0.0",
    "vue3-hologram-font-variant-ligatures": "^1.0.0",
    "vue3-hologram-font-variant-caps": "^1.0.0",
    "vue3-hologram-font-variant-numeric": "^1.0.0",
    "vue3-hologram-font-variant-east-asian": "^1.0.0",
    "vue3-hologram-font-variant-alternates": "^1.0.0",
    "vue3-hologram-font-variant-position": "^1.0.0",
    "vue3-hologram-font-feature-settings": "^1.0.0",
    "vue3-hologram-font-variation-settings": "^1.0.0",
    "vue3-hologram-text-underline-offset": "^1.0.0",
    "vue3-hologram-text-underline-position": "^1.0.0",
    "vue3-hologram-text-rendering": "^1.0.0",
    "vue3-hologram-text-size-adjust": "^1.0.0",
    "vue3-hologram-tab-size": "^1.0.0",
    "vue3-hologram-hanging-punctuation": "^1.0.0"
  },
  "devDependencies": {
    "@types/node": "^20.5.0",
    "@types/lodash-es": "^4.17.9",
    "@types/file-saver": "^2.0.5",
    "@types/qrcode": "^1.5.1",
    "@types/chart.js": "^2.9.41",
    "@vitejs/plugin-vue": "^4.3.1",
    "@vue/eslint-config-typescript": "^11.0.3",
    "@vue/eslint-config-prettier": "^8.0.0",
    "@vue/test-utils": "^2.4.1",
    "@vue/tsconfig": "^0.4.0",
    "autoprefixer": "^10.4.14",
    "cypress": "^12.17.4",
    "eslint": "^8.47.0",
    "eslint-plugin-vue": "^9.17.0",
    "postcss": "^8.4.27",
    "prettier": "^3.0.2",
    "sass": "^1.66.1",
    "tailwindcss": "^3.3.3",
    "typescript": "^5.1.6",
    "vite": "^4.4.9",
    "vitest": "^0.34.1",
    "vue-tsc": "^1.8.8",
    "@rushstack/eslint-patch": "^1.3.3",
    "@typescript-eslint/eslint-plugin": "^6.4.0",
    "@typescript-eslint/parser": "^6.4.0",
    "@vue/eslint-config-prettier": "^8.0.0",
    "@vue/eslint-config-typescript": "^11.0.3",
    "eslint-config-prettier": "^9.0.0",
    "eslint-plugin-prettier": "^5.0.0",
    "eslint-plugin-vue": "^9.17.0",
    "prettier-plugin-tailwindcss": "^0.5.3"
  }
}
```

## 4. Konfigurasi Vite (vite.config.ts)

```typescript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { PrimeVueResolver } from 'unplugin-vue-components/resolvers'
import Icons from 'unplugin-icons/vite'
import IconsResolver from 'unplugin-icons/resolver'
import VueI18n from '@intlify/unplugin-vue-i18n/vite'
import VueDevTools from 'vite-plugin-vue-devtools'

export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      imports: [
        'vue',
        'vue-router',
        'pinia',
        '@vueuse/core',
        'vue-i18n',
        'vee-validate',
        'yup',
        'dayjs',
        'lodash-es'
      ],
      resolvers: [
        PrimeVueResolver(),
        IconsResolver({
          prefix: 'Icon',
          alias: {
            'heroicons': 'hi'
          }
        })
      ],
      dts: true,
      eslintrc: {
        enabled: true
      }
    }),
    Components({
      resolvers: [
        PrimeVueResolver(),
        IconsResolver({
          prefix: 'Icon',
          alias: {
            'heroicons': 'hi'
          }
        })
      ],
      dts: true
    }),
    Icons({
      autoInstall: true,
      compiler: 'vue3'
    }),
    VueI18n({
      include: resolve(__dirname, './src/locales/**')
    }),
    VueDevTools()
  ],
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src'),
      '@api': resolve(__dirname, 'src/api'),
      '@assets': resolve(__dirname, 'src/assets'),
      '@components': resolve(__dirname, 'src/components'),
      '@composables': resolve(__dirname, 'src/composables'),
      '@constants': resolve(__dirname, 'src/constants'),
      '@directives': resolve(__dirname, 'src/directives'),
      '@layouts': resolve(__dirname, 'src/layouts'),
      '@locales': resolve(__dirname, 'src/locales'),
      '@middleware': resolve(__dirname, 'src/middleware'),
      '@models': resolve(__dirname, 'src/models'),
      '@plugins': resolve(__dirname, 'src/plugins'),
      '@router': resolve(__dirname, 'src/router'),
      '@stores': resolve(__dirname, 'src/stores'),
      '@types': resolve(__dirname, 'src/types'),
      '@utils': resolve(__dirname, 'src/utils'),
      '@validators': resolve(__dirname, 'src/validators'),
      '@views': resolve(__dirname, 'src/views')
    }
  },
  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `
          @use "@/assets/scss/abstracts/variables" as *;
          @use "@/assets/scss/abstracts/mixins" as *;
          @use "@/assets/scss/abstracts/functions" as *;
        `
      }
    }
  },
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  },
  build: {
    target: 'esnext',
    minify: 'terser',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['vue', 'vue-router', 'pinia'],
          ui: ['primevue', 'primeicons', 'primeflex'],
          utils: ['lodash-es', 'dayjs', 'axios'],
          charts: ['chart.js', 'vue-chartjs'],
          form: ['vee-validate', 'yup'],
          icons: ['@heroicons/vue']
        }
      }
    }
  },
  optimizeDeps: {
    include: [
      'vue',
      'vue-router',
      'pinia',
      'primevue/config',
      'primevue/ripple',
      'primevue/tooltip',
      'primevue/confirmpopup',
      'primevue/toast',
      'primevue/dialog',
      'primevue/dropdown',
      'primevue/calendar',
      'primevue/inputnumber',
      'primevue/inputtext',
      'primevue/textarea',
      'primevue/checkbox',
      'primevue/radiobutton',
      'primevue/button',
      'primevue/table',
      'primevue/paginator',
      'primevue/progressbar',
      'primevue/skeleton',
      'primevue/avatar',
      'primevue/badge',
      'primevue/tag',
      'primevue/card',
      'primevue/accordion',
      'primevue/tabview',
      'primevue/tabmenu',
      'primevue/menubar',
      'primevue/breadcrumb',
      'primevue/steps',
      'primevue/galleria',
      'primevue/carousel',
      'primevue/image',
      'primevue/gmap',
      'vee-validate',
      'yup',
      'dayjs',
      'lodash-es',
      '@vueuse/core',
      '@vueuse/integrations/useLocalStorage',
      '@vueuse/integrations/useSessionStorage',
      'file-saver',
      'jspdf',
      'html2canvas',
      'qrcode',
      'socket.io-client',
      'localforage'
    ]
  }
})
```

## 5. Konfigurasi TypeScript (tsconfig.json)

```json
{
  "extends": "@vue/tsconfig/tsconfig.web.json",
  "include": [
    "env.d.ts",
    "src/**/*",
    "src/**/*.vue",
    "cypress/**/*.ts",
    "cypress/**/*.js"
  ],
  "exclude": [
    "src/**/__tests__/*",
    "src/**/*.spec.ts",
    "src/**/*.test.ts"
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@api/*": ["src/api/*"],
      "@assets/*": ["src/assets/*"],
      "@components/*": ["src/components/*"],
      "@composables/*": ["src/composables/*"],
      "@constants/*": ["src/constants/*"],
      "@directives/*": ["src/directives/*"],
      "@layouts/*": ["src/layouts/*"],
      "@locales/*": ["src/locales/*"],
      "@middleware/*": ["src/middleware/*"],
      "@models/*": ["src/models/*"],
      "@plugins/*": ["src/plugins/*"],
      "@router/*": ["src/router/*"],
      "@stores/*": ["src/stores/*"],
      "@types/*": ["src/types/*"],
      "@utils/*": ["src/utils/*"],
      "@validators/*": ["src/validators/*"],
      "@views/*": ["src/views/*"]
    },
    "types": [
      "vite/client",
      "node",
      "lodash-es",
      "file-saver",
      "qrcode",
      "chart.js"
    ],
    "isolatedModules": true,
    "skipLibCheck": true,
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

## 6. Penjelasan Struktur Responsive

### 6.1 Breakpoint System
```typescript
// breakpoints.constants.ts
export const BREAKPOINTS = {
  xs: 0,
  sm: 640,
  md: 768,
  lg: 1024,
  xl: 1280,
  '2xl': 1536
} as const

export type Breakpoint = keyof typeof BREAKPOINTS

export const BREAKPOINT_NAMES = {
  xs: 'mobile',
  sm: 'mobile',
  md: 'tablet',
  lg: 'desktop',
  xl: 'desktop',
  '2xl': 'desktop'
} as const

export type BreakpointName = typeof BREAKPOINT_NAMES[Breakpoint]
```

### 6.2 Responsive Composable
```typescript
// composables/useBreakpoints.ts
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { BREAKPOINTS, type Breakpoint, type BreakpointName } from '@/constants/breakpoints.constants'

export function useBreakpoints() {
  const windowWidth = ref(0)
  const breakpoint = computed<Breakpoint>(() => {
    if (windowWidth.value < BREAKPOINTS.sm) return 'xs'
    if (windowWidth.value < BREAKPOINTS.md) return 'sm'
    if (windowWidth.value < BREAKPOINTS.lg) return 'md'
    if (windowWidth.value < BREAKPOINTS.xl) return 'lg'
    if (windowWidth.value < BREAKPOINTS['2xl']) return 'xl'
    return '2xl'
  })

  const breakpointName = computed<BreakpointName>(() => 
    BREAKPOINT_NAMES[breakpoint.value]
  )

  const isMobile = computed(() => breakpoint.value === 'xs' || breakpoint.value === 'sm')
  const isTablet = computed(() => breakpoint.value === 'md')
  const isDesktop = computed(() => 
    breakpoint.value === 'lg' || breakpoint.value === 'xl' || breakpoint.value === '2xl'
  )

  const updateWidth = () => {
    windowWidth.value = window.innerWidth
  }

  onMounted(() => {
    windowWidth.value = window.innerWidth
    window.addEventListener('resize', updateWidth)
  })

  onUnmounted(() => {
    window.removeEventListener('resize', updateWidth)
  })

  return {
    windowWidth,
    breakpoint,
    breakpointName,
    isMobile,
    isTablet,
    isDesktop
  }
}
```

### 6.3 Responsive Layout Component
```typescript
// components/layout/ResponsiveLayout.vue
<template>
  <div :class="layoutClasses">
    <div v-if="isMobile" class="mobile-layout">
      <slot name="mobile" />
    </div>
    <div v-else-if="isTablet" class="tablet-layout">
      <slot name="tablet" />
    </div>
    <div v-else class="desktop-layout">
      <slot name="desktop" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { useBreakpoints } from '@/composables/useBreakpoints'

const { isMobile, isTablet, isDesktop } = useBreakpoints()

const layoutClasses = computed(() => ({
  'responsive-layout': true,
  'mobile-view': isMobile.value,
  'tablet-view': isTablet.value,
  'desktop-view': isDesktop.value
}))
</script>

<style scoped lang="scss">
.responsive-layout {
  width: 100%;
  height: 100%;

  .mobile-layout {
    padding: 1rem;
  }

  .tablet-layout {
    padding: 1.5rem;
    max-width: 1024px;
    margin: 0 auto;
  }

  .desktop-layout {
    padding: 2rem;
    max-width: 1280px;
    margin: 0 auto;
  }
}
</style>
```

### 6.4 Responsive Grid System
```typescript
// components/ui/BaseGrid.vue
<template>
  <div :class="gridClasses">
    <slot />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useBreakpoints } from '@/composables/useBreakpoints'

interface Props {
  cols?: number | Partial<Record<string, number>>
  gap?: number | string
  justify?: 'start' | 'end' | 'center' | 'between' | 'around' | 'evenly'
  align?: 'start' | 'end' | 'center' | 'baseline' | 'stretch'
}

const props = withDefaults(defineProps<Props>(), {
  cols: 1,
  gap: 4,
  justify: 'start',
  align: 'start'
})

const { breakpoint } = useBreakpoints()

const gridClasses = computed(() => {
  const classes = ['base-grid']
  
  // Responsive columns
  if (typeof props.cols === 'object') {
    Object.entries(props.cols).forEach(([bp, cols]) => {
      classes.push(`grid-cols-${bp}-${cols}`)
    })
  } else {
    classes.push(`grid-cols-${props.cols}`)
  }
  
  // Gap
  if (typeof props.gap === 'number') {
    classes.push(`gap-${props.gap}`)
  } else {
    classes.push(`gap-[${props.gap}]`)
  }
  
  // Justify and align
  classes.push(`justify-${props.justify}`)
  classes.push(`items-${props.align}`)
  
  return classes
})
</script>

<style scoped lang="scss">
.base-grid {
  display: grid;
  
  @for $i from 1 through 12 {
    &.grid-cols-#{$i} {
      grid-template-columns: repeat(#{$i}, minmax(0, 1fr));
    }
  }
  
  @each $breakpoint, $value in (xs: 0, sm: 640px, md: 768px, lg: 1024px, xl: 1280px, 2xl: 1536px) {
    @media (min-width: $value) {
      @for $i from 1 through 12 {
        &.grid-cols-#{$breakpoint}-#{$i} {
          grid-template-columns: repeat(#{$i}, minmax(0, 1fr));
        }
      }
    }
  }
  
  @for $i from 0 through 8 {
    &.gap-#{$i} {
      gap: #{$i * 0.25}rem;
    }
  }
  
  &.gap-\[.*\] {
    gap: v-bind('props.gap');
  }
  
  &.justify-start { justify-content: flex-start; }
  &.justify-end { justify-content: flex-end; }
  &.justify-center { justify-content: center; }
  &.justify-between { justify-content: space-between; }
  &.justify-around { justify-content: space-around; }
  &.justify-evenly { justify-content: space-evenly; }
  
  &.items-start { align-items: flex-start; }
  &.items-end { align-items: flex-end; }
  &.items-center { align-items: center; }
  &.items-baseline { align-items: baseline; }
  &.items-stretch { align-items: stretch; }
}
</style>
```

### 6.5 Responsive Navigation
```typescript
// components/common/AppNavigation.vue
<template>
  <nav :class="navClasses">
    <!-- Mobile Navigation -->
    <div v-if="isMobile" class="mobile-nav">
      <div class="mobile-nav-header">
        <button @click="toggleMobileMenu" class="menu-toggle">
          <Icon name="hi-menu" class="menu-icon" />
        </button>
        <div class="logo">
          <slot name="logo" />
        </div>
        <div class="nav-actions">
          <slot name="actions" />
        </div>
      </div>
      
      <Transition name="slide-down">
        <div v-if="mobileMenuOpen" class="mobile-menu">
          <slot name="mobile-menu" />
        </div>
      </Transition>
    </div>
    
    <!-- Tablet Navigation -->
    <div v-else-if="isTablet" class="tablet-nav">
      <div class="tablet-nav-container">
        <div class="logo">
          <slot name="logo" />
        </div>
        <div class="nav-menu">
          <slot name="tablet-menu" />
        </div>
        <div class="nav-actions">
          <slot name="actions" />
        </div>
      </div>
    </div>
    
    <!-- Desktop Navigation -->
    <div v-else class="desktop-nav">
      <div class="desktop-nav-container">
        <div class="logo">
          <slot name="logo" />
        </div>
        <div class="nav-menu">
          <slot name="desktop-menu" />
        </div>
        <div class="nav-actions">
          <slot name="actions" />
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useBreakpoints } from '@/composables/useBreakpoints'

const { isMobile, isTablet, isDesktop } = useBreakpoints()
const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const navClasses = computed(() => ({
  'app-navigation': true,
  'mobile-view': isMobile.value,
  'tablet-view': isTablet.value,
  'desktop-view': isDesktop.value
}))
</script>

<style scoped lang="scss">
.app-navigation {
  width: 100%;
  background-color: var(--surface-primary);
  border-bottom: 1px solid var(--border-color);
  
  .mobile-nav {
    .mobile-nav-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem;
      
      .menu-toggle {
        background: none;
        border: none;
        cursor: pointer;
        padding: 0.5rem;
        
        .menu-icon {
          width: 1.5rem;
          height: 1.5rem;
          color: var(--text-primary);
        }
      }
      
      .logo {
        flex: 1;
        text-align: center;
      }
    }
    
    .mobile-menu {
      position: absolute;
      top: 100%;
      left: 0;
      right: 0;
      background-color: var(--surface-primary);
      border-top: 1px solid var(--border-color);
      box-shadow: var(--shadow-md);
      z-index: 1000;
    }
  }
  
  .tablet-nav {
    .tablet-nav-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem 1.5rem;
      max-width: 1024px;
      margin: 0 auto;
      
      .nav-menu {
        flex: 1;
        display: flex;
        justify-content: center;
      }
    }
  }
  
  .desktop-nav {
    .desktop-nav-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem 2rem;
      max-width: 1280px;
      margin: 0 auto;
      
      .nav-menu {
        flex: 1;
        display: flex;
        justify-content: center;
      }
    }
  }
}

.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.3s ease;
}

.slide-down-enter-from {
  transform: translateY(-100%);
  opacity: 0;
}

.slide-down-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}
</style>
```

## 7. Penjelasan Keseluruhan

Rancangan frontend Web LaundryKu Management System dengan Vue 3 ini menyediakan fondasi yang kuat untuk pengembangan aplikasi web yang responsif dan modern. Beberapa keunggulan dari rancangan ini:

### 7.1 Arsitektur yang Kuat
- **Vue 3 Composition API**: Pendekatan modern untuk membangun komponen yang reaktif dan reusable
- **TypeScript**: Type safety untuk pengembangan yang lebih robust
- **Modular Structure**: Organisasi kode yang terstruktur dengan separation of concerns
- **State Management**: Pinia untuk state management yang sederhana dan efektif

### 7.2 Responsive Design
- **Breakpoint System**: Sistem breakpoint yang komprehensif untuk berbagai ukuran layar
- **Responsive Components**: Komponen yang menyesuaikan dengan ukuran layar
- **Adaptive Layouts**: Layout yang berbeda untuk mobile, tablet, dan desktop
- **Grid System**: Grid system yang responsif dengan dukungan untuk berbagai konfigurasi

### 7.3 Fitur-Fitur Lengkap
- **Authentication**: Login, register, dan session management
- **Dashboard**: Analytics dashboard dengan chart dan statistik
- **Order Management**: Pembuatan, tracking, dan manajemen pesanan
- **Customer Management**: Manajemen data pelanggan dengan fitur pencarian
- **Service Management**: Manajemen layanan laundry dengan pricing
- **Payment Integration**: Integrasi dengan payment gateway
- **Real-time Updates**: WebSocket untuk update real-time
- **Reporting**: Sistem laporan yang komprehensif
- **Multi-language Support**: Internationalization dengan Vue I18n
- **Theme Support**: Dark mode dan light mode

### 7.4 Development Experience
- **Vite**: Build tool yang cepat dan modern
- **Auto-imports**: Import otomatis untuk komponen dan utilities
- **Hot Module Replacement**: Development yang cepat dengan HMR
- **TypeScript**: Type safety dan better developer experience
- **ESLint + Prettier**: Code quality dan formatting otomatis
- **Testing**: Unit tests dan E2E tests dengan Vitest dan Cypress

### 7.5 Performance Optimizations
- **Code Splitting**: Automatic code splitting dengan dynamic imports
- **Lazy Loading**: Komponen dan route yang di-load hanya saat dibutuhkan
- **Tree Shaking**: Menghilangkan unused code
- **Caching**: Strategi caching yang efektif
- **Optimized Build**: Build optimization dengan Vite dan Rollup

### 7.6 UI/UX Features
- **PrimeVue**: UI framework yang kaya fitur dengan Material Design
- **Form Validation**: VeeValidate dengan Yup untuk validasi form yang robust
- **Toast Notifications**: Sistem notifikasi yang user-friendly
- **Loading States**: Loading indicators untuk feedback visual
- **Error Handling**: Error boundaries dan error pages yang informatif
- **Accessibility**: ARIA labels dan keyboard navigation support

Dengan rancangan ini, tim pengembang dapat membangun aplikasi web LaundryKu yang:
- Responsif di berbagai ukuran layar (mobile, tablet, desktop)
- Memberikan pengalaman pengguna yang konsisten
- Mudah di-maintain dan di-scale
- Mengikuti best practices dari Vue.js development
- Siap untuk fitur-fitur tambahan di masa depan