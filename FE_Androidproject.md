

# Rancangan Frontend Android LaundryKu Management System dengan Jetpack Compose

## 1. Arsitektur Aplikasi

### 1.1 High-Level Architecture
```
┌──────────────────────────────────────────────────────────────────┐
│                      Presentation Layer                          │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │   UI        │ │   View      │ │   State     │ │   Event     │ │
│  │ Components  │ │ Models      │ │ Management  │ │  Handling   │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────┐
│                      Domain Layer                                │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │ Use Cases   │ │ Entities    │ │ Repository  │ │ Exceptions  │ │
│  │ (Interactor)│ │             │ │  Interfaces │ │             │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────┐
│                      Data Layer                                  │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │
│  │ Remote Data │ │ Local Data  │ │ Repository  │ │ Data        │ │
│  │ Sources     │ │ Sources     │ │  Impl       │ │ Models      │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### 1.2 Teknologi Utama
- **UI Framework**: Jetpack Compose (BOM 2023.10.x)
- **Architecture**: MVVM with Clean Architecture
- **Navigation**: Navigation Compose
- **State Management**: ViewModel + StateFlow + SavedStateHandle
- **Dependency Injection**: Hilt
- **Networking**: Retrofit + OkHttp
- **Local Storage**: Room + DataStore
- **Async Programming**: Coroutines + Flow
- **Image Loading**: Coil
- **Adaptive UI**: Material Design 3 + Window Size Classes

## 2. Struktur Folder Proyek

```
laundryku-android/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/
│   │   │   │       └── laundryku/
│   │   │   │           ├── LaundryKuApplication.kt
│   │   │   │           ├── di/
│   │   │   │           │   ├── AppModule.kt
│   │   │   │           │   ├── DatabaseModule.kt
│   │   │   │           │   ├── NetworkModule.kt
│   │   │   │           │   └── RepositoryModule.kt
│   │   │   │           ├── data/
│   │   │   │           │   ├── local/
│   │   │   │           │   │   ├── dao/
│   │   │   │           │   │   │   ├── UserDao.kt
│   │   │   │           │   │   │   ├── LaundryDao.kt
│   │   │   │           │   │   │   ├── OrderDao.kt
│   │   │   │           │   │   │   └── ServiceDao.kt
│   │   │   │           │   │   ├── database/
│   │   │   │           │   │   │   └── AppDatabase.kt
│   │   │   │           │   │   ├── datastore/
│   │   │   │           │   │   │   └── PreferencesDataStore.kt
│   │   │   │           │   │   └── entity/
│   │   │   │           │   │       ├── UserEntity.kt
│   │   │   │           │   │       ├── LaundryEntity.kt
│   │   │   │           │   │       ├── OrderEntity.kt
│   │   │   │           │   │       └── ServiceEntity.kt
│   │   │   │           │   ├── model/
│   │   │   │           │   │   ├── dto/
│   │   │   │           │   │   │   ├── UserDto.kt
│   │   │   │           │   │   │   ├── LaundryDto.kt
│   │   │   │           │   │   │   ├── OrderDto.kt
│   │   │   │           │   │   │   └── ServiceDto.kt
│   │   │   │           │   │   └── response/
│   │   │   │           │   │       ├── ApiResponse.kt
│   │   │   │           │   │       ├── PaginatedResponse.kt
│   │   │   │           │   │       └── ErrorResponse.kt
│   │   │   │           │   └── remote/
│   │   │   │           │       ├── api/
│   │   │   │           │       │   ├── ApiService.kt
│   │   │   │           │       │   ├── AuthApi.kt
│   │   │   │           │       │   ├── UserApi.kt
│   │   │   │           │       │   ├── LaundryApi.kt
│   │   │   │           │       │   ├── OrderApi.kt
│   │   │   │           │       │   ├── ServiceApi.kt
│   │   │   │           │       │   ├── PaymentApi.kt
│   │   │   │           │       │   └── NotificationApi.kt
│   │   │   │           │       ├── interceptor/
│   │   │   │           │       │   ├── AuthInterceptor.kt
│   │   │   │           │       │   └── ErrorInterceptor.kt
│   │   │   │           │       ├── retrofit/
│   │   │   │           │       │   └── RetrofitClient.kt
│   │   │   │           │       └── WebSocket/
│   │   │   │           │           └── WebSocketManager.kt
│   │   │   │           ├── domain/
│   │   │   │           │   ├── model/
│   │   │   │           │   │   ├── User.kt
│   │   │   │           │   │   ├── Laundry.kt
│   │   │   │           │   │   ├── Order.kt
│   │   │   │           │   │   ├── Service.kt
│   │   │   │           │   │   ├── Payment.kt
│   │   │   │           │   │   └── Notification.kt
│   │   │   │           │   ├── repository/
│   │   │   │           │   │   ├── UserRepository.kt
│   │   │   │           │   │   ├── LaundryRepository.kt
│   │   │   │           │   │   ├── OrderRepository.kt
│   │   │   │           │   │   ├── ServiceRepository.kt
│   │   │   │           │   │   ├── PaymentRepository.kt
│   │   │   │           │   │   └── NotificationRepository.kt
│   │   │   │           │   ├── usecase/
│   │   │   │           │   │   ├── auth/
│   │   │   │           │   │   │   ├── LoginUseCase.kt
│   │   │   │           │   │   │   ├── RegisterUseCase.kt
│   │   │   │           │   │   │   ├── LogoutUseCase.kt
│   │   │   │           │   │   │   └── RefreshTokenUseCase.kt
│   │   │   │           │   │   ├── user/
│   │   │   │           │   │   │   ├── GetUserProfileUseCase.kt
│   │   │   │           │   │   │   ├── UpdateUserProfileUseCase.kt
│   │   │   │           │   │   │   └── ChangePasswordUseCase.kt
│   │   │   │           │   │   ├── laundry/
│   │   │   │           │   │   │   ├── GetLaundriesUseCase.kt
│   │   │   │           │   │   │   ├── GetLaundryDetailUseCase.kt
│   │   │   │           │   │   │   └── SearchLaundriesUseCase.kt
│   │   │   │           │   │   ├── order/
│   │   │   │           │   │   │   ├── CreateOrderUseCase.kt
│   │   │   │           │   │   │   ├── GetOrdersUseCase.kt
│   │   │   │           │   │   │   ├── GetOrderDetailUseCase.kt
│   │   │   │           │   │   │   ├── UpdateOrderStatusUseCase.kt
│   │   │   │           │   │   │   └── CancelOrderUseCase.kt
│   │   │   │           │   │   ├── service/
│   │   │   │           │   │   │   ├── GetServicesUseCase.kt
│   │   │   │           │   │   │   ├── GetServiceDetailUseCase.kt
│   │   │   │           │   │   │   └── GetServicesByLaundryUseCase.kt
│   │   │   │           │   │   ├── payment/
│   │   │   │           │   │   │   ├── ProcessPaymentUseCase.kt
│   │   │   │           │   │   │   ├── GetPaymentMethodsUseCase.kt
│   │   │   │           │   │   │   └── GetPaymentHistoryUseCase.kt
│   │   │   │           │   │   └── notification/
│   │   │   │           │   │       ├── GetNotificationsUseCase.kt
│   │   │   │           │   │       ├── MarkNotificationReadUseCase.kt
│   │   │   │           │   │       └── SendNotificationUseCase.kt
│   │   │   │           │   └── exception/
│   │   │   │           │       ├── NetworkException.kt
│   │   │   │           │       ├── AuthenticationException.kt
│   │   │   │           │       ├── NotFoundException.kt
│   │   │   │           │       └── ValidationException.kt
│   │   │   │           ├── presentation/
│   │   │   │           │   ├── theme/
│   │   │   │           │   │   ├── Color.kt
│   │   │   │           │   │   ├── Type.kt
│   │   │   │           │   │   └── Shape.kt
│   │   │   │           │   ├── ui/
│   │   │   │           │   │   ├── components/
│   │   │   │           │   │   │   ├── common/
│   │   │   │           │   │   │   │   ├── LoadingIndicator.kt
│   │   │   │           │   │   │   │   ├── ErrorScreen.kt
│   │   │   │           │   │   │   │   ├── EmptyState.kt
│   │   │   │           │   │   │   │   ├── PullRefreshIndicator.kt
│   │   │   │           │   │   │   │   ├── SearchBar.kt
│   │   │   │           │   │   │   │   └── PaginationLoader.kt
│   │   │   │           │   │   │   ├── form/
│   │   │   │           │   │   │   │   ├── CustomTextField.kt
│   │   │   │           │   │   │   │   ├── PasswordTextField.kt
│   │   │   │           │   │   │   │   ├── DropdownField.kt
│   │   │   │           │   │   │   │   ├── DatePickerField.kt
│   │   │   │           │   │   │   │   ├── CheckboxField.kt
│   │   │   │           │   │   │   │   └── RadioButtonField.kt
│   │   │   │           │   │   │   ├── card/
│   │   │   │           │   │   │   │   ├── LaundryCard.kt
│   │   │   │           │   │   │   │   ├── OrderCard.kt
│   │   │   │           │   │   │   │   ├── ServiceCard.kt
│   │   │   │           │   │   │   │   └── NotificationCard.kt
│   │   │   │           │   │   │   ├── button/
│   │   │   │           │   │   │   │   ├── PrimaryButton.kt
│   │   │   │           │   │   │   │   ├── SecondaryButton.kt
│   │   │   │           │   │   │   │   ├── TextButton.kt
│   │   │   │           │   │   │   │   └── IconButton.kt
│   │   │   │           │   │   │   ├── dialog/
│   │   │   │           │   │   │   │   ├── ConfirmationDialog.kt
│   │   │   │           │   │   │   │   ├── InfoDialog.kt
│   │   │   │           │   │   │   │   └── ProgressDialog.kt
│   │   │   │           │   │   │   ├── bottomsheet/
│   │   │   │           │   │   │   │   ├── FilterBottomSheet.kt
│   │   │   │           │   │   │   │   ├── SortBottomSheet.kt
│   │   │   │           │   │   │   │   └── PaymentMethodBottomSheet.kt
│   │   │   │           │   │   │   ├── navigation/
│   │   │   │           │   │   │   │   ├── BottomNavigationBar.kt
│   │   │   │           │   │   │   │   ├── TopAppBar.kt
│   │   │   │           │   │   │   │   └── NavigationDrawer.kt
│   │   │   │           │   │   │   └── adaptive/
│   │   │   │           │   │   │     ├── AdaptiveLayout.kt
│   │   │   │           │   │   │     ├── ResponsiveScreen.kt
│   │   │   │           │   │   │     └── WindowSizeClass.kt
│   │   │   │           │   │   ├── screen/
│   │   │   │           │   │   │   ├── auth/
│   │   │   │           │   │   │   │   ├── LoginScreen.kt
│   │   │   │           │   │   │   │   ├── RegisterScreen.kt
│   │   │   │           │   │   │   │   ├── ForgotPasswordScreen.kt
│   │   │   │           │   │   │   │   └── OnboardingScreen.kt
│   │   │   │           │   │   │   ├── main/
│   │   │   │           │   │   │   │   ├── HomeScreen.kt
│   │   │   │           │   │   │   │   ├── OrderScreen.kt
│   │   │   │           │   │   │   │   ├── HistoryScreen.kt
│   │   │   │           │   │   │   │   ├── ProfileScreen.kt
│   │   │   │           │   │   │   │   └── NotificationScreen.kt
│   │   │   │           │   │   │   ├── laundry/
│   │   │   │           │   │   │   │   ├── LaundryListScreen.kt
│   │   │   │           │   │   │   │   ├── LaundryDetailScreen.kt
│   │   │   │           │   │   │   │   ├── LaundryMapScreen.kt
│   │   │   │           │   │   │   │   └── LaundrySearchScreen.kt
│   │   │   │           │   │   │   ├── order/
│   │   │   │           │   │   │   │   ├── CreateOrderScreen.kt
│   │   │   │           │   │   │   │   ├── OrderDetailScreen.kt
│   │   │   │           │   │   │   │   ├── OrderTrackingScreen.kt
│   │   │   │           │   │   │   │   └── OrderReviewScreen.kt
│   │   │   │           │   │   │   ├── service/
│   │   │   │           │   │   │   │   ├── ServiceListScreen.kt
│   │   │   │           │   │   │   │   ├── ServiceDetailScreen.kt
│   │   │   │           │   │   │   │   └── ServiceBookingScreen.kt
│   │   │   │           │   │   │   ├── payment/
│   │   │   │           │   │   │   │   ├── PaymentScreen.kt
│   │   │   │           │   │   │   │   ├── PaymentMethodScreen.kt
│   │   │   │           │   │   │   │   └── PaymentHistoryScreen.kt
│   │   │   │           │   │   │   ├── profile/
│   │   │   │           │   │   │   │   ├── UserProfileScreen.kt
│   │   │   │           │   │   │   │   ├── EditProfileScreen.kt
│   │   │   │           │   │   │   │   ├── AddressScreen.kt
│   │   │   │           │   │   │   │   ├── SettingsScreen.kt
│   │   │   │           │   │   │   │   └── HelpScreen.kt
│   │   │   │           │   │   │   └── staff/
│   │   │   │           │   │   │     ├── StaffDashboardScreen.kt
│   │   │   │           │   │   │     ├── StaffOrderListScreen.kt
│   │   │   │           │   │   │     ├── StaffOrderDetailScreen.kt
│   │   │   │           │   │   │     └── StaffProfileScreen.kt
│   │   │   │           │   ├── navigation/
│   │   │   │           │   │   ├── AppNavigation.kt
│   │   │   │           │   │   ├── MainNavigator.kt
│   │   │   │           │   │   └── AuthNavigator.kt
│   │   │   │           │   └── viewmodel/
│   │   │   │           │       ├── auth/
│   │   │   │           │       │   ├── LoginViewModel.kt
│   │   │   │           │       │   ├── RegisterViewModel.kt
│   │   │   │           │       │   └── ForgotPasswordViewModel.kt
│   │   │   │           │       ├── main/
│   │   │   │           │       │   ├── HomeViewModel.kt
│   │   │   │           │       │   ├── OrderViewModel.kt
│   │   │   │           │       │   ├── HistoryViewModel.kt
│   │   │   │           │       │   ├── ProfileViewModel.kt
│   │   │   │           │       │   └── NotificationViewModel.kt
│   │   │   │           │       ├── laundry/
│   │   │   │           │       │   ├── LaundryListViewModel.kt
│   │   │   │           │       │   ├── LaundryDetailViewModel.kt
│   │   │   │           │       │   └── LaundryMapViewModel.kt
│   │   │   │           │       ├── order/
│   │   │   │           │       │   ├── CreateOrderViewModel.kt
│   │   │   │           │       │   ├── OrderDetailViewModel.kt
│   │   │   │           │       │   └── OrderTrackingViewModel.kt
│   │   │   │           │       ├── service/
│   │   │   │           │       │   ├── ServiceListViewModel.kt
│   │   │   │           │       │   └── ServiceDetailViewModel.kt
│   │   │   │           │       ├── payment/
│   │   │   │           │       │   ├── PaymentViewModel.kt
│   │   │   │           │       │   └── PaymentMethodViewModel.kt
│   │   │   │           │       └── profile/
│   │   │   │           │           ├── UserProfileViewModel.kt
│   │   │   │           │           ├── EditProfileViewModel.kt
│   │   │   │           │           └── SettingsViewModel.kt
│   │   │   │           └── util/
│   │   │   │               ├── extension/
│   │   │   │               │   ├── StringExtension.kt
│   │   │   │               │   ├── DateExtension.kt
│   │   │   │               │   ├── ViewExtension.kt
│   │   │   │               │   └── CollectionExtension.kt
│   │   │   │               ├── constant/
│   │   │   │               │   ├── AppConstant.kt
│   │   │   │               │   ├── ApiConstant.kt
│   │   │   │               │   └── NavigationConstant.kt
│   │   │   │               └── helper/
│   │   │   │                   ├── NetworkHelper.kt
│   │   │   │                   ├── ValidationHelper.kt
│   │   │   │                   ├── DateHelper.kt
│   │   │   │                   └── ImageHelper.kt
│   │   │   ├── res/
│   │   │   │   ├── drawable/
│   │   │   │   ├── mipmap/
│   │   │   │   ├── values/
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   ├── dimens.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   ├── values-night/
│   │   │   │   ├── values-w600dp/
│   │   │   │   ├── values-w1240dp/
│   │   │   │   ├── layout/
│   │   │   │   ├── navigation/
│   │   │   │   └── xml/
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   │       └── java/
│   │           └── com/
│   │               └── laundryku/
│   │                   ├── ExampleUnitTest.kt
│   │                   └── ViewModelTest.kt
│   └── build.gradle.kts
├── build.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
├── gradle/
├── local.properties
└── README.md
```

## 3. Library yang Dibutuhkan (build.gradle.kts - Module Level)

```kotlin
plugins {
    alias(libs.plugins.com.android.application)
    alias(libs.plugins.org.jetbrains.kotlin.android)
    alias(libs.plugins.kotlin.kapt)
    alias(libs.plugins.kotlin.parcelize)
    alias(libs.plugins.dagger.hilt.android)
    alias(libs.plugins.kotlin.serialization)
    alias(libs.plugins.kotlin.ksp)
    alias(libs.plugins.androidx.navigation.safeargs)
}

android {
    namespace = "com.laundryku"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.laundryku"
        minSdk = 24
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
        vectorDrawables {
            useSupportLibrary = true
        }
    }

    buildTypes {
        release {
            isMinifyEnabled = true
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
        debug {
            isMinifyEnabled = false
            applicationIdSuffix = ".debug"
        }
    }
    
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }
    
    kotlinOptions {
        jvmTarget = "17"
        freeCompilerArgs = listOf(
            "-Xskip-prerelease-check",
            "-opt-in=androidx.compose.material3.ExperimentalMaterial3Api",
            "-opt-in=androidx.compose.foundation.ExperimentalFoundationApi",
            "-opt-in=androidx.compose.animation.ExperimentalAnimationApi",
            "-opt-in=androidx.compose.material3.windowsizeclass.ExperimentalMaterial3WindowSizeClassApi",
            "-opt-in=androidx.compose.material3.adaptive.ExperimentalMaterial3AdaptiveApi"
        )
    }
    
    buildFeatures {
        compose = true
        buildConfig = true
    }
    
    composeOptions {
        kotlinCompilerExtensionVersion = "1.5.4"
    }
    
    packaging {
        resources {
            excludes += "/META-INF/{AL2.0,LGPL2.1}"
        }
    }
    
    testOptions {
        unitTests {
            isIncludeAndroidResources = true
        }
    }
    
    sourceSets {
        getByName("main") {
            java.srcDir("src/main/java")
            res.srcDir("src/main/res")
        }
        getByName("test") {
            java.srcDir("src/test/java")
            res.srcDir("src/test/res")
        }
    }
}

dependencies {
    // Core Android & Compose
    implementation(libs.androidx.core.ktx)
    implementation(libs.androidx.lifecycle.runtime.ktx)
    implementation(libs.androidx.activity.compose)
    implementation(platform(libs.androidx.compose.bom))
    implementation(libs.androidx.compose.ui)
    implementation(libs.androidx.compose.ui.graphics)
    implementation(libs.androidx.compose.ui.tooling.preview)
    implementation(libs.androidx.compose.material3)
    implementation(libs.androidx.compose.material3.window.size)
    implementation(libs.androidx.compose.material3.adaptive)
    implementation(libs.androidx.compose.material.icons.extended)
    
    // Navigation
    implementation(libs.androidx.navigation.compose)
    implementation(libs.androidx.navigation.runtime.ktx)
    
    // ViewModel & Lifecycle
    implementation(libs.androidx.lifecycle.viewmodel.compose)
    implementation(libs.androidx.lifecycle.runtime.compose)
    implementation(libs.androidx.lifecycle.viewmodel.ktx)
    implementation(libs.androidx.lifecycle.runtime.ktx)
    
    // Hilt (Dependency Injection)
    implementation(libs.hilt.android)
    kapt(libs.hilt.compiler)
    implementation(libs.androidx.hilt.navigation.compose)
    
    // Networking
    implementation(libs.retrofit.core)
    implementation(libs.retrofit.kotlin.serialization)
    implementation(libs.okhttp.core)
    implementation(libs.okhttp.logging)
    implementation(libs.okhttp.mockwebserver)
    
    // Serialization
    implementation(libs.kotlinx.serialization.json)
    
    // Coroutines
    implementation(libs.kotlinx.coroutines.core)
    implementation(libs.kotlinx.coroutines.android)
    implementation(libs.kotlinx.coroutines.play.services)
    testImplementation(libs.kotlinx.coroutines.test)
    
    // Room (Local Database)
    implementation(libs.androidx.room.runtime)
    implementation(libs.androidx.room.ktx)
    ksp(libs.androidx.room.compiler)
    implementation(libs.androidx.room.paging)
    
    // DataStore
    implementation(libs.androidx.datastore.preferences)
    implementation(libs.androidx.datastore.preferences.core)
    
    // Paging 3
    implementation(libs.androidx.paging.runtime)
    implementation(libs.androidx.paging.compose)
    
    // Image Loading
    implementation(libs.coil.compose)
    implementation(libs.coil.svg)
    implementation(libs.coil.video)
    
    // Accompanist (Utilities)
    implementation(libs.accompanist.systemuicontroller)
    implementation(libs.accompanist.permissions)
    implementation(libs.accompanist.placeholder)
    implementation(libs.accompanist.pager)
    implementation(libs.accompanist.pager.indicators)
    implementation(libs.accompanist.navigation.animation)
    implementation(libs.accompanist.flowlayout)
    
    // Maps & Location
    implementation(libs.google.maps.compose)
    implementation(libs.play.services.location)
    implementation(libs.play.services.maps)
    
    // Camera
    implementation(libs.androidx.camera.core)
    implementation(libs.androidx.camera.camera2)
    implementation(libs.androidx.camera.lifecycle)
    implementation(libs.androidx.camera.view)
    implementation(libs.androidx.camera.extensions)
    
    // Biometric
    implementation(libs.androidx.biometric)
    
    // Firebase
    implementation(platform(libs.firebase.bom))
    implementation(libs.firebase.analytics)
    implementation(libs.firebase.messaging)
    implementation(libs.firebase.crashlytics)
    
    // In-App Update
    implementation(libs.play.core)
    implementation(libs.play.core.ktx)
    
    // Rating & Review
    implementation(libs.play.review)
    implementation(libs.play.review.ktx)
    
    // Billing
    implementation(libs.play.billing.ktx)
    
    // AdMob
    implementation(libs.play.ads)
    
    // WebSocket
    implementation(libs.java.websocket)
    implementation(libs.okhttp.websocket)
    
    // Date & Time
    implementation(libs.threetenabp)
    
    // Logger
    implementation(libs.timber)
    
    // Testing
    testImplementation(libs.junit)
    testImplementation(libs.mockito.core)
    testImplementation(libs.mockito.kotlin)
    testImplementation(libs.kotlinx.coroutines.test)
    testImplementation(libs.androidx.arch.core.testing)
    testImplementation(libs.turbine)
    
    // Android Testing
    androidTestImplementation(libs.androidx.junit)
    androidTestImplementation(libs.androidx.espresso.core)
    androidTestImplementation(platform(libs.androidx.compose.bom))
    androidTestImplementation(libs.androidx.compose.ui.test.junit4)
    debugImplementation(libs.androidx.compose.ui.tooling)
    debugImplementation(libs.androidx.compose.ui.test.manifest)
    
    // Hilt Testing
    testImplementation(libs.hilt.android.testing)
    kaptTest(libs.hilt.compiler)
    androidTestImplementation(libs.hilt.android.testing)
    kaptAndroidTest(libs.hilt.compiler)
}
```

## 4. Konfigurasi Gradle (build.gradle.kts - Project Level)

```kotlin
plugins {
    alias(libs.plugins.android.application) apply false
    alias(libs.plugins.android.library) apply false
    alias(libs.plugins.jetbrains.kotlin.android) apply false
    alias(libs.plugins.kotlin.serialization) apply false
    alias(libs.plugins.dagger.hilt.android) apply false
    alias(libs.plugins.kotlin.ksp) apply false
    alias(libs.plugins.androidx.navigation.safeargs) apply false
}

buildscript {
    repositories {
        google()
        mavenCentral()
    }
    
    dependencies {
        classpath(libs.android.gradle.plugin)
        classpath(libs.kotlin.gradle.plugin)
        classpath(libs.hilt.android.gradle.plugin)
        classpath(libs.google.services)
        classpath(libs.firebase.crashlytics.gradle)
        classpath(libs.androidx.navigation.safeargs.gradle.plugin)
    }
}

allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://jitpack.io") }
    }
}

tasks.register("clean", Delete::class) {
    delete(rootProject.buildDir)
}
```

## 5. Version Catalog (gradle/libs.versions.toml)

```toml
[versions]
agp = "8.1.4"
kotlin = "1.9.20"
core-ktx = "1.12.0"
lifecycle-runtime-ktx = "2.6.2"
activity-compose = "1.8.2"
compose-bom = "2023.10.01"
navigation = "2.7.6"
hilt = "2.48.1"
room = "2.6.1"
retrofit = "2.9.0"
okhttp = "4.12.0"
kotlinx-serialization = "1.6.0"
coroutines = "1.7.3"
coil = "2.4.0"
accompanist = "0.32.0"
paging = "3.2.1"
datastore = "1.0.0"
camera = "1.3.0"
biometric = "1.2.0-alpha05"
firebase-bom = "32.7.0"
play-core = "1.12.1"
play-services = "18.2.0"
maps-compose = "4.3.0"
threetenabp = "1.4.6"
timber = "5.0.1"
junit = "4.13.2"
junit-version = "1.1.5"
espresso-core = "3.5.1"
mockito = "5.6.0"
turbine = "1.0.0"
material3-window = "1.1.2"
material3-adaptive = "1.0.0-alpha05"

[libraries]
androidx-core-ktx = { group = "androidx.core", name = "core-ktx", version.ref = "core-ktx" }
androidx-lifecycle-runtime-ktx = { group = "androidx.lifecycle", name = "lifecycle-runtime-ktx", version.ref = "lifecycle-runtime-ktx" }
androidx-activity-compose = { group = "androidx.activity", name = "activity-compose", version.ref = "activity-compose" }
androidx-compose-bom = { group = "androidx.compose", name = "compose-bom", version.ref = "compose-bom" }
androidx-compose-ui = { group = "androidx.compose.ui", name = "ui" }
androidx-compose-ui-graphics = { group = "androidx.compose.ui", name = "ui-graphics" }
androidx-compose-ui-tooling = { group = "androidx.compose.ui", name = "ui-tooling" }
androidx-compose-ui-tooling-preview = { group = "androidx.compose.ui", name = "ui-tooling-preview" }
androidx-compose-ui-test-manifest = { group = "androidx.compose.ui", name = "ui-test-manifest" }
androidx-compose-ui-test-junit4 = { group = "androidx.compose.ui", name = "ui-test-junit4" }
androidx-compose-material3 = { group = "androidx.compose.material3", name = "material3" }
androidx-compose-material-icons-extended = { group = "androidx.compose.material", name = "material-icons-extended" }
androidx-compose-material3-window-size = { group = "androidx.compose.material3", name = "material3-window-size-class", version.ref = "material3-window" }
androidx-compose-material3-adaptive = { group = "androidx.compose.material3", name = "material3-adaptive", version.ref = "material3-adaptive" }

androidx-navigation-compose = { group = "androidx.navigation", name = "navigation-compose", version.ref = "navigation" }
androidx-navigation-runtime-ktx = { group = "androidx.navigation", name = "navigation-runtime-ktx", version.ref = "navigation" }
androidx-lifecycle-viewmodel-compose = { group = "androidx.lifecycle", name = "lifecycle-viewmodel-compose", version.ref = "lifecycle-runtime-ktx" }
androidx-lifecycle-runtime-compose = { group = "androidx.lifecycle", name = "lifecycle-runtime-compose", version.ref = "lifecycle-runtime-ktx" }
androidx-lifecycle-viewmodel-ktx = { group = "androidx.lifecycle", name = "lifecycle-viewmodel-ktx", version.ref = "lifecycle-runtime-ktx" }

hilt-android = { group = "com.google.dagger", name = "hilt-android", version.ref = "hilt" }
hilt-compiler = { group = "com.google.dagger", name = "hilt-compiler", version.ref = "hilt" }
androidx-hilt-navigation-compose = { group = "androidx.hilt", name = "hilt-navigation-compose", version = "1.1.0" }

retrofit-core = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
retrofit-kotlin-serialization = { group = "com.squareup.retrofit2", name = "converter-kotlinx-serialization", version.ref = "retrofit" }
okhttp-core = { group = "com.squareup.okhttp3", name = "okhttp", version.ref = "okhttp" }
okhttp-logging = { group = "com.squareup.okhttp3", name = "logging-interceptor", version.ref = "okhttp" }
okhttp-mockwebserver = { group = "com.squareup.okhttp3", name = "mockwebserver", version.ref = "okhttp" }
okhttp-websocket = { group = "com.squareup.okhttp3", name = "okhttp-ws", version.ref = "okhttp" }

kotlinx-serialization-json = { group = "org.jetbrains.kotlinx", name = "kotlinx-serialization-json", version.ref = "kotlinx-serialization" }

kotlinx-coroutines-core = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-core", version.ref = "coroutines" }
kotlinx-coroutines-android = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-android", version.ref = "coroutines" }
kotlinx-coroutines-play-services = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-play-services", version.ref = "coroutines" }
kotlinx-coroutines-test = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-test", version.ref = "coroutines" }

androidx-room-runtime = { group = "androidx.room", name = "room-runtime", version.ref = "room" }
androidx-room-ktx = { group = "androidx.room", name = "room-ktx", version.ref = "room" }
androidx-room-paging = { group = "androidx.room", name = "room-paging", version.ref = "room" }

androidx-datastore-preferences = { group = "androidx.datastore", name = "datastore-preferences", version.ref = "datastore" }
androidx-datastore-preferences-core = { group = "androidx.datastore", name = "datastore-preferences-core", version.ref = "datastore" }

androidx-paging-runtime = { group = "androidx.paging", name = "paging-runtime", version.ref = "paging" }
androidx-paging-compose = { group = "androidx.paging", name = "paging-compose", version.ref = "paging" }

coil-compose = { group = "io.coil-kt", name = "coil-compose", version.ref = "coil" }
coil-svg = { group = "io.coil-kt", name = "coil-svg", version.ref = "coil" }
coil-video = { group = "io.coil-kt", name = "coil-video", version.ref = "coil" }

accompanist-systemuicontroller = { group = "com.google.accompanist", name = "accompanist-systemuicontroller", version.ref = "accompanist" }
accompanist-permissions = { group = "com.google.accompanist", name = "accompanist-permissions", version.ref = "accompanist" }
accompanist-placeholder = { group = "com.google.accompanist", name = "accompanist-placeholder", version.ref = "accompanist" }
accompanist-pager = { group = "com.google.accompanist", name = "accompanist-pager", version.ref = "accompanist" }
accompanist-pager-indicators = { group = "com.google.accompanist", name = "accompanist-pager-indicators", version.ref = "accompanist" }
accompanist-navigation-animation = { group = "com.google.accompanist", name = "accompanist-navigation-animation", version.ref = "accompanist" }
accompanist-flowlayout = { group = "com.google.accompanist", name = "accompanist-flowlayout", version.ref = "accompanist" }

google-maps-compose = { group = "com.google.maps.android", name = "maps-compose", version.ref = "maps-compose" }
play-services-location = { group = "com.google.android.gms", name = "play-services-location", version.ref = "play-services" }
play-services-maps = { group = "com.google.android.gms", name = "play-services-maps", version.ref = "play-services" }

androidx-camera-core = { group = "androidx.camera", name = "camera-core", version.ref = "camera" }
androidx-camera-camera2 = { group = "androidx.camera", name = "camera-camera2", version.ref = "camera" }
androidx-camera-lifecycle = { group = "androidx.camera", name = "camera-lifecycle", version.ref = "camera" }
androidx-camera-view = { group = "androidx.camera", name = "camera-view", version.ref = "camera" }
androidx-camera-extensions = { group = "androidx.camera", name = "camera-extensions", version.ref = "camera" }

androidx-biometric = { group = "androidx.biometric", name = "biometric", version.ref = "biometric" }

firebase-bom = { group = "com.google.firebase", name = "firebase-bom", version.ref = "firebase-bom" }
firebase-analytics = { group = "com.google.firebase", name = "firebase-analytics-ktx" }
firebase-messaging = { group = "com.google.firebase", name = "firebase-messaging-ktx" }
firebase-crashlytics = { group = "com.google.firebase", name = "firebase-crashlytics-ktx" }

play-core = { group = "com.google.android.play", name = "core", version.ref = "play-core" }
play-core-ktx = { group = "com.google.android.play", name = "core-ktx", version.ref = "play-core" }
play-review = { group = "com.google.android.play", name = "review", version.ref = "play-core" }
play-review-ktx = { group = "com.google.android.play", name = "review-ktx", version.ref = "play-core" }
play-billing-ktx = { group = "com.android.billingclient", name = "billing-ktx", version.ref = "play-core" }
play-ads = { group = "com.google.android.gms", name = "play-services-ads", version.ref = "play-services" }

java-websocket = { group = "org.java-websocket", name = "Java-WebSocket", version = "1.5.3" }

threetenabp = { group = "com.jakewharton.threetenabp", name = "threetenabp", version.ref = "threetenabp" }

timber = { group = "com.jakewharton.timber", name = "timber", version.ref = "timber" }

junit = { group = "junit", name = "junit", version.ref = "junit" }
junit-version = { group = "androidx.test.ext", name = "junit", version.ref = "junit-version" }
espresso-core = { group = "androidx.test.espresso", name = "espresso-core", version.ref = "espresso-core" }
mockito-core = { group = "org.mockito", name = "mockito-core", version.ref = "mockito" }
mockito-kotlin = { group = "org.mockito.kotlin", name = "mockito-kotlin", version.ref = "mockito" }
androidx-arch-core-testing = { group = "androidx.arch.core", name = "core-testing", version = "2.2.0" }
turbine = { group = "app.cash.turbine", name = "turbine", version.ref = "turbine" }
hilt-android-testing = { group = "com.google.dagger", name = "hilt-android-testing", version.ref = "hilt" }

[plugins]
com-android-application = { id = "com.android.application", version.ref = "agp" }
org-jetbrains-kotlin-android = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }
kotlin-kapt = { id = "org.jetbrains.kotlin.kapt", version.ref = "kotlin" }
kotlin-parcelize = { id = "org.jetbrains.kotlin.plugin.parcelize", version.ref = "kotlin" }
dagger-hilt-android = { id = "com.google.dagger.hilt.android", version.ref = "hilt" }
kotlin-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }
kotlin-ksp = { id = "com.google.devtools.ksp", version = "1.9.20-1.0.14" }
androidx-navigation-safeargs = { id = "androidx.navigation.safeargs.kotlin", version.ref = "navigation" }

# Gradle plugins
android-gradle-plugin = { id = "com.android.application", version.ref = "agp" }
kotlin-gradle-plugin = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }
hilt-android-gradle-plugin = { id = "com.google.dagger.hilt.android", version.ref = "hilt" }
google-services = { id = "com.google.gms.google-services", version = "4.4.0" }
firebase-crashlytics = { id = "com.google.firebase.crashlytics", version = "2.9.9" }
androidx-navigation-safeargs-gradle-plugin = { id = "androidx.navigation.safeargs.kotlin", version.ref = "navigation" }
```

## 6. Penjelasan Struktur Adaptive UI

### 6.1 Window Size Classes
Material Design 3 memperkenalkan Window Size Classes untuk mengkategorikan ukuran layar menjadi kategori yang lebih bermakna:

```kotlin
// WindowSizeClass.kt
enum class WindowSizeClass {
    COMPACT,   // Phone portrait
    MEDIUM,    // Tablet portrait, Foldable portrait
    EXPANDED   // Tablet landscape, Desktop
}

// WindowSizeClassUtil.kt
fun getWindowSizeClass(windowWidthDp: Int): WindowSizeClass {
    return when {
        windowWidthDp < 600 -> WindowSizeClass.COMPACT
        windowWidthDp < 840 -> WindowSizeClass.MEDIUM
        else -> WindowSizeClass.EXPANDED
    }
}
```

### 6.2 Adaptive Layout Strategy
```kotlin
// AdaptiveLayout.kt
@Composable
fun AdaptiveLayout(
    windowSizeClass: WindowSizeClass,
    content: @Composable () -> Unit
) {
    when (windowSizeClass) {
        WindowSizeClass.COMPACT -> {
            // Phone layout - single column
            CompactLayout(content = content)
        }
        WindowSizeClass.MEDIUM -> {
            // Tablet portrait - two columns
            MediumLayout(content = content)
        }
        WindowSizeClass.EXPANDED -> {
            // Tablet landscape/desktop - three columns
            ExpandedLayout(content = content)
        }
    }
}
```

### 6.3 Navigation Drawer Adaptation
```kotlin
// NavigationDrawer.kt
@Composable
fun AdaptiveNavigationDrawer(
    windowSizeClass: WindowSizeClass,
    navigationContent: @Composable () -> Unit,
    content: @Composable () -> Unit
) {
    if (windowSizeClass == WindowSizeClass.COMPACT) {
        // Bottom navigation for compact screens
        BottomNavigationLayout(content = content)
    } else {
        // Navigation drawer for medium and expanded screens
        PermanentNavigationDrawer(
            drawerContent = navigationContent,
            content = content
        )
    }
}
```

### 6.4 List Detail Layout
```kotlin
// ListDetailLayout.kt
@Composable
fun ListDetailLayout(
    windowSizeClass: WindowSizeClass,
    listContent: @Composable () -> Unit,
    detailContent: @Composable () -> Unit
) {
    if (windowSizeClass == WindowSizeClass.COMPACT) {
        // Separate screens for list and detail
        var showDetail by remember { mutableStateOf(false) }
        if (showDetail) {
            detailContent()
        } else {
            listContent()
        }
    } else {
        // Side by side layout
        Row {
            Box(modifier = Modifier.weight(1f)) {
                listContent()
            }
            Box(modifier = Modifier.weight(1f)) {
                detailContent()
            }
        }
    }
}
```

## 7. Penjelasan Multi-Screen Support

### 7.1 Responsive Screen Components
```kotlin
// ResponsiveScreen.kt
@Composable
fun ResponsiveScreen(
    modifier: Modifier = Modifier,
    content: @Composable (windowSizeClass: WindowSizeClass) -> Unit
) {
    val configuration = LocalConfiguration.current
    val windowMetrics = rememberWindowMetrics()
    val windowDpSize = windowMetrics.bounds.toSize()
    val windowWidthDp = windowDpSize.width.dp.value.toInt()
    
    val windowSizeClass = remember(windowWidthDp) {
        getWindowSizeClass(windowWidthDp)
    }
    
    Box(modifier = modifier) {
        content(windowSizeClass)
    }
}
```

### 7.2 Adaptive Typography
```kotlin
// AdaptiveTypography.kt
@Composable
fun adaptiveTextStyle(
    windowSizeClass: WindowSizeClass,
    compactStyle: TextStyle,
    mediumStyle: TextStyle,
    expandedStyle: TextStyle
): TextStyle {
    return when (windowSizeClass) {
        WindowSizeClass.COMPACT -> compactStyle
        WindowSizeClass.MEDIUM -> mediumStyle
        WindowSizeClass.EXPANDED -> expandedStyle
    }
}
```

### 7.3 Adaptive Spacing
```kotlin
// AdaptiveSpacing.kt
@Composable
fun adaptivePadding(
    windowSizeClass: WindowSizeClass,
    compact: PaddingValues = PaddingValues(),
    medium: PaddingValues = PaddingValues(),
    expanded: PaddingValues = PaddingValues()
): PaddingValues {
    return when (windowSizeClass) {
        WindowSizeClass.COMPACT -> compact
        WindowSizeClass.MEDIUM -> medium
        WindowSizeClass.EXPANDED -> expanded
    }
}
```

### 7.4 Adaptive Grid Layout
```kotlin
// AdaptiveGrid.kt
@Composable
fun AdaptiveGrid(
    windowSizeClass: WindowSizeClass,
    items: List<Any>,
    modifier: Modifier = Modifier,
    content: @Composable (Any) -> Unit
) {
    val columns = when (windowSizeClass) {
        WindowSizeClass.COMPACT -> 1
        WindowSizeClass.MEDIUM -> 2
        WindowSizeClass.EXPANDED -> 3
    }
    
    LazyVerticalGrid(
        columns = GridCells.Fixed(columns),
        modifier = modifier
    ) {
        items(items) { item ->
            content(item)
        }
    }
}
```

## 8. Penjelasan Keseluruhan

Rancangan frontend Android LaundryKu Management System dengan Jetpack Compose ini menyediakan fondasi yang kuat untuk pengembangan aplikasi yang responsif dan adaptif. Beberapa keunggulan dari rancangan ini:

### 8.1 Arsitektur yang Kuat
- **Clean Architecture**: Pemisahan yang jelas antara layer Presentation, Domain, dan Data
- **MVVM Pattern**: ViewModel untuk state management dengan StateFlow
- **Dependency Injection**: Hilt untuk manajemen dependency yang efisien
- **Repository Pattern**: Abstraksi untuk data sources

### 8.2 Modern UI dengan Jetpack Compose
- **Declarative UI**: Pendekatan modern untuk membangun UI
- **Material Design 3**: Desain terbaru dari Google dengan theming yang kaya
- **Reactive Programming**: State management yang reaktif dengan Compose

### 8.3 Multi-Screen Support
- **Window Size Classes**: Kategorisasi ukuran layar yang bermakna
- **Adaptive Layouts**: Layout yang menyesuaikan dengan ukuran layar
- **Responsive Components**: Komponen yang beradaptasi dengan window size
- **Navigation Adaptation**: Pola navigasi yang berbeda untuk setiap ukuran layar

### 8.4 Fitur-Fitur Lengkap
- **Authentication**: Login, register, dan session management
- **Order Management**: Pembuatan, tracking, dan manajemen pesanan
- **Payment Integration**: Integrasi dengan payment gateway
- **Real-time Updates**: WebSocket untuk update real-time
- **Offline Support**: Room database dan DataStore untuk local storage
- **Push Notifications**: Firebase Cloud Messaging
- **Maps Integration**: Google Maps untuk lokasi laundry
- **Camera Integration**: Untuk dokumentasi pesanan

### 8.5 Development Experience
- **Type Safety**: Kotlin dengan null safety dan type inference
- **Testing**: Unit tests dan UI tests yang komprehensif
- **Build System**: Gradle dengan version catalog untuk dependency management
- **Code Quality**: Linting dan formatting otomatis
- **Documentation**: Komentar KDoc yang lengkap

### 8.6 Performance Optimizations
- **Paging 3**: Untuk data yang besar dengan loading yang efisien
- **Coil**: Image loading yang efisien dengan caching
- **Coroutines**: Background processing yang non-blocking
- **Lazy Loading**: Komponen yang di-load hanya saat dibutuhkan

Dengan rancangan ini, tim pengembang dapat membangun aplikasi Android LaundryKu yang:
- Berjalan di berbagai ukuran layar (phone, tablet, foldable)
- Memberikan pengalaman pengguna yang konsisten
- Mudah di-maintain dan di-scale
- Mengikuti best practices dari Android development
- Siap untuk fitur-fitur tambahan di masa depan