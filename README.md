# 🧪 DummyJSON API Test Suite

This repository contains a comprehensive suite of automated tests for the [**DummyJSON API**](https://dummyjson.com/), utilizing [Postman](https://www.postman.com/) and [Newman](https://github.com/postmanlabs/newman). The tests cover various API functionalities to ensure reliability and performance.

## 📖 Table of Contents

- [Overview](#overview)
- [Collection Structure](#collection-structure)
- [Environment Setup](#environment-setup)
- [Running Tests Locally](#running-tests-locally)
- [Data-Driven Testing](#data-driven-testing)
- [CI/CD Integration](#cicd-integration)
- [Test Reports](#test-reports)
- [Resources](#resources)

## 📄 <a id="overview">Overview</a>

The test suite is organized into distinct folders within the Postman collection, each targeting specific API functionalities:

- **API Docs\Auth**: Covers login and token management.
- **Happy Path**: Expected behaviors for:
  - **Product Lifecycle**: Create, update, get, sort, and delete products.
  - **User Management**: Get, search, filter, and delete users.
  - **Cart Workflow**: Create/view/delete carts by `userId` or `cartId`.
  - **Posts and Comments**: CRUD workflows for posts and comments.
- **Negative**: Test invalid inputs and edge cases for:
  - **Auth**
  - **Product Lifecycle**
  - **User Management**
  - **Cart Workflow**
  - **Posts and Comments**

## 📁 <a id="collection-structure">Collection Structure</a>

### 🔐 Auth

- `POST /auth/login`: User login and token handling

### 🛒 Cart Workflow

- `GET /users`: Retrieve user list
- `GET /products`: Get list of products
- `POST /products/add`: Add a new product
- `PUT /products/:productId`: Update a product
- `GET /products/:productId`: Get product details
- `GET /products?sortBy=title&order=desc`: Sort products
- `GET /products/categories`: List categories
- `DELETE /products/:productId`: Delete a product

### 👤 User Management

- `POST /user/login`: Authenticate a user
- `GET /users/search?q=John`: Search users
- `GET /users/filter?key=hair.color&value=Black`: Filter users
- `GET /users/:userId/posts`: User's posts
- `GET /users/:userId/todos`: User's to-dos
- `DELETE /users/:userId`: Delete user
- `PUT /users/:userId`: Update user

### 📝 Posts & Comments

- `GET /posts`: Get all posts
- `GET /comments`: Get all comments
- `GET /posts/:postId/comments`: Get post's comments
- `GET /posts?sortBy=id&order=asc`: Sort posts
- `GET /posts/user/:userId`: User's posts

## ⚙️ <a id="environment-setup">Environment Setup</a>

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) (v18+)
- [Newman](https://github.com/postmanlabs/newman)
- [Newman HTML Reporter](https://github.com/postmanlabs/newman-reporter-html)

Install globally:

```bash
npm install -g newman newman-reporter-html
```

## 🧪 <a id="running-tests-locally">Running Tests Locally</a>

Clone this repository and navigate into the directory:

```bash
git clone https://github.com/Bozhidar100/PostmanProject
cd PostmanProject
```

Run the entire collection:

```bash
newman run Projetct.postman_collection.json   --environment PostmanGroupProject.postman_environment.json   --reporters cli,junit,html   --reporter-junit-export results.xml   --reporter-html-export report.html
```

## 📊 <a id="data-driven-testing">Data-Driven Testing</a>

Data files can be used to iterate over multiple test inputs.

Examples:

- **Cart Workflow** → `TestingData/products.json`
- **Authentication** → `TestingData/user-logins.json`

Run Authentication Validation:

```bash
newman run Projetct.postman_collection.json   --folder "Auth"   -d TestingData/user-logins.json   --reporters cli,jinit,html   --reporter-junit-export results.xml   --reporter-html-export report.html
```

Run Cart Workflow:

```bash
newman run Projetct.postman_collection.json   --folder "Cart Workflow"   -d TestingData/products.json   --reporters cli,jinit,html   --reporter-junit-export results.xml   --reporter-html-export report.html
```

## 🚀 <a id="cicd-integration">CI/CD Integration</a>

GitHub Actions runs tests automatically on:

- Push to `main`
- Pull requests
- Scheduled runs

Workflow: `.github/workflows/postman-tests.yml`

It includes:

- Whole collection tests
- Data-driven folder tests
- HTML report generation and artifact upload

## 📈 <a id="test-reports">Test Reports</a>

Reports are saved in and uploaded as CI artifacts.

They include:

- Passed/failed tests
- Response times
- Request/response logs

## 📚 <a id="resources">Resources</a>

- [Postman Documentation](https://learning.postman.com/)
- [Newman CLI Docs](https://www.npmjs.com/package/newman)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
