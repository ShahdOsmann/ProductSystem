# ASP.NETCore3LayerProductSystem

🏢 ProductSystem

🔷 **ASP.NET Core MVC – 3-Layer Architecture (Repository + Unit Of Work) (.NET 9)**

---

## 📌 Project Overview

**ProductSystem** is a structured ASP.NET Core MVC application built using a professional multi-layered architecture.

The goal of this project is to demonstrate:
- ✅ Clean 3-Layer Architecture
- ✅ Email Confirmation
- ✅ JWT Authentication
- ✅ Password Recovery
- ✅ Repository Pattern
- ✅ Generic Repository
- ✅ Unit of Work Pattern
- ✅ Dependency Injection (DI)
- ✅ Separation of Concerns (SoC)
- ✅ ViewModel Pattern
- ✅ Entity Framework Core
- ✅ Fluent API Configuration
- ✅ Uploading Images
- ✅ Data Seeding
- ✅ Audit Logging

This architecture is scalable and suitable for enterprise-level business systems.

---

## 🏗 Architecture Overview

```
ProductSystem
│
├── ProductSystem.MVC   → Presentation Layer
├── ProductSystem.BLL   → Business Logic Layer
└── ProductSystem.DAL   → Data Access Layer
```

### 🔁 Application Flow

```
Client Request
      ↓
Controller (MVC)
      ↓
Manager (BLL)
      ↓
UnitOfWork (DAL)
      ↓
Repository (DAL)
      ↓
DbContext (EF Core)
      ↓
SQL Server
```

Each layer has a clear and strict responsibility.

---

## 🧩 Layers Explained

### 1️⃣ Presentation Layer – ProductSystem.MVC

**Contains:**

* Controllers
* Razor Views

**Responsibilities:**

* Handle HTTP Requests
* Perform Model Validation
* Call Business Layer
* Return Views

**Important Rules:**
❌ No direct DbContext usage
❌ No business logic
❌ No database queries

Controllers depend ONLY on BLL interfaces.
 
---

### 2️⃣ Business Logic Layer – ProductSystem.BLL

**Contains:**

* Managers
* ViewModels
* Mapping Logic (Domain ↔ ViewModel)

**Responsibilities:**

* Business rules implementation
* Data transformation
* Transaction control through UnitOfWork
* Keep Controllers thin

**Why Managers?**
Managers act as an abstraction over data access. They protect the Presentation Layer from database details.
 
---

### 3️⃣ Data Access Layer – ProductSystem.DAL

**Contains:**

* Entities (Domain Models)
* DbContext
* Generic Repository
* Specific Repositories
* UnitOfWork
* Entity Configurations
* Seeding
* Audit Logic

**Responsibilities:**

* Communicate with database
* Execute queries
* Track changes
* Save data

---

## 🛠 Design Patterns Used

✅ **Repository Pattern**

* Abstracts database logic from business logic
* Interfaces: `IGenericRepository<T>`, `IProductRepository`, `ICategoryRepository`
* Prevents direct DbContext usage outside DAL

✅ **Generic Repository**

* Prevents duplicated CRUD code
* Implemented Methods: `GetAll()`, `GetById(int id)`, `Add(T entity)`, `Delete(T entity)`
* Reusable across all entities

✅ **Unit Of Work Pattern**

* Coordinates multiple repositories using a single DbContext instance

 
**Benefits:**

* Single transaction boundary
* Centralized SaveChanges()
* Cleaner architecture
* Better scalability

✅ **Dependency Injection**

* Services are registered using extension methods

**DAL Registration**

```csharp
services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(connectionString));

services.AddScoped<IProductRepository, ProductRepository>();
services.AddScoped<ICategoryRepository, CategoryRepository>();
services.AddScoped<IUnitOfWork, UnitOfWork>();
```

**BLL Registration**

```csharp
services.AddScoped<ICategoryManager, CategoryManager>();
services.AddScoped<IProductManager, ProductManager>();
```

Ensures loose coupling and testability.

---

## 🗄 Database Layer

**Database Provider:** SQL Server
**ORM:** Entity Framework Core

### 📦 Entities

**Category** 

Relationship: One Category → Many Products

**Product**
 

Relationship: Many Products → One Category

---

## 🔎 Audit Logging

Implemented inside `AppDbContext`:
 

All auditable entities implement:

```csharp
public interface IAuditableEntity
{
    DateTime CreatedAt { get; set; }
    DateTime? UpdatedAt { get; set; }
}
```

---

## 🌱 Data Seeding

Seeded inside `OnModelCreating()`:

* Default Categories
* Default Products

Useful for:

* Development
* Testing
* Demonstration

---

## 📌 Features

**Category Module**

* View All Categories
* View Category Details
* Create Category
* Edit Category
* Delete Category

**Product Module**

* View All Products
* View Product Details
* Create Product
* Assign Product to Category

**Authentication Features**

* Email Confirmation on Sign-Up
* JWT-based Authentication
* Forgot Password / Password Recovery

---

## 🚀 How To Run

1️⃣ **Configure Connection String** in `appsettings.json`:

```json
"ConnectionStrings": {
  "ProductSystem": "Server=.;Database=ProductSystemDB;Trusted_Connection=True;"
}
```

2️⃣ **Apply Migrations**

```bash
Add-Migration InitialCreate
Update-Database
```

3️⃣ **Run Application**

```bash
dotnet run
```

or press F5 in Visual Studio.

---

## 🧠 Architectural Principles Applied

* Separation of Concerns (SoC)
* Dependency Inversion Principle (DIP)
* Single Responsibility Principle (SRP)
* DRY Principle
* Layered Architecture
* Loose Coupling
* Clean Code Structure

---

## 🧪 Testing Strategy (Future)

* Mock `IUnitOfWork`
* Test Managers independently
* Use InMemory Database for integration tests

---

## 🏆 Project Level Assessment

This project demonstrates:

* Solid understanding of ASP.NET Core
* Clean architecture thinking
* Proper pattern usage
* Enterprise-ready structure
 
---

## 👨‍💻 Author

**Shahd Osman**
Software Engineer
