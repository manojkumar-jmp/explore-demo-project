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
