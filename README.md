# Fullstack Asset Management System

A robust, enterprise-grade asset management solution built with **.NET 8** and **Next.js 15+**. This system enables organizations to track lifecycle, inspections, and repairs of their physical assets with QR code integration.

---

## 🚀 Features

- **📊 Comprehensive Dashboard:** Real-time statistics and charts showing asset health, status distribution, and recent activities.
- **📦 Asset Lifecycle Management:** Full CRUD operations for assets, including detailed filtering and pagination.
- **🔍 QR Code Integration:** 
  - **Scanning:** Built-in scanner to quickly identify assets and view their history.
  - **Generation:** Automatic generation of unique QR labels for every asset.
- **🛠️ Repair Workflow:** Integrated system to report damages, request repairs, and track the status of maintenance tasks.
- **📝 Inspection Logs:** Detailed recording of asset inspections and damage assessments.
- **🔐 Secure Authentication:** Enterprise-ready login powered by **Azure Active Directory (Azure AD)**.
- **📜 Audit Trails:** Automatic logging of all major operations for accountability and history tracking.
- **📱 Responsive Design:** Modern, mobile-first UI built with **Tailwind CSS 4** and **Shadcn UI**.

---

## 🛠️ Tech Stack

### Backend
- **Framework:** .NET 8 Web API
- **Database:** PostgreSQL 16
- **ORM:** Entity Framework Core
- **Auth:** Microsoft Identity Web (Azure AD Integration)
- **Documentation:** Swagger / OpenAPI

### Frontend
- **Framework:** Next.js (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS 4 + Shadcn UI
- **State/Forms:** React Hook Form + Zod
- **Auth:** NextAuth.js
- **Charts:** Recharts
- **QR:** jsQR (Scanning) & qrcode.react (Generation)

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/)
- [Node.js 18+](https://nodejs.org/) (for local frontend development)
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) (for local backend development)
- An **Azure AD Tenant** for authentication configuration.

---

## 🚀 Installation & Setup Guide

### 1. Azure Active Directory Setup
This project uses **Microsoft Entra ID (Azure AD)** for authentication. You must register an application in the [Azure Portal](https://portal.azure.com/):

**A. Backend API Registration:**
- Register a new "Web API" application.
- Expose an API (e.g., `api://your-client-id`).
- Add a scope (e.g., `access_as_user`).

**B. Frontend Web Registration:**
- Register a new "Web" application.
- Set the Redirect URI to: `http://{domain}/api/auth/callback/azure-ad`
- Generate a **Client Secret**.
- Grant API permissions to the Backend API scope created in step A.

### 2. Environment Configuration
Create a `.env.docker` file in the root directory. Use `.env.docker.example` as a template:

```env
# Database
POSTGRES_USER=your_user
POSTGRES_PASSWORD=your_password
POSTGRES_DB=asset_db

# Backend (.NET)
ConnectionStrings__DefaultConnection=Host=postgres-db;Port=5432;Database=asset_db;Username=your_user;Password=your_password;
AzureAd__TenantId=your-tenant-id
AzureAd__ClientId=your-backend-client-id

# Frontend (Next.js)
AZURE_AD_CLIENT_ID=your-frontend-client-id
AZURE_AD_CLIENT_SECRET=your-client-secret
AZURE_AD_TENANT_ID=your-tenant-id
NEXTAUTH_SECRET=a-random-32-char-string
```

### 3. Running the Application

#### Using Docker (Recommended)
> **Note:** Docker handles all dependencies (`dotnet restore`, `npm install`, etc.) automatically inside the containers. You do NOT need to run them manually on your host machine.
```bash
# Build and start all services
docker-compose up -d --build
```

#### Running Locally for Development
**Backend:**
```bash
cd Asset-Management-BE
dotnet run
```
**Frontend:**
```bash
cd Asset-Management-FE
npm install
npm run dev
```

---

## 📂 Project Structure

```text
├── Asset-Management-BE/   # .NET 8 Web API (Backend)
│   ├── Controllers/       # API Endpoints
│   ├── Models/            # Database Entities
│   ├── Data/              # DB Context & Migrations
│   └── Services/          # Business Logic
├── Asset-Management-FE/   # Next.js Application (Frontend)
│   ├── app/               # App Router Pages & Layouts
│   ├── components/        # Reusable UI Components
│   ├── lib/               # Utilities & API Clients
│   └── hooks/             # Custom React Hooks
├── docker-compose.yml     # Container Orchestration
└── Caddyfile              # Reverse proxy configuration
```
