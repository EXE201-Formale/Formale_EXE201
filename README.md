# 👔 Formale - AI-Powered Fashion E-commerce Platform

<div align="center">

![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=Swagger&logoColor=black)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON%20web%20tokens&logoColor=white)

**Formale** is a fashion e-commerce platform integrated with Artificial Intelligence (AI) to suggest outfits that match users' personal styles.

[Features](#-key-features) •
[Installation](#-installation) •
[API Endpoints](#-api-endpoints) •
[Architecture](#-system-architecture) •
[Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [Key Features](#-key-features)
- [Technologies Used](#-technologies-used)
- [System Architecture](#-system-architecture)
- [Project Structure](#-project-structure)
- [Database](#-database)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [API Endpoints](#-api-endpoints)
- [Authentication & Authorization](#-authentication--authorization)
- [AI Integration](#-ai-integration)
- [Payment](#-payment)
- [Contributing](#-contributing)

---

## ✨ Key Features

### 🛍️ **E-commerce**
- Fashion product management (clothing, footwear, accessories)
- Shopping cart and online ordering
- Integrated PayOS payment gateway
- Product reviews and feedback

### 🤖 **AI-Powered Outfit Suggestions**
- Style analysis from natural language descriptions
- Automatic outfit suggestions (Tops + Bottoms + Footwear + Accessories)
- Combines products from personal closet and system inventory
- Save and manage outfit combos

### 👤 **User Management**
- Registration with OTP email verification
- Login via account or Google OAuth 2.0
- Role-based authorization system (Admin, User, Manager)
- Premium packages with advanced features

### 📦 **Virtual Closet**
- Store favorite products
- Manage created outfits
- Search and filter products in closet

---

## 🛠 Technologies Used

### Backend Framework
| Technology | Version | Description |
|-----------|-----------|-------|
| **.NET** | 8.0 | Main framework |
| **Entity Framework Core** | 9.0 | Database ORM |
| **SQL Server** | - | Relational database |

### Authentication & Security
| Technology | Description |
|-----------|-------|
| **JWT Bearer** | Token-based authentication |
| **Google OAuth 2.0** | Social login |
| **OTP via Email** | Account verification |

### Third-party Integrations
| Service | Description |
|---------|-------|
| **PayOS** | Vietnam payment gateway |
| **Cloudinary** | Image storage and management |
| **OpenRouter AI** | AI outfit suggestions (DeepSeek model) |
| **SMTP (MimeKit)** | Email verification service |

### Supporting Libraries
| Library | Version | Description |
|----------|-----------|-------|
| **AutoMapper** | 14.0 | Object mapping |
| **FluentValidation** | 12.0 | Data validation |
| **Swashbuckle** | 6.6.2 | Swagger/OpenAPI |
| **RestSharp** | 112.1 | HTTP client |
| **Google.Apis.Auth** | 1.69 | Google authentication |

---

## 🏗 System Architecture

The project is built following **Clean Architecture** with 4 layers:

```
┌─────────────────────────────────────────────────────────────┐
│                      PRESENTATION LAYER                     │
│                          (API)                              │
│   Controllers │ AutoMapper │ Swagger │ Middleware          │
├─────────────────────────────────────────────────────────────┤
│                      APPLICATION LAYER                      │
│                      (Application)                          │
│   Services │ DTOs │ Interfaces │ Validation │ Settings     │
├─────────────────────────────────────────────────────────────┤
│                      INFRASTRUCTURE LAYER                   │
│                      (Infrastructure)                       │
│   DbContext │ Repositories │ Migrations │ External APIs    │
├─────────────────────────────────────────────────────────────┤
│                        DOMAIN LAYER                         │
│                         (Domain)                            │
│   Entities │ Enums │ Base Classes │ Business Rules         │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

```
Client Request → Controller → Service → Repository → Database
                    ↓            ↓
               Validation    Business Logic
                    ↓            ↓
              DTO Mapping   Entity Mapping
```

---

## 📁 Project Structure

```
Formale_EXE201/
├── 📂 API/                          # Presentation Layer
│   ├── Controllers/                 # REST API Controllers
│   │   ├── AuthController.cs        # Authentication
│   │   ├── ProductController.cs     # Products
│   │   ├── CartController.cs        # Shopping Cart
│   │   ├── OrderController.cs       # Orders
│   │   ├── PaymentController.cs     # Payments
│   │   ├── OutfitController.cs      # AI Outfit Suggestions
│   │   ├── UserClosetController.cs  # Virtual Closet
│   │   ├── FeedbackController.cs    # Reviews
│   │   └── ...
│   ├── Mapper/
│   │   └── AutoMapperProfile.cs     # AutoMapper Configuration
│   ├── Properties/
│   │   └── launchSettings.json
│   ├── Program.cs                   # Application entry point
│   └── API.csproj
│
├── 📂 Application/                   # Application Layer
│   ├── DTO/                         # Data Transfer Objects
│   │   ├── LoginDTO.cs
│   │   ├── RegisterDTO.cs
│   │   ├── ProductRequestDto.cs
│   │   ├── ProductResponseDto.cs
│   │   ├── OutfitSuggestionDto.cs
│   │   ├── PaymentDTO.cs
│   │   └── ...
│   ├── Interface/                   # Service Interfaces
│   │   ├── IProductService.cs
│   │   ├── IOutfitService.cs
│   │   ├── IPaymentService.cs
│   │   └── ...
│   ├── Service/                     # Service Implementations
│   │   ├── ProductService.cs
│   │   ├── OutfitService.cs
│   │   ├── OpenRouterService.cs     # AI Integration
│   │   ├── PaymentService.cs
│   │   ├── PayOsService.cs
│   │   ├── CloudinaryService.cs
│   │   ├── EmailService.cs
│   │   └── ...
│   ├── Settings/                    # Configuration classes
│   │   ├── JwtSetting.cs
│   │   ├── EmailSettings.cs
│   │   ├── PayOsSetting.cs
│   │   └── GoogleSetting.cs
│   ├── Validation/                  # FluentValidation rules
│   └── Application.csproj
│
├── 📂 Domain/                        # Domain Layer
│   ├── Entities/                    # Domain Entities
│   │   ├── UserAccount.cs
│   │   ├── Product.cs
│   │   ├── Order.cs
│   │   ├── Payment.cs
│   │   ├── OutfitCombo.cs
│   │   ├── UserCloset.cs
│   │   └── ...
│   ├── Enum/                        # Enumerations
│   │   ├── Status.cs
│   │   ├── PaymentMethod.cs
│   │   └── PremiumPackageTier.cs
│   ├── Base/                        # Base classes
│   └── Domain.csproj
│
├── 📂 Infrastructure/                # Infrastructure Layer
│   ├── Repository/                  # Data Access
│   │   ├── UserRepository.cs
│   │   ├── ProductRepository.cs
│   │   ├── OrderRepository.cs
│   │   └── ...
│   ├── Base/                        # Generic Repository
│   ├── migrations/                  # EF Core Migrations
│   ├── AppDBContext.cs              # Database Context
│   └── Infrastructure.csproj
│
├── Formale_EXE201.sln               # Solution file
└── README.md
```

---

## 🗄 Database

### Entity Relationship Diagram

```
┌──────────────────┐       ┌──────────────────┐       ┌──────────────────┐
│   UserAccount    │       │     Product      │       │      Order       │
├──────────────────┤       ├──────────────────┤       ├──────────────────┤
│ UserId (PK)      │       │ ProductId (PK)   │       │ OrderId (PK)     │
│ FullName         │       │ Name             │       │ UserId (FK)      │
│ Email            │       │ Price            │       │ TotalPrice       │
│ Password         │       │ BrandId (FK)     │       │ Status           │
│ RoleId (FK)      │       │ ColorId (FK)     │       │ CreatedAt        │
│ PremiumPackageId │       │ StyleId (FK)     │       │ UpdatedAt        │
│ IsActive         │       │ CategoryId (FK)  │       └────────┬─────────┘
│ Status           │       │ MaterialId (FK)  │                │
└────────┬─────────┘       │ TypeId (FK)      │                │
         │                 │ ImageURL         │       ┌────────▼─────────┐
         │                 │ IsSystemCreated  │       │    OrderItem     │
         │                 └────────┬─────────┘       ├──────────────────┤
         │                          │                 │ OrderItemId (PK) │
         │                          │                 │ OrderId (FK)     │
┌────────▼─────────┐       ┌────────▼─────────┐       │ ProductId (FK)   │
│    UserCloset    │       │     Feedback     │       │ Quantity         │
├──────────────────┤       ├──────────────────┤       │ Price            │
│ ClosetId (PK)    │       │ FeedbackId (PK)  │       └──────────────────┘
│ UserId (FK)      │       │ UserId (FK)      │
│ ProductId (FK)   │       │ ProductId (FK)   │
│ ComboId (FK)     │       │ Rating           │
└──────────────────┘       │ Comment          │
                           └──────────────────┘

┌──────────────────┐       ┌──────────────────┐       ┌──────────────────┐
│   OutfitCombo    │       │ OutfitComboItem  │       │     Payment      │
├──────────────────┤       ├──────────────────┤       ├──────────────────┤
│ ComboId (PK)     │───┐   │ ItemId (PK)      │       │ Id (PK)          │
│ Name             │   │   │ ComboId (FK)     │───────│ UserId (FK)      │
│ Description      │   └──▶│ ProductId (FK)   │       │ OrderId (FK)     │
│ UserId (FK)      │       │ Slot             │       │ OrderCode        │
└──────────────────┘       └──────────────────┘       │ Amount           │
                                                      │ Status           │
┌──────────────────┐       ┌──────────────────┐       │ PaymentUrl       │
│  PremiumPackage  │       │      Roles       │       └──────────────────┘
├──────────────────┤       ├──────────────────┤
│ PackageId (PK)   │       │ RoleId (PK)      │
│ Name             │       │ RoleName         │
│ Price            │       │ • Admin (1)      │
│ DurationInDays   │       │ • User (2)       │
│ Tier             │       │ • Manager (3)    │
└──────────────────┘       └──────────────────┘
```

### Main Entities

#### 👤 **UserAccount**
```csharp
- UserId, FullName, Email, UserName, Password
- PhoneNumber, Address, DateOfBirth
- RoleId, PremiumPackageId, PremiumExpiryDate
- Token, OTP, OtpExpiry
- IsActive, Status, LoginProvider
- Image_User, Background_Image, Description
```

#### 👕 **Product**
```csharp
- ProductId, Name, Price, Description, ImageURL
- BrandId, ColorId, StyleId, CategoryId, MaterialId, TypeId
- IsSystemCreated, UserId
- TotalFeedbacks, AverageRating
- IsDeleted, CreatedAt, UpdatedAt (from BaseEntity)
```

#### 🛒 **Order & OrderItem**
```csharp
Order:
- OrderId, UserId, TotalPrice, Status
- PaidAt, CreatedAt, UpdatedAt

OrderItem:
- OrderItemId, OrderId, ProductId
- Quantity, Price
```

#### 💳 **Payment**
```csharp
- Id, UserId, OrderId, PremiumPackageId
- OrderCode, Amount, Description
- BuyerName, BuyerEmail, BuyerPhone, BuyerAddress
- PaymentUrl, CheckoutUrl, TransactionId
- Status, Method, Signature
- CancelUrl, ReturnUrl, CancelReason
```

#### 👔 **OutfitCombo & OutfitComboItem**
```csharp
OutfitCombo:
- ComboId, Name, Description, UserId

OutfitComboItem:
- ItemId, ComboId, ProductId, Slot
```

### Enums

```csharp
// Status (Order/Payment)
enum Status { PENDING, COMPLETE, FAILED, CANCELLED }

// PaymentMethod
enum PaymentMethod { VNPAY, MOMO, PayOs }

// PremiumPackageTier
enum PremiumPackageTier { Premium, Gold }
```

---

## 🚀 Installation

### System Requirements
- **.NET SDK** 8.0 or higher
- **SQL Server** 2019 or higher
- **Visual Studio 2022** or **VS Code**
- **Git**

### Step 1: Clone repository
```bash
git clone https://github.com/your-username/Formale_EXE201.git
cd Formale_EXE201
```

### Step 2: Restore packages
```bash
dotnet restore
```

### Step 3: Configure appsettings.json
Create `appsettings.json` file in `API/` folder (see [Configuration](#-configuration))

### Step 4: Apply migrations
```bash
cd API
dotnet ef database update --project ../Infrastructure
```

### Step 5: Run application
```bash
dotnet run --project API
```

### Step 6: Access Swagger
Open browser and navigate to:
```
https://localhost:5001/swagger
```

---

## ⚙ Configuration

Create `appsettings.json` file in `API/` folder:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  
  "ConnectionStrings": {
    "DefaultConnection": "Server=YOUR_SERVER;Database=FormaleDB;Trusted_Connection=True;TrustServerCertificate=True;"
  },
  
  "JwtSettings": {
    "Issuer": "FormaleAPI",
    "Audience": "FormaleClient",
    "SecretKey": "YOUR_SUPER_SECRET_KEY_AT_LEAST_32_CHARACTERS_LONG",
    "ExpiryInMinutes": 60
  },
  
  "EmailSettings": {
    "SmtpHost": "smtp.gmail.com",
    "SmtpPort": 587,
    "SmtpUser": "your-email@gmail.com",
    "SmtpPass": "your-app-password"
  },
  
  "PayOsConfig": {
    "BaseUrl": "https://api-merchant.payos.vn",
    "ClientId": "YOUR_PAYOS_CLIENT_ID",
    "ApiKey": "YOUR_PAYOS_API_KEY",
    "ChecksumKey": "YOUR_PAYOS_CHECKSUM_KEY"
  },
  
  "GoogleSetting": {
    "ClientId": "YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com",
    "ClientSecret": "YOUR_GOOGLE_CLIENT_SECRET"
  },
  
  "OpenRouter": {
    "ApiKey": "YOUR_OPENROUTER_API_KEY"
  },
  
  "Cloudinary": {
    "CloudName": "YOUR_CLOUDINARY_CLOUD_NAME",
    "ApiKey": "YOUR_CLOUDINARY_API_KEY",
    "ApiSecret": "YOUR_CLOUDINARY_API_SECRET"
  }
}
```

### How to Get Credentials

| Service | Guide |
|---------|-----------|
| **PayOS** | Register at [payos.vn](https://payos.vn) |
| **Google OAuth** | Create project at [Google Cloud Console](https://console.cloud.google.com) |
| **OpenRouter** | Register at [openrouter.ai](https://openrouter.ai) |
| **Cloudinary** | Register at [cloudinary.com](https://cloudinary.com) |
| **Gmail SMTP** | Create App Password in Google Account Settings |

---

## 📡 API Endpoints

### 🔐 Authentication (`/api/Auth`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `POST` | `/register` | Register new account | ❌ |
| `POST` | `/register-manager` | Create Manager account | Admin |
| `POST` | `/login` | Login | ❌ |
| `POST` | `/change-password` | Change password (requires OTP) | ✅ |
| `POST` | `/logout` | Logout | ✅ |
| `POST` | `/active-account` | Activate account with OTP | ❌ |
| `POST` | `/resend-otp` | Resend OTP code | ❌ |
| `GET` | `/signin-google` | Login with Google | ❌ |

### 👥 Users (`/api/User`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/` | Get all users | Admin |
| `GET` | `/get-user-info` | Get current user info | ✅ |
| `PUT` | `/update-profile` | Update profile | User |
| `DELETE` | `/{userId}` | Delete user | Admin |
| `POST` | `/ban/{userId}` | Ban user | Admin |
| `POST` | `/unban/{userId}` | Unban user | Admin |

### 👕 Products (`/api/Product`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/` | Get all products | ❌ |
| `GET` | `/{id}` | Get product by ID | ❌ |
| `POST` | `/` | Create new product | ✅ |
| `PUT` | `/{id}` | Update product | ✅ |
| `PUT` | `/update-image/{id}` | Update product image | ✅ |
| `DELETE` | `/{id}` | Delete product (soft delete) | Admin |
| `GET` | `/search` | Search with filter & pagination | ❌ |
| `POST` | `/suggest` | AI outfit suggestion | Premium |

### 🛒 Cart (`/api/Cart`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/` | Get current cart | ✅ |
| `POST` | `/add-item/{productId}` | Add product to cart | ✅ |
| `POST` | `/reduce-item/{productId}` | Reduce product quantity | ✅ |
| `GET` | `/preview` | Preview order | ✅ |
| `DELETE` | `/remove-item/{productId}` | Remove product from cart | ✅ |

### 📦 Orders (`/api/Order`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `POST` | `/create-from-cart` | Create order from cart | ✅ |
| `GET` | `/all` | Get all orders | Admin |
| `GET` | `/{orderId}` | Get order by ID | Admin |

### 💳 Payments (`/api/Payment`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/getpayment` | Get all payments | Admin |
| `GET` | `/getpayment-byuser` | Get user's payments | ✅ |
| `POST` | `/create` | Create new payment | ✅ |
| `POST` | `/search-transaction` | Search by transaction ID | ✅ |
| `POST` | `/cancel` | Cancel payment | ✅ |
| `PUT` | `/update-status/{paymentId}` | Update status | Admin |
| `GET` | `/check-status/{orderCode}` | Check PayOS status | ✅ |
| `GET` | `/premium-payments` | Premium package payments | Admin |
| `POST` | `/confirm-premium-payment` | Confirm Premium payment | Admin |

### 👔 Outfit - AI Suggestion (`/api/Outfit`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `POST` | `/suggest` | Suggest outfit from closet | Premium |
| `POST` | `/save` | Save suggested combo | ✅ |
| `GET` | `/{comboId}` | Get combo details | ✅ |
| `PUT` | `/{comboId}/replace-item` | Replace item in combo | ✅ |
| `GET` | `/user-combos` | Get user's combos list | ✅ |
| `PUT` | `/update-combo-info` | Update combo name/description | ✅ |

### 🗄️ User Closet (`/api/UserCloset`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/` | Get all closets | Admin |
| `GET` | `/{closetId}` | Get closet by ID | User |
| `DELETE` | `/{closetId}` | Remove item from closet | User |
| `GET` | `/my-closet` | Get user's closet | ✅ |
| `GET` | `/my-items` | Get products in closet | ✅ |
| `GET` | `/my-combos` | Get outfit combos | ✅ |
| `GET` | `/search` | Search in closet | ✅ |

### ⭐ Feedback (`/api/Feedback`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `POST` | `/create` | Create new review | ✅ |
| `PUT` | `/update` | Update review | ✅ |
| `GET` | `/rating/{productId}` | Get rating statistics | ❌ |
| `GET` | `/` | Get product feedbacks | ❌ |
| `GET` | `/user-feedbacks` | Get user's feedbacks | ✅ |
| `DELETE` | `/{feedbackId}` | Delete feedback | Admin |
| `GET` | `/all` | Get all feedbacks | Admin |

### 💎 Premium Packages (`/api/PremiunPackage`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/` | Get packages list | ❌ |
| `POST` | `/{packageId}` | Get package by ID | ❌ |
| `POST` | `/update/{packageId}` | Update package | Admin |
| `POST` | `/buy` | Purchase Premium package | ✅ |
| `POST` | `/update-premium` | Assign Premium to user | Admin |

### 📊 Analytics (`/api/Log`)

| Method | Endpoint | Description | Auth |
|--------|----------|-------|------|
| `GET` | `/all` | Get all visits | Admin |
| `GET` | `/today` | Today's visits | Admin |
| `GET` | `/{date}` | Visits by date | Admin |
| `GET` | `/registrations-this-month` | Registrations this month | Admin |

### 🏷️ Product Attributes

Each attribute has CRUD endpoints:

| Controller | Endpoint Base |
|------------|---------------|
| ProductBrand | `/api/ProductBrand` |
| ProductCategory | `/api/ProductCategory` |
| ProductColor | `/api/ProductColor` |
| ProductMaterial | `/api/ProductMaterial` |
| ProductStyle | `/api/ProductStyle` |
| ProductType | `/api/ProductType` |

---

## 🔐 Authentication & Authorization

### JWT Authentication

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Roles

| RoleId | Role Name | Permissions |
|--------|-----------|-----------|
| 1 | **Admin** | Full system access |
| 2 | **User** | Shopping, reviews, closet |
| 3 | **Manager** | Manage products, orders |

### Authentication Flow

```
1. Register → Send OTP via email
2. Confirm OTP → Activate account
3. Login → Receive JWT token
4. API Request → Send Bearer token
5. Change password → Confirm with new OTP
```

### Google OAuth Flow

```
1. Client redirect → /api/Auth/signin-google
2. Google authentication
3. Callback with ID token
4. Server validates token
5. Create/update user
6. Return JWT token
```

---

## 🤖 AI Integration

### AI Outfit Suggestion Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     User Input                              │
│     "I want to wear something for a fancy party"           │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                   OpenRouter Service                        │
│   Model: deepseek/deepseek-r1-0528-qwen3-8b:free           │
│   Task: Classify input → Style (Formal, Casual, etc.)      │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼ Style: "Formal"
┌─────────────────────────────────────────────────────────────┐
│                    Outfit Service                           │
│   1. Get products from User Closet by Style                 │
│   2. Fallback: Get from System Products if missing          │
│   3. Create combo: Tops + Bottoms + Footwear + Accessories  │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                  OutfitSuggestionDto                        │
│   - Style: "Formal"                                         │
│   - ComboId: guid                                           │
│   - Tops: { ProductId, Name, Price, ImageURL, ... }        │
│   - Bottoms: { ... }                                        │
│   - Footwears: { ... }                                      │
│   - Accessories: { ... }                                    │
│   - MissingNotice: ["Missing Tops - Use Outfit System"]    │
└─────────────────────────────────────────────────────────────┘
```

### Supported Styles

| Style | Description |
|-------|-------|
| **Casual** | Everyday wear |
| **Formal** | Business, office wear |
| **Streetwear** | Street style |
| **Sporty** | Athletic wear |
| **Vintage** | Classic style |
| **Minimalist** | Minimalist |
| **Bohemian** | Boho style |

### API Usage

```http
POST /api/Outfit/suggest
Authorization: Bearer {token}
Content-Type: application/json

{
  "prompt": "I want to wear something casual for a weekend coffee with friends"
}
```

**Response:**
```json
{
  "style": "Casual",
  "comboId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "tops": {
    "productId": "...",
    "name": "T-Shirt Basic White",
    "price": 299000,
    "imageURL": "https://..."
  },
  "bottoms": { ... },
  "footwears": { ... },
  "accessories": { ... },
  "missingNotice": []
}
```

---

## 💳 Payment

### PayOS Integration

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│   Client    │ ──▶  │  Formale    │ ──▶  │   PayOS     │
│             │      │    API      │      │    API      │
└─────────────┘      └─────────────┘      └─────────────┘
       │                    │                    │
       │  1. Create Order   │                    │
       │ ──────────────────▶│                    │
       │                    │  2. Create Payment │
       │                    │ ──────────────────▶│
       │                    │                    │
       │                    │  3. Checkout URL   │
       │                    │ ◀──────────────────│
       │  4. Redirect URL   │                    │
       │ ◀──────────────────│                    │
       │                    │                    │
       │  5. Complete Payment on PayOS           │
       │ ───────────────────────────────────────▶│
       │                    │                    │
       │                    │  6. Webhook/Poll   │
       │                    │ ◀──────────────────│
       │                    │                    │
       │  7. Order Complete │                    │
       │ ◀──────────────────│                    │
```

### Payment Status Flow

```
PENDING → COMPLETE (Payment successful)
        → CANCELLED (Cancelled by user)
        → FAILED (Payment error)
```

### API Usage

**Create Payment:**
```http
POST /api/Payment/create
{
  "orderId": 123,
  "returnUrl": "https://yourapp.com/payment/success",
  "cancelUrl": "https://yourapp.com/payment/cancel"
}
```

**Check Status:**
```http
GET /api/Payment/check-status/{orderCode}
```

---

## 📊 Services Overview

| Service | Main Functions |
|---------|----------------|
| `UserAccountService` | Registration, login, OTP, Google OAuth |
| `UserService` | CRUD users, profile management |
| `ProductService` | CRUD products, search, filter |
| `CartService` | Shopping cart management |
| `OrderService` | Create orders from cart |
| `PaymentService` | Payment management |
| `PayOsService` | PayOS API integration |
| `PremiumService` | Premium package management |
| `OutfitService` | AI outfit suggestions |
| `OutfitComboItemService` | Manage items in combo |
| `UserClosetService` | Virtual closet |
| `FeedbackService` | Product reviews |
| `CloudinaryService` | Upload/delete images |
| `EmailService` | SMTP email sending |
| `OpenRouterService` | AI model calls |
| `VisitLogService` | Analytics, statistics |
| `CurrentUserService` | Get user from JWT claims |

---

## 🧪 Testing

### Swagger UI

Access Swagger to test API:
```
https://localhost:5001/swagger
```

### Test with JWT

1. Login via `/api/Auth/login`
2. Copy token from response
3. Click "Authorize" in Swagger
4. Enter: `Bearer {your-token}`
5. Test protected endpoints

---

## 📝 Code Conventions

### Naming Conventions

| Type | Convention | Example |
|------|------------|-------|
| Class | PascalCase | `ProductService` |
| Method | PascalCase | `GetAllProducts()` |
| Variable | camelCase | `productList` |
| Property | PascalCase | `ProductId` |
| Interface | IPascalCase | `IProductService` |
| DTO | PascalCase + Dto | `ProductResponseDto` |

### Project Structure Rules

- **Controllers**: Only routing and validation
- **Services**: Business logic
- **Repositories**: Data access
- **DTOs**: Data transfer, no logic
- **Entities**: Domain models

---

## 🤝 Contributing

1. Fork repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 📞 Contact

- **Project Link**: [https://github.com/EXE201-Formale](https://github.com/EXE201-Formale)

---

<div align="center">

**⭐ Star this repo if you find it helpful! ⭐**

Made with ❤️ by Formale Team

</div>
