# Gym Management System - Power Fitness

## 📋 Project Overview

Power Fitness is a complete gym management system built with ASP.NET Core MVC using **3-Layer Architecture** principles.

**Dependency Flow:** PL → BLL → DAL
- PL handles HTTP requests, MVC controllers, Razor views, authentication, and authorization.
- BLL contains business logic, services, validation, view models, and mapping.
- DAL handles data persistence using Entity Framework Core, SQL Server, repositories, Unit of Work, and database configurations.

## 🚀 Getting Started

### Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [Visual Studio](https://visualstudio.microsoft.com/) with ASP.NET and web development workload

### Step 1: Clone the Repository

```bash
git clone https://github.com/Bola-Edward/Gym-Management-System.git
cd Gym-Management-System
```

### Step 2: Update Database Connection

Open `GymManagementSystem.PL/appsettings.json` and update the connection string:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=YOUR_SERVER_NAME; Database=YOUR_DATABASE_NAME; Trusted_Connection=True; TrustServerCertificate=True;"
  }
}
```

### Step 3: Set Startup Project

In Visual Studio:
1. Right-click on **GymManagementSystem.PL** → **Set as Startup Project**
2. Ensure **GymManagementSystem.PL** is bolded

### Step 4: Apply Database Migrations

Open **Package Manager Console** (Tools → NuGet Package Manager → Package Manager Console)

**Set Default project to:** `GymManagementSystem.DAL`

Then run:

```powershell
Update-Database
```

If you need to create a new migration (after model changes):

```powershell
Add-Migration "MigrationName"
Update-Database
```

### Step 5: Seed Initial Data

> ⚠️ **Important**: The database is seeded automatically when you run the application for the first time.

The seeders is configured in `GymManagementSystem.DAL/Seeder/` and registered in `Program.cs`. It will run at application startup and populate:
- **Identity Roles and Accounts**
- **Categories** (Yoga, Boxing, CrossFit, Cardio, Strength Training)
- **Plans** (Basic, Standard, Premium, Annual)
Plan and category data can be loaded from JSON seed files.

### Step 6: Run the Application

**In Visual Studio:** Press `F5` or click **Run**

The application will start using the configured ASP.NET Core development environment.

## 📁 Project Structure Details

```
GymManagementSystem/
├── GymManagementSystem.PL/          # Presentation Layer
│   ├── Controllers/                 # MVC Controllers
│   ├── Views/                       # Razor Views
│   ├── wwwroot/                     # Static files and attachments
│   └── Program.cs                   # App entry point
│
├── GymManagementSystem.BLL/         # Business Logic Layer
│   ├── Services/                    # Business logic services
│   ├── ViewModels/                  # View Models
│   ├── Mapping/                     # AutoMapper profiles
│   └── Validation/                  # Business validation
│
└── GymManagementSystem.DAL/         # Data Access Layer
    ├── Data/                        # DbContext
    ├── Entities/                    # Domain entities
    ├── Configurations/              # Entity configurations (Fluent API)
    ├── Interceptors/                # EF Core interceptors
    ├── Migrations/                  # Database migrations
    ├── Repositories/                # Data access implementations
    └── Seeder/                      # Database seeders
```
