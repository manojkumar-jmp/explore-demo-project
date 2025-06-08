# BookLibrary Demo Project: Architecture Overview & Testing Scope

---

## 1. Architecture Overview

A simple ASP.NET MVC (.NET Framework 4.8) application for managing a library of books. This project demonstrates clean layered architecture, separation of concerns, dependency injection, and testability, suitable for BDD (SpecFlow), UI automation (Selenium), and xUnit-based unit testing tutorials.

### **Solution Structure**

```
BookLibrary/
├── BookLibrary.Data/        # Data access (EF models, DbContext, Repository)
├── BookLibrary.Business/    # Business logic (Services, business rules)
├── BookLibrary.Web/         # ASP.NET MVC web UI (Controllers, Views)
└── BookLibrary.Tests/       # Test project (xUnit, SpecFlow, Selenium)
```

### **Layered Architecture**

#### **A. Data Layer (`BookLibrary.Data`)**
- **Entities:** Defines `Book` with properties (`Id`, `Title`, `Author`).
- **DbContext:** `LibraryContext` manages EF DB connection and `DbSet<Book>`.
- **Repository Pattern:** `IBookRepository` abstracts data access; `BookRepository` implements CRUD using `LibraryContext`.

#### **B. Business Layer (`BookLibrary.Business`)**
- **Services:** `IBookService` interface and `BookService` implementation.
- **Business Rules:** Encapsulates domain logic, e.g., **book titles cannot contain the word "Test"** (throws exception if violated).
- **Dependency:** Uses `IBookRepository` for data operations.

#### **C. Presentation Layer (`BookLibrary.Web`)**
- **Controllers:** e.g., `BooksController` depends on `IBookService` (not direct data access).
- **Views:** Razor views for listing, creating, editing, deleting books.
- **Error Handling:** Business rule violations are shown as model errors in the UI.

#### **D. Dependency Injection**
- **Unity Container:** Configured in `UnityConfig.cs` (Web project).
    - Maps interfaces to implementations:
        - `IBookRepository` → `BookRepository`
        - `IBookService` → `BookService`
        - Registers `LibraryContext`
- **Controller Construction:** Services injected via constructors, allowing for easy mocking and testing.

#### **E. Testing Layer (`BookLibrary.Tests`)**
- **xUnit:** For unit testing business, repository, and controller layers.
- **SpecFlow:** BDD scenarios for features like "Add Book", "List Books".
- **Selenium:** UI automation for browser-based tests, e.g., verifying business rules in the UI.

---

### **Key Architectural Benefits**

- **Separation of Concerns:** Data access, business logic, and UI are distinct, reducing coupling.
- **Testability:** All dependencies are injected; repositories and services can be mocked.
- **Maintainability:** Business rules are centralized in the business layer.
- **Reusability:** Business logic is decoupled from UI, so it can be reused in other apps (e.g., APIs).
- **Extensibility:** New features or rules can be added to the business layer without affecting other parts of the system.
- **BDD & Automation Ready:** Structure is ideal for SpecFlow (business scenarios) and Selenium (UI tests).

---

### **Example Flow: "Add Book" (with Business Rule)**

1. **User submits 'Add Book' form** in the UI.
2. **BooksController** receives the request, calls `IBookService.AddBook`.
3. **BookService** checks business rules (e.g., title doesn't contain "Test").
    - If invalid, throws exception.
    - If valid, calls `IBookRepository.Add` and `Save`.
4. **BookRepository** persists the book using `LibraryContext`.
5. **If error**, message is displayed in UI; **if success**, user is redirected to book list.

---

## 2. Scope for Unit Test (xUnit), SpecFlow (BDD), and UI Testing

This project is designed so you can demonstrate and teach all major test levels in a modern .NET Framework solution using **xUnit**.

---

### **A. Unit Testing Scope (xUnit)**

**Where?**  
- `BookLibrary.Tests` project.

**What to Test?**
- **Business Layer:** Test business rules in `BookService` (e.g., prevent "Test" in book title).
- **Repository Layer:** (optional, with in-memory DB or mocking).
- **Controller Logic:** Test controller actions using mocks for `IBookService`.
- **Validation:** Edge cases (nulls, invalid data).

**Why?**
- Fast feedback.
- Pinpoint bugs in isolated units (no DB or UI required).
- Teaches how to use Moq or similar libraries for dependency mocking.
---

### **B. SpecFlow (BDD) Testing Scope**

**Where?**  
- `BookLibrary.Tests` project (with SpecFlow NuGet).

**What to Test?**
- **Business Scenarios:** End-user stories, e.g., "As a librarian, I want to add a book so that it appears in the catalog."
- **Integration:** End-to-end scenarios, e.g., adding a book and verifying it appears in the list.
- **Negative Cases:** Try adding a book with "Test" in title and check for error.

**Why?**
- Closes the gap between requirements and implementation.
- Living documentation for business logic.
- Can drive development (TDD/BDD).

---

### **C. UI (Selenium) Testing Scope**

**Where?**  
- `BookLibrary.Tests` (UI test folder) or a dedicated project like `BookLibrary.UI.Tests`.

**What to Test?**
- **UI Flows:** Add, edit, delete book via the browser.
- **Validation Messages:** Confirm business rules/errors appear in UI.
- **Cross-browser:** Optionally, Chrome, Firefox, Edge, etc.

**Why?**
- Ensures entire stack works together.
- Catches regression and integration bugs.
- Mimics real user behavior.

---

### **D. How the Layers Interact in Testing**

| Test Level     | Layer Under Test     | Dependencies         | Tools/Libraries              |
|----------------|----------------------|----------------------|------------------------------|
| Unit Test      | Business, Controller | Mocked Repositories  | xUnit, Moq                   |
| BDD (SpecFlow) | Full Stack           | Real DB/Test DB      | SpecFlow, xUnit              |
| UI Test        | Full Stack + UI      | Real DB, Browser     | Selenium WebDriver, xUnit    |

---
