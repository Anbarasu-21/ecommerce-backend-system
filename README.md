# E-Commerce Backend System

A production-ready RESTful Web API built using **Spring Boot 3**, **Spring Security**, and **JWT (JSON Web Tokens)** featuring Role-Based Access Control (RBAC). 

This project simulates an online shopping platform containing authentication, product catalogs, categories, shopping carts, transactional checkouts with stock verification, and automatic inventory management.

---

## 🛠️ Tech Stack & Dependencies
* **Language:** Java 17
* **Framework:** Spring Boot 3.2.5 (Spring MVC, Spring Data JPA, Spring Security)
* **Database:** H2 In-Memory Database (configured for rapid development/testing)
* **Token-based Security:** JSON Web Token (JJWT 0.11.5)
* **API Documentation:** SpringDoc OpenAPI / Swagger UI
* **Other Tools:** Lombok (boilerplate reduction), BCrypt (password hashing)

---

## 🚀 Key Features

### 🔒 1. Authentication & Security
* Secure user registration and login endpoints.
* Password hashing using **BCrypt Password Encoder**.
* Stateless token-based security via **JWT**.
* Custom filter (`JwtAuthFilter`) to intercept, decode, and validate requests.
* **Role-Based Access Control (RBAC):** Dedicated permissions for `CUSTOMER` and `ADMIN` roles.

### 📦 2. Product & Category Management
* Full CRUD endpoints for categories and products (Admin only).
* Public endpoints to view and search the product catalog (accessible without login).
* Built-in server-side **Pagination**, **Sorting**, and **Keyword Searching**.

### 🛒 3. Shopping Cart Module
* Interactive cart operations: Add products to cart, update quantity, and remove items.
* Performs real-time inventory checks during cart additions.

### 💳 4. Order & Inventory Management
* **Transactional Checkout:** Placing an order aggregates cart items, calculates total price, and clears the user's cart in a safe, single transaction (`@Transactional`).
* **Auto Stock Reduction:** Verifies stock levels prior to checkout and automatically decrements inventory.
* Centralized exception handling to prevent double ordering or checking out out-of-stock items.

---

## 📊 Database Schema (ERD Model)

The database includes the following key tables:
1. **users** (`id`, `name`, `email`, `password`, `role`)
2. **categories** (`id`, `name`, `description`)
3. **products** (`id`, `name`, `description`, `price`, `quantity`, `category_id`)
4. **cart** (`id`, `user_id`, `product_id`, `quantity`)
5. **orders** (`id`, `user_id`, `total_amount`, `status`, `order_date`)
6. **order_items** (`id`, `order_id`, `product_id`, `quantity`, `price`)

---

## ⚙️ How to Run Locally

### Prerequisites
* Java JDK 17 or higher
* Maven (optional, or use IDE tools)

### Steps
1. Open the project in your IDE (IntelliJ IDEA, Eclipse, etc.).
2. Let the IDE download the Maven dependencies automatically.
3. Run the main class: `src/main/java/com/ecommerce/EcommerceApplication.java`.
4. The server will start on port `8080`.

---

## 🧪 Testing the APIs

### 1. Interactive Swagger Documentation
Open the following link in your browser to view and test all REST endpoints:
👉 **[http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)**

### 2. Seeded Test Accounts
On startup, a data initializer automatically seeds the database with the following accounts:
* **Admin Account:** `admin@ecommerce.com` / Password: `admin123`
* **Customer Account:** `customer@ecommerce.com` / Password: `customer123`

### 3. How to Authenticate in Swagger
1. Find the `POST /api/auth/login` endpoint.
2. Enter the login credentials (admin or customer) and execute the request.
3. Copy the returned `"token"` string.
4. Click the **Authorize** button at the top right of the Swagger UI page.
5. Enter: `Bearer <your_copied_token>` and click Authorize.
6. Now you can make authorized requests to restricted endpoints!

### 4. Database Console (H2)
To inspect the physical tables and run database queries:
* **H2 Console URL:** **[http://localhost:8080/h2-console](http://localhost:8080/h2-console)**
* **JDBC URL:** `jdbc:h2:mem:ecommerce_db`
* **User Name:** `sa`
* **Password:** *(leave blank)*
