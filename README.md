# Gym Management System

## 📋 Project Overview

Gym Management System is a web-based gym management application built with **ASP.NET Core MVC** using a **3-Layer Architecture**.

The system provides features for managing members, trainers, memberships, training sessions, bookings, plans, categories, and gym operations.

**Dependency Flow:** PL → BLL → DAL

- **PL (Presentation Layer):** Handles HTTP requests, MVC controllers, Razor views, authentication, and authorization.
- **BLL (Business Logic Layer):** Contains business logic, services, validation, view models, and mapping.
- **DAL (Data Access Layer):** Handles data persistence using Entity Framework Core, SQL Server, repositories, Unit of Work, and database configurations.

## 🚀 Getting Started

### Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [Visual Studio](https://visualstudio.microsoft.com/) with ASP.NET and web development workload

### Step 1: Clone the Repository

```bash
git clone https://github.com/Bola-Edward/Gym-Management-System.git
cd Gym-Management-System
Step 2: Update Database Connection

Configure the SQL Server connection string in the application's configuration file.

The application uses Entity Framework Core with SQL Server for data persistence.

Step 3: Set Startup Project

In Visual Studio:

Right-click on GymManagementSystem.PL
Select Set as Startup Project
Make sure GymManagementSystem.PL is selected as the startup project
Step 4: Apply Database Migrations

The application automatically checks for pending Entity Framework Core migrations during startup and applies them to the database.

Existing migrations include the initial database schema and ASP.NET Core Identity tables.

If you need to create a new migration after changing the data model:

Add-Migration "MigrationName"
Update-Database
Step 5: Seed Initial Data

The application automatically seeds initial data when it starts.

The database seeding process includes:

Identity Roles and Accounts
Membership Plans
Session Categories

Plan and category data can be loaded from JSON seed files.

Step 6: Run the Application

In Visual Studio, press F5 or click Run.

The application will start using the configured ASP.NET Core development environment.

📁 Project Structure Details
GymManagementSystem/
│
├── GymManagementSystem.PL/              # Presentation Layer
│   ├── Controllers/                     # MVC Controllers
│   ├── Views/                           # Razor Views
│   ├── wwwroot/                         # CSS, JavaScript, images, attachments
│   └── Program.cs                       # Application entry point
│
├── GymManagementSystem.BLL/             # Business Logic Layer
│   ├── Services/                        # Business services
│   ├── ViewModels/                      # MVC View Models
│   ├── Mapping/                         # AutoMapper profiles
│   ├── Validation/                      # Business validation
│   └── Attachments/                     # Attachment management
│
└── GymManagementSystem.DAL/             # Data Access Layer
    ├── Data/                            # DbContext
    ├── Entities/                        # Domain entities
    ├── Configurations/                  # EF Core Fluent API configurations
    ├── Repositories/                    # Repository implementations
    ├── Interceptors/                    # EF Core interceptors
    ├── Migrations/                      # EF Core migrations
    └── Seeders/                         # Database seeders

✨ Key Features
Member management with CRUD operations
Trainer management
Membership management and cancellation
Training session management
Session booking and attendance tracking
Membership plan management
Session category management
Gym dashboard with operational statistics
Member health record management
Member image and attachment management
Role-based authentication and authorization
ASP.NET Core Identity integration
Repository and Unit of Work patterns
Soft delete functionality
Automatic audit tracking
EF Core Fluent API configurations
Database constraints and filtered unique indexes
JSON-based database seeding
🔐 Authentication & Authorization

The application uses ASP.NET Core Identity with cookie-based authentication and role-based authorization.

Supported roles include:

SuperAdmin
Admin

Authentication is handled through the AccountController, which provides:

Login
Logout
Access denied handling
Return URL support

Authorization is applied to controllers and actions based on the user's assigned role.

🏋️ Main Application Areas
Members

Manage gym members and their information, including:

Personal information
Address
Health records
Profile images
Membership information
Trainers

Manage trainers and their professional information, including:

Personal information
Address
Specialty
Plans

Manage membership plans including:

Name
Duration
Price
Description
Active / inactive status

The application prevents deactivating plans that have active memberships.

Sessions

Create and manage training sessions with:

Description
Trainer
Category
Start and end dates
Capacity
Current booked members

Session capacity is validated when creating and managing sessions.

Bookings

Manage member bookings for training sessions.

The booking system supports:

Creating bookings
Viewing session rosters
Cancelling bookings
Tracking attendance
Memberships

Assign and manage memberships between members and plans.

Memberships include:

Member
Plan
Start date
End date
Active status
Dashboard

The dashboard provides gym operation statistics such as:

Total members
Active members
Total trainers
Upcoming sessions
Ongoing sessions
Completed sessions
🏗️ Architecture

The application follows a 3-Layer Architecture:

Presentation Layer (PL)

Responsible for the web application and user interaction.

It contains:

MVC Controllers
Razor Views
Authentication and authorization
Static assets
Request validation
User feedback through TempData
Business Logic Layer (BLL)

Contains the application's business logic and application services.

It contains services for:

Members
Trainers
Plans
Sessions
Bookings
Memberships
Dashboard

The BLL also handles validation, business rules, ViewModels, mapping, and attachment management.

Data Access Layer (DAL)

Responsible for persistence and database access.

It contains:

GymDbContext
Entity configurations
Repositories
Unit of Work
EF Core migrations
Database seeders
EF Core interceptors
🗄️ Data Access

The application uses Entity Framework Core with SQL Server.

The GymDbContext manages entities including:

Users
Members
Trainers
Plans
Categories
Sessions
Bookings
Memberships
Health Records

Entity relationships and constraints are configured using the EF Core Fluent API.

📦 Repository & Unit of Work

The project uses the Repository Pattern to abstract data access operations.

The generic repository provides common operations such as:

Add
Update
Delete
Get by ID
Query with related entities

Specialized repositories are used where domain-specific queries are required.

The Unit of Work coordinates repository operations through a shared GymDbContext and provides a centralized SaveChangesAsync() operation.

🗑️ Soft Delete

The application uses soft deletion instead of permanently removing certain records from the database.

Deleted records are marked using:

IsDeleted
DeletedAt

Global query filters prevent soft-deleted records from appearing in normal queries.

This allows deleted data to remain available when required while keeping it hidden from standard application operations.

🕒 Audit Tracking

An EF Core SaveChangesInterceptor automatically manages audit fields.

The interceptor updates:

CreatedAt
UpdatedAt
DeletedAt

This keeps audit information consistent without requiring every service to manually update these fields.

👤 Entity Design

The application uses a base entity structure and inheritance for users.

Members and trainers are derived from a common User entity using EF Core Table-Per-Hierarchy (TPH) mapping.

A discriminator is used to identify the user type.

The project also includes an Address value object containing:

Street
City
Building Number
🌱 Database Seeding

Initial application data is created automatically during application startup.

The seeding process includes:

Identity roles and default accounts
Membership plans
Session categories

Plan and category data are loaded from JSON files when the corresponding database tables are empty.

⚙️ Application Startup

During application startup, the application:

Registers the DAL and BLL services.
Configures Entity Framework Core and SQL Server.
Configures ASP.NET Core Identity.
Applies pending database migrations.
Seeds initial database data.
Configures authentication and authorization middleware.
Starts the MVC application.

The default MVC route is:

{controller=Home}/{action=Index}/{id?}
📁 Static Files & Attachments

Static assets are stored under:

wwwroot/

This includes:

CSS
JavaScript
Images
Member attachments

Member uploaded files are stored under:

wwwroot/Attachments/

Uploaded files use unique filenames to avoid naming conflicts.

🛠️ Technologies Used
ASP.NET Core MVC
.NET 10
C#
Entity Framework Core
SQL Server
ASP.NET Core Identity
AutoMapper
Bootstrap
jQuery
Razor Views
Git & GitHub
📌 Architecture Notes
3-Layer Architecture separates Presentation, Business Logic, and Data Access responsibilities.
Repository Pattern abstracts database access from the business layer.
Unit of Work coordinates database operations across repositories.
ASP.NET Core Identity provides authentication and role-based authorization.
EF Core Fluent API configures relationships, constraints, indexes, and query filters.
Soft Delete keeps deleted records out of normal queries without physically removing them.
Audit Interceptor automatically manages entity timestamps.
TPH Inheritance is used for the User, Member, and Trainer hierarchy.
Result Pattern is used to represent expected operation outcomes and business validation errors.
📄 License

This project was developed as a learning and portfolio project.
