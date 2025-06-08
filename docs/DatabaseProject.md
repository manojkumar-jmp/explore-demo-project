
### **Example: Database Project Content**

```
BookLibrary.Database/
├── Tables/
│   └── Book.sql
├── StoredProcedures/
│   └── usp_AddBook.sql
├── Seed/
│   └── SampleBooks.sql
├── Test/
│   └── testBook.sql          # tSQLt test example (optional)
├── README.md                 # Document usage, deployment, etc.

```

**Note:**  
- You can update scripts in this project as you evolve your EF models/migrations.
- Optionally, include tSQLt tests for your database objects if you want automated DB-level validation.
- **EF Migrations** can also export SQL to this project for source control.

---

### **How to Use This in the Project**

- **Development:**  
  - Develop normally using EF Code-First/Migrations.
- **Script Management:**  
  - After updating your model, use `Update-Database -Script` or `Script-Migration` to generate/update SQL scripts.
  - Save/update these scripts in the `BookLibrary.Database` project.
- **Testing:**  
  - Optionally add tSQLt tests for your database objects if you want automated DB-level validation.
- **Deployment:**  
  - Use these scripts for manual deployments, CI/CD pipelines, or sharing DB changes with the team.

---
