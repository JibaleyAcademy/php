# PHP Best Practices: PSR-12, Variable Naming, Function Naming, SOLID, and Laravel Style Guide

## Table of Contents
- [PSR Standards](#psr-standards)
  - [PSR-12: Extended Coding Style Guide](#psr-12-extended-coding-style-guide)
- [Naming Conventions](#naming-conventions)
  - [Variable Naming](#variable-naming)
  - [Function Naming](#function-naming)
- [SOLID Principles](#solid-principles)
  - [Single Responsibility Principle](#single-responsibility-principle)
  - [Open/Closed Principle](#openclosed-principle)
  - [Liskov Substitution Principle](#liskov-substitution-principle)
  - [Interface Segregation Principle](#interface-segregation-principle)
  - [Dependency Inversion Principle](#dependency-inversion-principle)
- [Laravel Style Guide](#laravel-style-guide)
  - [Controllers](#controllers)
  - [Models](#models)
  - [Views](#views)
  - [Validation](#validation)
  - [Routing](#routing)
- [General Best Practices](#general-best-practices)
- [References and Documentation](#references-and-documentation)

---

## PSR Standards

### PSR-12: Extended Coding Style Guide
- PSR-12 builds upon PSR-1 and PSR-2 to provide a detailed coding standard for PHP.
- Key highlights:
  - Lines must not exceed 120 characters; soft limit of 80 characters is recommended.
  - Use `declare(strict_types=1);` at the beginning of each file when applicable.
  - Visibility must be declared on all properties and methods (e.g., `public`, `protected`, `private`).
  - Use `null` coalescing operator (`??`) where appropriate.
  - Multi-line arguments and arrays must have a trailing comma.

Reference: [PSR-12 Specification](https://www.php-fig.org/psr/psr-12/)

---

## Naming Conventions

### Variable Naming
- Use descriptive and meaningful names in `camelCase` format.
  - Example:
    ```php
    $userName = 'John Doe';
    $orderTotal = 150.75;
    ```
- Avoid using single-letter variable names except for loop counters.
- Prefix boolean variables with `is` or `has` for clarity.
  - Example:
    ```php
    $isActive = true;
    $hasAccess = false;
    ```

### Function Naming
- Use descriptive names in `camelCase` format for functions.
  - Example:
    ```php
    function calculateTotal($items) {
        // Logic here
    }
    ```
- Keep function names short but descriptive, focusing on what the function does.
- Use verbs for function names to indicate actions (e.g., `get`, `calculate`, `create`).

---

## SOLID Principles

### Single Responsibility Principle
- A class should have one and only one reason to change.
  - Example:
    ```php
    class InvoiceGenerator {
        public function generate() {
            // Logic for generating invoices
        }
    }
    ```

### Open/Closed Principle
- Classes should be open for extension but closed for modification.
  - Use abstract classes or interfaces for extensibility.

### Liskov Substitution Principle
- Subclasses must be substitutable for their base classes without altering the program.
  - Example:
    ```php
    interface Payment {
        public function process();
    }

    class CreditCardPayment implements Payment {
        public function process() {
            // Logic for credit card payment
        }
    }
    ```

### Interface Segregation Principle
- Prefer many small, specific interfaces over a single large one.
  - Example:
    ```php
    interface Logger {
        public function log(string $message);
    }

    interface FileLogger extends Logger {
        public function setPath(string $path);
    }
    ```

### Dependency Inversion Principle
- High-level modules should not depend on low-level modules but on abstractions.
  - Use dependency injection to manage dependencies.

---

## Laravel Style Guide

### Controllers
- Keep controllers thin; move complex logic to services or helper classes.
  - Example:
    ```php
    class UserController extends Controller {
        public function store(Request $request, UserService $userService) {
            $userService->create($request->all());
        }
    }
    ```

### Models
- Use Eloquent accessors and mutators for data transformation.
  - Example:
    ```php
    class User extends Model {
        public function getFullNameAttribute() {
            return "$this->first_name $this->last_name";
        }
    }
    ```

### Views
- Use Blade templates and avoid embedding business logic in views.
  - Example:
    ```blade
    <h1>{{ $user->full_name }}</h1>
    ```

### Validation
- Use Laravel's validation rules and `FormRequest` classes for request validation.
  - Example:
    ```php
    public function store(UserRequest $request) {
        // Validation happens automatically in UserRequest
    }
    ```

### Routing
- Use route grouping and middlewares for clean and manageable routes.
  - Example:
    ```php
    Route::middleware(['auth'])->group(function () {
        Route::resource('users', UserController::class);
    });
    ```

---

### Roadmap

[https://laraveldaily.com/roadmap-learning-path](https://laraveldaily.com/roadmap-learning-path)

### Open Source Project

[https://laraveldaily.com/code-examples/projects](https://laraveldaily.com/code-examples/projects)

## General Best Practices
- **Avoid Hardcoding:** Use `.env` files for configuration.
- **Security First:** Sanitize inputs and use Laravel's built-in security features.
- **Unit Testing:** Write tests to ensure code reliability.
- **Version Control:** Commit often with clear messages.
- **Documentation:** Maintain clear comments and API documentation.

---

## References and Documentation
- [PSR-12 Specification](https://www.php-fig.org/psr/psr-12/)
- [Laravel Documentation](https://laravel.com/docs)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [PHP The Right Way](https://phptherightway.com/)
- [PHP Official Manual](https://www.php.net/manual/en/)
