# Daily Bazar — Admin Dashboard

React-based admin panel for **Daily Bazar**. Provides full control over products, orders, users, return requests, contact messages, and newsletter subscribers. Includes a live analytics dashboard powered by Recharts and a date-range report generator.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 19 + Vite |
| State Management | Redux Toolkit |
| Routing | React Router v7 |
| Styling | Tailwind CSS |
| Charts | Recharts |
| HTTP Client | Axios |
| Rich Text Editor | Jodit React + `@uiw/react-md-editor` |
| Icons | Lucide React, React Icons |
| Notifications | React Toastify |

---

## Features

### Authentication
- Admin login / logout via JWT (HTTP-only cookie, same API as client)
- `loadUser` on app mount to restore session
- Admin profile update with avatar upload

### Dashboard — Analytics Overview
Powered by `GET /api/v1/admin/fetch/dashboard-stats`:
- **Total Revenue** — sum of all paid orders
- **Today's Revenue** vs Yesterday's Revenue
- **Monthly Revenue Growth Rate** (current vs previous month, %)
- **Order Status Counts** — Processing, Shipped, Delivered, Cancelled, Returned
- **Monthly Sales Line Chart** (Recharts)
- **Top 5 Selling Products** table with image, category, units sold
- **Low Stock Alerts** — products with stock ≤ 5
- **New Users This Month**
- **Newsletter Subscriber Count**

### Report Generator
- Date-range picker (`from` / `to`)
- Calls `GET /api/v1/admin/fetch/report`
- Returns: total revenue, total orders, order status breakdown, new users, daily sales chart, top 10 products, return statistics (total / pending / approved / rejected)

### Products
- List all products with image, price, stock, category
- **Create** — multipart form with Jodit rich text editor for description, Cloudinary upload, size variants (for Fashion), discount price
- **Update** — edit existing product, add/remove individual images (syncs Cloudinary), update sizes
- **Delete** — removes product and all Cloudinary images
- View product modal

Redux slice: `fetchProducts`, `createProduct`, `updateProduct`, `deleteProduct`

### Orders
- Full order list with payment status, shipping info
- Update order status: Processing → Shipped → Delivered → Cancelled
- Status update logic on backend:
  - `Cancelled` restores stock + marks payment Refunded/Cancelled
  - `Delivered` (COD) marks payment Paid, deducts stock
- Delete order

### Return Requests
- View all return requests with buyer info, order total, shipping address, reason, description
- **Approve** — sets order to Returned, payment to Refunded, restores stock (DB transaction)
- **Reject** — with optional admin note shown to customer
- Status badges: Pending / Approved / Rejected

### Users
- Paginated user list (10 per page)
- Delete user (also removes Cloudinary avatar)

### Contact Messages
- View all messages with read/unread status
- Mark as read
- Delete message

### Newsletter Subscribers
- View all subscriber emails with subscription date

### Admin Profile
- Update name, email, phone, avatar

---

## Redux Store

| Slice | State | Async Actions |
|---|---|---|
| `authSlice` | `user`, `isAuthenticated` | `loginAdmin`, `loadUser`, `logoutAdmin`, `updateAdminProfile` |
| `productsSlice` | `products`, `loading` | `fetchProducts`, `createProduct`, `updateProduct`, `deleteProduct` |
| `orderSlice` | `orders`, `returnRequests` | `fetchAllOrders`, `updateOrderStatus`, `deleteOrder`, `fetchAllReturnRequests`, `updateReturnRequest` |
| `adminSlice` | `stats`, `users`, `subscribers` | `fetchDashboardStats`, `fetchAllUsers`, `deleteUser`, `fetchAllSubscribers` |
| `extraSlice` | modal open flags | `toggleCreateProductModal`, `toggleUpdateProductModal`, `toggleViewProductModal` |

---

## Project Structure

```
ecommerce-dashboard-template/
├── public/
├── src/
│   ├── components/       # Reusable UI (charts, tables, modals, sidebar)
│   ├── pages/            # Dashboard, Products, Orders, Returns
│   │                     # Users, Messages, Subscribers, Profile
│   ├── store/
│   │   ├── index.js      # Redux store
│   │   └── slices/       # authSlice, productsSlice, orderSlice
│   │                     # adminSlice, extraSlice
│   ├── lib/
│   │   └── axiosInstance.js
│   ├── App.jsx
│   └── main.jsx
├── index.html
└── package.json
```

---

## Getting Started

### Prerequisites
- Node.js v18+
- Backend server running (see [Server README](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Backend/blob/main/README.md))
- Admin account in the database (`role = 'Admin'`)

### Installation

```bash
cd "ECommerce(Dashboard)/ecommerce-dashboard-template"
npm install
npm run dev
```

Dashboard runs at `http://localhost:5174`

### Environment Variables

Create a `.env` file:

```env
VITE_API_URL=http://localhost:5000/api/v1
```

---

## Pages Summary

| Page | Route | Description |
|---|---|---|
| Login | `/login` | Admin authentication |
| Dashboard | `/` | Analytics overview + charts |
| Products | `/products` | CRUD with rich text editor |
| Orders | `/orders` | Order management + status updates |
| Returns | `/returns` | Approve / reject return requests |
| Users | `/users` | View + delete registered users |
| Messages | `/messages` | Contact form inbox |
| Subscribers | `/subscribers` | Newsletter subscriber list |
| Profile | `/profile` | Update admin profile |

---

## Related Repositories

- 🌐 [Client (Frontend)](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Frontend)
- ⚙️ [Server (Backend API)](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Backend)
