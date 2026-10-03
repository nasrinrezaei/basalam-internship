# Basalam Internship — Shopping Cart & Checkout

A mobile-first shopping cart and checkout flow built with **Vue.js 2** as part of an internship project for **Basalam**.

The project focuses on implementing a marketplace-style shopping experience where products are grouped by vendor and users can manage their cart, select a delivery address, and proceed to a payment screen.

---

## 📌 Project Overview

This project is a frontend implementation of a multi-vendor shopping and checkout flow inspired by the Basalam marketplace.

The application covers the following flow:

```text
Shopping Cart
     ↓
Vendor & Product Management
     ↓
Address Selection
     ↓
Payment
```

The cart data is fetched from an external API using **Axios**, while application-level state is managed with **Vuex**.

The interface is designed primarily for a **360px mobile viewport** and supports Persian/RTL content.

---

## ✨ Features

### 🛒 Shopping Cart

- Fetch cart data from an external API
- Display products grouped by vendor
- Display vendor information
- Display product image, price, quantity and stock
- Increase/decrease product quantity
- Remove products from the cart
- Prevent increasing quantity beyond available stock
- Calculate product totals
- Calculate vendor totals
- Calculate the overall cart total

### 🚚 Free Shipping

The checkout UI includes a free-shipping progress indicator for each vendor.

When the vendor's cart value reaches the configured threshold, the user is notified that shipping is free.

### 📍 Address Selection

- Display available addresses
- Select a delivery address
- Store the selected address through Vuex

### 💳 Payment

The payment screen includes:

- Order summary
- Vendor-level order breakdown
- Product-level order breakdown
- Discount code input
- Account credit option
- Payment gateway selection

Available payment gateway options are currently represented as frontend data.

> **Note:** Payment processing itself is not connected to a real payment gateway in this version.

### 🔄 Loading & Error Handling

The application provides:

- Loading state while fetching cart data
- Error state when the API request fails
- Retry functionality

---

## 🏗 Architecture

The project follows a component-based architecture using Vue.js.

```text
src/
│
├── App.vue
├── main.js
├── routes.js
│
├── components/
│   ├── Basket.vue
│   ├── BasketAddress.vue
│   ├── BasketPayment.vue
│   ├── Header.vue
│   │
│   ├── ForBasket/
│   │   ├── ButtonContainer.vue
│   │   ├── Pay.vue
│   │   ├── Product.vue
│   │   └── Vendor.vue
│   │
│   ├── ForBasketAddress/
│   │   └── Preaddress.vue
│   │
│   ├── ForBasketPayment/
│   │   ├── SumProduct.vue
│   │   └── SumVendor.vue
│   │
│   └── Share/
│       ├── Back.vue
│       ├── Button.vue
│       ├── Cash.vue
│       └── Chose.vue
│
├── data/
│   └── AddressDate.js
│
└── store/
    └── store.js
```

### Application Flow

```text
main.js
   │
   ├── Vue Router
   │
   ├── Vuex Store
   │
   └── App.vue
          │
          ├── Header
          │
          └── router-view
                 │
                 ├── Basket
                 │
                 ├── BasketAddress
                 │
                 └── BasketPayment
```

---

## 🧠 State Management

**Vuex** is used as the centralized state management solution.

The main state contains:

```js
state = {
  cart,
  AddressData,
  ChosedAddress
}
```

### Main Getters

The store provides getters for:

- Cart data
- Number of cart items
- Total cart price
- Vendor-specific price
- Total number of products/items

### Actions

The main API-related action is responsible for fetching cart data.

```text
Component
    ↓
Vuex Action
    ↓
Axios
    ↓
API
    ↓
Mutation
    ↓
Vuex State
    ↓
Component
```

This keeps API communication and shared state separate from the UI components.

---

## 🧩 Component Structure

The application is divided into reusable components.

### Basket

Responsible for displaying the overall shopping cart and its vendors.

### Vendor

Represents a single seller/vendor and contains:

- Vendor information
- Vendor products
- Vendor total
- Shipping information

### Product

Responsible for individual product interactions:

- Quantity management
- Stock validation
- Product removal
- Price calculation

### BasketAddress

Responsible for the delivery-address selection step.

### BasketPayment

Responsible for the final checkout/payment interface.

### Shared Components

Reusable components such as buttons, back navigation, price summaries and selection controls are placed inside:

```text
components/Share/
```

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| Vue.js 2 | Frontend framework |
| Vue Router | Client-side routing |
| Vuex | State management |
| Axios | HTTP/API requests |
| JavaScript | Application logic |
| HTML | UI structure |
| CSS | Styling |
| IRANSans | Persian typography |

---

## 🌐 Routes

The application currently contains three main routes:

| Route | Component | Description |
|---|---|---|
| `/` | `Basket.vue` | Shopping cart |
| `/BasketAddress` | `BasketAddress.vue` | Delivery address selection |
| `/BasketPayment` | `BasketPayment.vue` | Payment / checkout |

---

## 🔌 API

Cart information is retrieved from the following endpoint:

```text
GET https://mini-cart.iran.liara.run/v1/cart
```

The response contains cart information including vendors and their products.

The application consumes this data through Axios and stores it in Vuex.

### API Data Flow

```text
API
 │
 │ GET /v1/cart
 ▼
Axios
 │
 ▼
Vuex Action
 │
 ▼
Vuex Mutation
 │
 ▼
state.cart
 │
 ├── Basket
 ├── Vendor
 ├── Product
 └── Payment Summary
```

> The address data used by the current implementation is local/static data rather than being retrieved from an address API.

---

## 📱 Screenshots

Screenshots of the application can be added to this section.

Recommended structure:

```text
docs/
└── screenshots/
    ├── basket.png
    ├── address.png
    └── payment.png
```

Then reference them in the README:

### Shopping Cart

![Shopping Cart](docs/screenshots/basket.png)

### Address Selection

![Address Selection](docs/screenshots/address.png)

### Payment

![Payment](docs/screenshots/payment.png)

> If screenshots are not yet available, add them to `docs/screenshots/` and update the paths above.

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- Node.js
- npm

You can verify your installation with:

```bash
node --version
npm --version
```

### Installation

Clone the repository:

```bash
git clone https://github.com/nasrinrezaei/basalam-internship.git
```

Navigate to the project directory:

```bash
cd basalam-internship
```

Install dependencies:

```bash
npm install
```

### Run Development Server

```bash
npm run serve
```

The application will then be available through the local development server.

### Build for Production

```bash
npm run build
```

### Lint

```bash
npm run lint
```

---

## 🔄 User Flow

The main user journey is:

```text
┌───────────────┐
│ Shopping Cart │
└───────┬───────┘
        │
        ▼
┌───────────────────┐
│ Manage Products   │
│ • Quantity        │
│ • Remove Product  │
│ • Stock Check     │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│ Address Selection │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│ Payment / Checkout│
│ • Discount Code   │
│ • Credit          │
│ • Gateway         │
└───────────────────┘
```

---

## 🎯 Internship Goals

This project was developed to practice and demonstrate:

- Building reusable Vue components
- Managing shared application state with Vuex
- Working with REST APIs
- Handling asynchronous data fetching
- Implementing client-side routing
- Building a multi-vendor shopping cart
- Implementing reactive UI interactions
- Working with Persian/RTL interfaces
- Structuring a frontend project for a real-world marketplace scenario

---

## 🔮 Possible Improvements

Some possible next steps for extending the project include:

- Connect address management to a backend API
- Implement real payment gateway integration
- Implement discount-code validation
- Connect account credit to the checkout calculation
- Persist cart changes on the backend
- Make the cart badge dynamically reflect the actual cart quantity
- Add automated tests
- Improve responsive behavior for larger screen sizes
- Add environment variables for API configuration
- Improve error handling for individual API operations

---

## 👩‍💻 Author

**Nasrin Rezaei**

GitHub: [@nasrinrezaei](https://github.com/nasrinrezaei)

---

## 📄 License

This project was created as part of an internship project and is intended primarily for educational and demonstration purposes.
