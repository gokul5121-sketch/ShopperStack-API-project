# ShopperStack-API-Testing
End-to-end REST API test suite for the ShopperStack e-commerce platform, built using Postman and Newman with dynamic chaining, JWT authentication, and full CRUD coverage.

## Project Overview

ShopperStack is an e-commerce application that allows shoppers to browse products, manage carts, save wishlists, handle delivery addresses, and place orders.
This project contains a complete API testing suite that validates the entire shopper journey from login to order placement using Postman collections with automated test scripts.

## Tech Stack

| Tool | Purpose |
|------|---------|
| Postman | API testing & collection management |
| Newman | Command-line collection runner |
| JavaScript | Writing pm.test() assertions |
| Environment Variables | Dynamic token & ID chaining |

## Modules Tested

| # | Module | Endpoints | Methods |
|---|--------|-----------|---------|
| 1 | Profile (Login) | `/users/login` | POST |
| 2 | Product View | `/products`, `/products/alpha` | GET |
| 3 | Cart | `/shoppers/{userId}/carts` | POST, GET, PUT, DELETE |
| 4 | WishList | `/shoppers/{userId}/wishlist` | POST, GET, DELETE |
| 5 | Address | `/shoppers/{userId}/address` | POST, GET, PUT, DELETE |
| 6 | Order | `/shoppers/{userId}/orders` | POST, GET, PATCH |

Total: 17 API endpoints | ~50 test assertions

## Test Coverage

Each request includes the following assertions:

- Status code validation (200, 201, 204)
- Response time validation using threshold-based assertions
- Status message validation ("OK", "Created", "No Content")

### Key Automation Features

- JWT Token Chaining — Token extracted from Login and automatically applied to all authenticated requests
- Dynamic Variable Passing — `userId`, `productId`, `itemId`, `addID`, `orderID` are captured from responses and chained into subsequent requests
- Full CRUD Flows — Cart, WishList, and Address all cover Create → Read → Update → Delete

## How to Run
### Option 1: Postman (UI)

1. Download and install [Postman](https://www.postman.com/downloads/)
2. Import the collection:
   - Click Import → select `collection/SS_final_postman_collection.json`
3. Import the environment:
   - Click Import → select `environment/ShopperStack_env.json`
4. Set the environment as active
5. Run the collection using Collection Runner

### Option 2: Newman (Command Line)

Install Newman:
```bash
npm install -g newman
```

Run the collection:
```bash
newman run collection/SS_final_postman_collection.json \
  -e environment/ShopperStack_env.json
```

Run with HTML report:
```bash
npm install -g newman-reporter-htmlextra

newman run collection/SS_final_postman_collection.json \
  -e environment/ShopperStack_env.json \
  -r htmlextra \
  --reporter-htmlextra-export reports/newman-report.html
```

Then open `reports/newman-report.html` in your browser to view the full test report.

---
## Environment Variables

| Variable | Description | Set By |
|----------|-------------|--------|
| `S_url` | Base URL of ShopperStack API | Manually |
| `Btoken` | JWT Bearer token | Auto — Login response |
| `userId` | Logged-in user ID | Auto — Login response |
| `zoneId` | Delivery zone ID | Auto — Login response |
| `productId` | Selected product ID | Auto — HomePage response |
| `itemId` | Cart item ID | Auto — addToCart response |
| `addID` | Address ID | Auto — addAddress response |
| `orderID` | Order ID | Auto — Order response |

---


## Author
Gokul 
- 📧 gokulb.cs2001@gmail.com
- 🔗 LinkedIn (https://www.linkedin.com/in/gokul-ln/) 
- 🐙 GitHub  (https://github.com/gokul5121)
