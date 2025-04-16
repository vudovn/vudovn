# ASM React Shopping API

This is a RESTful API for an e-commerce application built with Node.js, Express, and MySQL.

## Setup

1. Clone the repository
2. Install dependencies:
   ```
   npm install
   ```
3. Configure the environment variables in `.env` file:
   ```
   DB_HOST=localhost
   DB_USER=root
   DB_PASS=
   DB_NAME=ass_react
   DB_DIALECT=mysql
   ```
4. Import the `asm_react.sql` file to your MySQL server
5. Start the server:
   ```
   node server.js
   ```

## API Endpoints

### Categories

- `GET /api/categories` - Get all categories
- `GET /api/categories/:id` - Get category by ID
- `POST /api/categories` - Create new category
- `PUT /api/categories/:id` - Update category
- `DELETE /api/categories/:id` - Delete category

### Products

- `GET /api/products` - Get all products
- `GET /api/products/:id` - Get product by ID
- `GET /api/categories/:categoryId/products` - Get products by category
- `POST /api/products` - Create new product
- `PUT /api/products/:id` - Update product
- `DELETE /api/products/:id` - Delete product

### Users

- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `POST /api/users` - Create new user
- `POST /api/login` - User login
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user

### Orders

- `GET /api/orders` - Get all orders
- `GET /api/orders/:id` - Get order by ID
- `GET /api/users/:userId/orders` - Get user orders
- `POST /api/orders` - Create new order
- `PUT /api/orders/:id` - Update order
- `DELETE /api/orders/:id` - Delete order

### Comments

- `GET /api/comments` - Get all comments
- `GET /api/comments/:id` - Get comment by ID
- `GET /api/products/:productId/comments` - Get comments by product
- `POST /api/comments` - Create new comment
- `PUT /api/comments/:id` - Update comment
- `DELETE /api/comments/:id` - Delete comment

## Data Models

### User

```json
{
  "id": 1,
  "username": "johndoe",
  "password": "hashed_password",
  "email": "john@example.com",
  "name": "John Doe",
  "phone": "1234567890",
  "avatar": "avatar.jpg",
  "status": 1,
  "role": 0
}
```

### Category

```json
{
  "id": 1,
  "name": "Vegetables",
  "status": 1
}
```

### Product

```json
{
  "id": 1,
  "name": "Fresh Carrots",
  "image": "carrots.jpg",
  "description": "Fresh organic carrots",
  "price": 20000,
  "discount_price": 18000,
  "quantity": 100,
  "is_featured": 1,
  "view": 0,
  "status": 1,
  "category_id": 1
}
```

### Order

```json
{
  "id": 1,
  "name": "John Doe",
  "phone": "1234567890",
  "payments": 1,
  "payment_status": 1,
  "order_status": 1,
  "user_id": 1,
  "items": [
    {
      "product_id": 1,
      "quantity": 2,
      "price": 20000
    }
  ]
}
```

### Comment

```json
{
  "id": 1,
  "content": "Great product!",
  "date": "2025-04-15T10:00:00",
  "status": 1,
  "product_id": 1,
  "user_id": 1
}
```
