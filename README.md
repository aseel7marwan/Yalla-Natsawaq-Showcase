<div align="center">

# 🛒 Yalla Natsawaq — يلا نتسوق

### A Hyper-Local Super App Connecting Communities

[![Flutter](https://img.shields.io/badge/Flutter-3.6+-02569B?style=for-the-badge&logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.6+-0175C2?style=for-the-badge&logo=dart&logoColor=white)](https://dart.dev)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com)
[![iOS](https://img.shields.io/badge/iOS-000000?style=for-the-badge&logo=apple&logoColor=white)](https://www.apple.com/ios)
[![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://developer.android.com)

![Status](https://img.shields.io/badge/Status-In_Development-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)

---

_Empowering local commerce through a seamless, multi-role digital marketplace._

</div>

---

## 📖 About The Project

**Yalla Natsawaq** (Arabic: يلا نتسوق — _"Let's Go Shopping"_) is a **hyper-local super app** designed to revolutionize the way local communities shop, sell, and deliver.

In many regions, local merchants struggle to reach nearby customers digitally, while customers lack a unified platform to browse, order, and receive products from their neighborhood stores. **Yalla Natsawaq bridges this gap** by creating a complete ecosystem that connects three key stakeholders — **merchants**, **customers**, and **delivery drivers** — all managed through a powerful **admin dashboard**.

> **What is a Hyper-Local Super App?**
> A single platform that handles multiple services — shopping, ordering, delivery, and business management — all optimized for a local geographic radius. Think of it as your neighborhood's all-in-one digital marketplace.

### 🎯 The Problem It Solves

| Challenge                              | Solution                                                   |
| -------------------------------------- | ---------------------------------------------------------- |
| Local merchants lack digital presence  | Dedicated merchant portal with product & order management  |
| Customers can't discover nearby stores | Geo-aware browsing with categories, search, and promotions |
| No reliable last-mile delivery         | Integrated driver network with real-time GPS tracking      |
| Fragmented management tools            | Unified admin dashboard with analytics & user control      |

---

## 📸 Screenshots

> _UI showcases and visual features of the platform._

_(Add your image links here using HTML <img width="400" src="..." /> tags to align them properly)_

---

## ✨ Key Features

### 🏗️ Multi-Role Architecture

Yalla Natsawaq supports **4 distinct user roles**, each with a tailored experience:

| Role            | Capabilities                                                                                                     |
| --------------- | ---------------------------------------------------------------------------------------------------------------- |
| 🛍️ **Customer** | Browse stores, add to cart, place orders, track deliveries in real-time, receive push notifications              |
| 🏪 **Merchant** | Manage products & inventory, receive and process orders, view sales analytics, customize store profile           |
| 🚗 **Driver**   | Accept delivery assignments, navigate to pickup/drop-off, update delivery status in real-time                    |
| 🛡️ **Admin**    | Manage all users & roles, oversee orders & deliveries, view platform-wide analytics, manage banners & promotions |

### 🔐 Authentication & Security

- **OTP (One-Time Password)** phone verification via Firebase Auth
- **Google Sign-In** and **Sign in with Apple** integration
- Role-based access control enforced at both client and Firestore rules level

### 📍 Real-Time Delivery Tracking

- Live GPS tracking for active deliveries
- Real-time order status updates synced via **Cloud Firestore**
- Push notifications at every delivery milestone (accepted, picked up, delivered)

### 🔔 Smart Notifications

- Role-specific notification sounds (merchant alerts, driver radar, customer updates)
- **Firebase Cloud Messaging (FCM)** for push notifications
- Local notifications for in-app alerts

### 🎨 Polished User Experience

- Custom splash screen and onboarding flow
- Shimmer loading effects for smooth perceived performance
- Cached network images for fast, offline-capable browsing
- **RTL (Right-to-Left)** and localization support

---

## 🛠️ Built With

| Technology                                                                       | Purpose                                          |
| -------------------------------------------------------------------------------- | ------------------------------------------------ |
| **[Flutter](https://flutter.dev)**                                               | Cross-platform UI framework (iOS, Android, Web)  |
| **[Dart](https://dart.dev)**                                                     | Programming language                             |
| **[Firebase Auth](https://firebase.google.com/docs/auth)**                       | OTP, Google, and Apple authentication            |
| **[Cloud Firestore](https://firebase.google.com/docs/firestore)**                | Real-time NoSQL database                         |
| **[Firebase Storage](https://firebase.google.com/docs/storage)**                 | Product images and media storage                 |
| **[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)** | Push notifications                               |
| **[Riverpod](https://riverpod.dev)**                                             | Reactive state management (with code generation) |
| **[GoRouter](https://pub.dev/packages/go_router)**                               | Declarative routing and deep linking             |
| **[Hive](https://pub.dev/packages/hive)**                                        | Lightweight local storage / caching              |
| **[fl_chart](https://pub.dev/packages/fl_chart)**                                | Analytics charts and data visualization          |

---

## 🏛️ Architecture & State Management

### Project Structure

```
lib/
├── core/               # App-wide constants, theme, utilities, and providers
├── features/           # Feature-based modular architecture
│   ├── admin/          # Admin dashboard, user management, analytics
│   ├── auth/           # OTP verification, social sign-in, role selection
│   ├── cart/           # Shopping cart logic and UI
│   ├── delivery/       # Driver interface and delivery tracking
│   ├── home/           # Customer-facing storefront and product browsing
│   ├── merchant/       # Merchant dashboard, product & order management
│   ├── orders/         # Order lifecycle management
│   ├── appointments/   # Service appointment scheduling
│   ├── banners/        # Promotional banner management
│   ├── onboarding/     # First-launch onboarding flow
│   └── splash/         # Splash screen
├── services/           # Shared services (notifications, location, etc.)
├── shared/             # Shared widgets and components
└── main.dart           # App entry point and Firebase initialization
```

### State Management with Riverpod

The app leverages **Riverpod** with code generation (`riverpod_annotation` + `riverpod_generator`) for a clean, testable, and scalable state management approach:

- **Role-Based Providers** — Separate provider trees for each user role ensure isolated, predictable state across Customer, Merchant, Driver, and Admin flows.
- **Reactive Data Streams** — Firestore streams are wrapped in Riverpod `StreamProvider`s, enabling the UI to react to real-time database changes (e.g., new orders, delivery updates) with zero polling.
- **Dependency Injection** — Services and repositories are provided through Riverpod, making the architecture modular and easily testable.

### Real-Time Data Flow

```
User Action → Riverpod Provider → Firestore Write
                                        ↓
                              Cloud Firestore (Real-time Sync)
                                        ↓
              Riverpod StreamProvider ← Firestore Snapshot
                                        ↓
                              UI Rebuild (All Connected Clients)
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

- **Flutter SDK** `>= 3.6.0` — [Installation Guide](https://docs.flutter.dev/get-started/install)
- **Dart SDK** `>= 3.6.0` (bundled with Flutter)
- **Firebase CLI** — [Installation Guide](https://firebase.google.com/docs/cli)
- **Android Studio** or **Xcode** (for platform-specific builds)
- A configured **Firebase project** with Auth, Firestore, Storage, and Messaging enabled

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/yalla-natsawaq.git
   cd yalla-natsawaq
   ```

2. **Install dependencies**

   ```bash
   flutter pub get
   ```

3. **Configure Firebase**

   Set up your own Firebase project and add the configuration files:

   ```bash
   # Install FlutterFire CLI
   dart pub global activate flutterfire_cli

   # Configure Firebase for your project
   flutterfire configure
   ```

   This will generate the required `firebase_options.dart` file.

4. **Run the code generator** (for Riverpod)

   ```bash
   dart run build_runner build --delete-conflicting-outputs
   ```

5. **Launch the app**

   ```bash
   # Android / iOS
   flutter run

   # Web
   flutter run -d chrome
   ```

---

## 🗺️ Roadmap

### ✅ Implemented

- [x] Multi-role authentication (OTP, Google, Apple Sign-In)
- [x] Customer storefront with product browsing and cart
- [x] Merchant dashboard with product & order management
- [x] Driver delivery interface
- [x] Admin dashboard with analytics and user management
- [x] Real-time order tracking via Cloud Firestore
- [x] Push notifications with role-specific sounds
- [x] Banner and promotion management
- [x] Onboarding and splash screen flow

### 🔜 Coming Next

- [ ] In-app chat between customers and merchants
- [ ] Advanced search with filters and sorting
- [ ] Payment gateway integration
- [ ] Multi-language support (Arabic, English, French)
- [ ] Driver route optimization
- [ ] Reviews and ratings system
- [ ] Scheduled / recurring orders

---

## 📂 Related Resources

| Resource                 | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| `firestore.rules`        | Firestore security rules with role-based access control |
| `firestore.indexes.json` | Composite indexes for optimized queries                 |
| `firebase.json`          | Firebase project configuration                          |

---

## ⚖️ License & Intellectual Property

> **⚠️ Proprietary / Showcase Only**
> This repository serves primarily as a technical portfolio piece. The architecture, concepts, and source code (where visible) are proprietary. Unauthorized copying, modification, distribution, or commercial use of this project is strictly prohibited without explicit written permission from the author.

---

## 👤 Author & Contact

**Aseel Marwan Kheder** _Full-Stack Softwareentwickler | Experte für DSGVO-konforme Plattformen & Native Apps_

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/aseel-marwan-kheder-36b17033b/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/aseel7marwan)

📧 **Email:** [aseel.marwan.kheder@gmail.com](mailto:aseel.marwan.kheder@gmail.com)

---

<div align="center">

_Built with ❤️ using Flutter & Firebase_

</div>
