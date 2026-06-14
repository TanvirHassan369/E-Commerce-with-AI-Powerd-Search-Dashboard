# 📊 E-Commerce Admin Dashboard

The admin panel for managing the full-stack e-commerce platform. Built with React 19 and Vite, featuring product management, order tracking, user management, analytics charts, and rich text editing.

---

## ✨ Features

- 📈 Analytics dashboard with charts (Recharts)
- 🛍️ Product management — add, edit, delete with rich text editor
- 📦 Order management & status updates
- 👥 User management
- 🖼️ Image upload support
- 📝 Rich text editor (Jodit React + MD Editor)
- 🔐 Admin authentication & protected routes
- 🔔 Toast notifications
- 📱 Fully responsive design

---

## 🧱 Tech Stack

| Technology | Purpose |
|---|---|
| React 19 + Vite | UI framework & build tool |
| Redux Toolkit | State management |
| React Router v7 | Client-side routing |
| Tailwind CSS | Styling |
| Recharts | Analytics charts |
| Axios | API communication |
| Jodit React | Rich text editor |
| React Toastify | Notifications |
| Lucide React + React Icons | Icons |

---

## 📁 Project Structure

```
ecommerce-dashboard-template/
├── public/             # Static assets
├── src/
│   ├── components/     # Reusable UI components
│   ├── pages/          # Dashboard, Products, Orders, Users, etc.
│   ├── store/          # Redux store & slices
│   ├── App.jsx
│   └── main.jsx
├── index.html
├── package.json
└── vite.config.js
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- Backend server running (see [Server README](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Backend/edit/main/README.md))

### Installation

```bash
# Clone the repository
git clone https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Dashboard

# Navigate to dashboard
cd "ECommerce(Dashboard)/ecommerce-dashboard-template"

# Install dependencies
npm install

# Start development server
npm run dev
```

Dashboard runs at `http://localhost:5174`

### Environment Variables
Create a `.env` file:
```
VITE_API_URL=http://localhost:5000
```

---

## 📸 Pages

| Page | Description |
|---|---|
| Dashboard | Overview with analytics & charts |
| Products | Add / edit / delete products |
| Orders | View & manage customer orders |
| Users | Manage registered users |
| Settings | Admin account settings |

---

## 🔗 Related

- 🌐 [Client (Frontend)](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Frontend)
- ⚙️ [Server (Backend)](https://github.com/TanvirHassan369/E-Commerce-with-AI-Powerd-Search-Backend)
