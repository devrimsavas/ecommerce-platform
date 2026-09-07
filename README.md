# SnapShop — E-Commerce Platform

A full-stack e-commerce application simulating admin, registered user, and guest roles, built as two separate Express/EJS applications: a backend API with an embedded storefront, and a dedicated admin panel frontend.

## ⚠️ Setup Note

To ensure the Admin Panel works correctly, the JWT token secret must be configured **identically in both** the `BACK-END` and `FRONT-END` `.env` files. Generate one with Node's crypto module:

```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

Requires **Node.js v20.10.0** or higher (`node --version` to check).

## 🚀 Features

- **Role-based access**: Admin, registered user, and guest, each with different permissions
- **Admin capabilities**: add, update, and delete products, brands, and categories; manage users; update order status
- **Product catalog**: products organized by brand and category, with search
- **Shopping cart & orders**: cart items, order creation, and order-item tracking
- **Authentication**: JWT-based, with `bcrypt` password hashing
- **API documentation**: auto-generated Swagger docs (`swagger-autogen`), served at `/doc`
- **Automated tests**: Jest + Supertest covering login and product/category flows

## 🛠 Tech Stack

**Backend:** Node.js, Express, EJS, Sequelize (ORM), MySQL, JWT, bcrypt, Swagger (swagger-autogen + swagger-ui-express), Jest + Supertest
**Frontend (Admin Panel):** Node.js, Express, EJS, Axios (consumes the backend API), JWT

## 📂 Folder Structure

The repository is split into three top-level sections:

```
ecommerce-platform/
├── BACK-END/           # API + embedded storefront (port 3000)
│   ├── controllers/     # Brand, Cart, Category, Order, Product, Search, User
│   ├── models/          # Sequelize models: Product, Cart, CartItem, Order, OrderItem, Brand, Category, User, MembershipStatus
│   ├── routes/          # admin, auth, brand, cart, category, guest, order, products, registeredUsers, search, user
│   ├── middlewares/      # Auth (JWT verification, role-based authorize)
│   ├── tests/            # login.test.js, product_category.test.js
│   └── views/             # Embedded EJS storefront views
├── FRONT-END/            # Standalone Admin Panel (port 5000)
│   ├── views/              # adminPanel, adminlogin, allusers, brands, categories, orders
│   └── routes/             # admin, index
└── DOCUMENTATION/        # Reflection report and project notes
```

### 1. BACK-END
Serves the Admin, User, and Guest APIs. Also includes its own embedded front-end views for direct use without the separate Admin Panel. API documentation is available via Swagger at `http://localhost:3000/doc`. Requires CORS to be enabled for cross-origin requests from the Admin Panel.

### 2. FRONT-END
A standalone Admin Panel application that consumes the backend API via Axios. **Cannot run independently** — the backend must be running in the background. Runs on port 5000.

### 3. DOCUMENTATION
Contains the project's reflection report, database design notes, challenges encountered during development, and personal notes from the development process.

## ▶️ Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/devrimsavas/ecommerce-platform.git
   cd ecommerce-platform
   ```
2. **Install dependencies in both folders**
   ```bash
   cd BACK-END && npm install
   cd ../FRONT-END && npm install
   ```
3. **Configure environment variables** — set up `.env` in both `BACK-END` and `FRONT-END` with the **same JWT token secret** (see Setup Note above), plus MySQL connection details in the backend
4. **Run the backend** (from `BACK-END/`)
   ```bash
   npm start
   ```
5. **Run the frontend** (from `FRONT-END/`, in a separate terminal)
   ```bash
   npm start
   ```
6. **Explore the API** at `http://localhost:3000/doc` (Swagger UI)

## 🧪 Testing

```bash
cd BACK-END
npm test
```
Runs the Jest + Supertest suite covering authentication and product/category endpoints.

## 📚 References

Resources used during development are documented in detail in the reflection report (`DOCUMENTATION/Reflection_Report.pdf`), including:

1. Backend by Noroff — "Database Module Introduction" (YouTube)
2. ChatGPT (OpenAI) — assistance with database modeling and idea generation
3. Codeium — code enhancement and error resolution
4. LinkedIn Learning — "Programming Foundations: Databases" by Simon Allardice
5. Noroff Learning Resources
6. Udemy — "Node.js, Express, MongoDB Bootcamp" by Jonas Schmedtmann
7. Vertabelo Blog — "ER Diagram for Online Shop"
