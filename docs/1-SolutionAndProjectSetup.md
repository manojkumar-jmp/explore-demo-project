## Solution & Project Setup

### 1. Create the Solution
- In Visual Studio, create a new Blank Solution named BookLibrary.

### 2. Add Core Projects

- BookLibrary.Data (Class Library)
  - For EF entities, DbContext, repositories.
- BookLibrary.Business (Class Library)
  - For service interfaces and business logic.
- BookLibrary.Web (ASP.NET MVC Web Application)
  - For UI (controllers, views, DI config).
- BookLibrary.Tests (xUnit Test Project)
  - For unit, BDD, and UI tests.
- BookLibrary.Database (SQL Server Database Project)
  - For SQL scripts, optional tSQLt tests.

#### Go to your VS2022 installer for Individual Components and select:

Net Framework project and item templates

> Enables .NET Framework project templates, item templates & related features for .NET Framework development.

![image](https://github.com/user-attachments/assets/e65816e7-d88b-4834-951e-7f3b1ff4d28d)
