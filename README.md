# 🍔 Cyberhunt CanteenPulse (JMS Canteen)
> **Next-Generation Smart Campus Canteen Operating System with Real-Time Kitchen Pipeline & Crowd Rush Telemetry**

[![Firebase](https://img.shields.io/badge/Database-Firebase%20Firestore-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Tailwind CSS](https://img.shields.io/badge/Styling-Tailwind%20CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Web Audio API](https://img.shields.io/badge/Audio-Synthesized%20Web%20Audio-orange?style=for-the-badge)](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
[![Status](https://img.shields.io/badge/Deployment-Production%20Ready-success?style=for-the-badge)]()

---

## 📌 Executive Overview

**Cyberhunt CanteenPulse** is a decentralized, high-concurrency web application built to eliminate long lunch-break lines and kitchen congestion in college and institutional canteens.

Equipped with a **Dual-Role Architecture (Student Portal & Kitchen Command Console)**, the platform connects students directly with canteen chefs using real-time Firestore listeners, instant audio cues, dynamic UPI payments, and a patent-style **Crowd Rush Radar** that dynamically predicts waiting times.

---

## 🌟 Key Highlights & Features

### 👨‍🎓 1. Student Portal Experience
- **Fluid Food Catalog:** Categorized menu with instant search (`Snacks`, `Meals`, `Beverages`, `Dessert`).
- **Interactive Tray & Cart:** Real-time subtotal calculation, quantity steppers, and campus subsidy breakdown.
- **Dual Checkout Options:**
  - **Dynamic UPI QR & Intent Link:** Open directly inside Google Pay, PhonePe, or Paytm with auto-filled total and canteen merchant VPA.
  - **Counter Cash Payment:** Instant order placement with cash-pending flag for kitchen verification.
- **Personal Order History & Token Tracker:** 4-stage visual progress tracker (`New ➔ Cooking ➔ Ready ➔ Collected`) with token ID assignment.
- **Auditory Pick-Up Alert:** Synthesizes an ascending 3-note chime (`523Hz ➔ 659Hz ➔ 784Hz`) via Web Audio API the instant the kitchen marks food **Ready**.

---

### 🍳 2. Kitchen Staff Command Console
- **Instant Order Stream:** Zero-delay order sync across devices via Cloud Firestore `onSnapshot`.
- **Audio Order Bell:** Double-tone kitchen chime (`587Hz` & `880Hz`) sounds immediately when a new ticket is booked.
- **One-Tap Order Progression:** Fast, touch-friendly state transitions:
  - `New` ➔ `Cooking` ➔ `Ready` ➔ `Collected`
- **Cash Verification:** One-tap `Collect ₹XX` button to confirm physical payment upon pickup.
- **Real-Time Stock Manager:** Instantly toggle items between **In Stock** and **Sold Out**. Out-of-stock items immediately disable across all student devices without reload.
- **Daily Sales & Revenue Summary Tab:**
  - **Total Revenue:** Verifiable tally of confirmed earnings.
  - **Payment Mode Split:** Clean division of UPI Online vs. Counter Cash.
  - **Dish Volumes:** Tabular breakdown of units sold, individual unit costs, and gross yield per dish.

---

### 📡 3. Live Crowd Rush Radar
- Replaces static queue counters with an active load balancer that evaluates active kitchen tickets:
  - 🟢 **Low Rush (0–4 active orders):** Minimal wait time (~3–5 minutes).
  - 🟠 **Medium Rush (5–9 active orders):** Moderate load (~10–15 minutes).
  - 🔴 **High Rush (10+ active orders):** Peak crowd alert (~20–30 minutes) with animated pulse wave.
- Marking an order **Collected** immediately cools down the rush level across all client dashboards.

---

## 🎨 Visual Design & Theme System

- **Warm Sunset Fire Palette:** Tailored with a vibrant blend of golden yellow (`#f59e0b`), fiery orange (`#ea580c`), and crimson red (`#dc2626`).
- **Glassmorphism Panels:** Translucent cards with `backdrop-filter: blur(20px)` and subtle glowing borders.
- **Theme Adaptability:** Includes a dedicated icon toggle (Moon 🌙 / Sun ☀️) that dynamically shifts between high-contrast light mode and an obsidian dark mode.
- **Responsive Layout:** Engineered mobile-first for fluid use on smartphones, tablets, and desktop kitchen screens.

---

## 🛠️ Technology Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend Core** | HTML5, Modern ES6+ JavaScript (Single-File Architecture) |
| **Styling & Icons** | Tailwind CSS CDN, Font Awesome 6.5, Outfit & Plus Jakarta Sans fonts |
| **Cloud Database** | Google Firebase Cloud Firestore (`onSnapshot` real-time listeners) |
| **Authentication** | Anonymous Session Bridge + Firestore Profile Registry |
| **Sound Synthesis** | Native Web Audio API (zero external `.mp3` dependencies) |
| **Payment Flow** | Dynamic QuickChart UPI QR Generator & Universal UPI Deep Linking |

---

## 🚀 Quick Start & Installation

### 1. File Structure Setup
Keep your files organized in the root directory:
```text
canteen-pulse/
├── index.html        # Main single-file application
├── logo.png          # Canteen brand logo (optional, has auto-fallback)
└── README.md         # Project documentation
```

### 2. Run Locally
Because this project uses ES Modules for Firebase, open it via a local web server:

#### Option A: Using VS Code Live Server
1. Open the project folder in **Visual Studio Code**.
2. Right-click `index.html` and click **"Open with Live Server"**.

#### Option B: Using Python
```bash
# Python 3
python -m http.server 8000
```
Then visit: `http://localhost:8000`

---

## 🔑 Default Credentials

### 👨‍🍳 Kitchen Staff Access
- **Portal Tab:** Kitchen Staff
- **Staff ID:** `staff101`
- **Access Key:** `admin`

### 🎓 Student Access
- Students can register with any valid Email / Gmail and password.
- **Pre-configured Test Account:**
  - **Email:** `surya@gmail.com`
  - **Password:** `123`

---

## 🔒 Firebase Security Rules

For testing and hackathon demonstrations, ensure your Firestore rules permit read/write access:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

> **Note:** In production, restrict read/write permissions based on authenticated user IDs and staff roles.

---

## 💡 Presentation Highlights for Judges

1. **True Cross-Device Interactivity:** Open the Student portal on a smartphone and the Staff console on a laptop; placing an order immediately chimes and renders in the kitchen queue.
2. **Resilience & Local Fallback:** Even under network fluctuations, the application maintains state locally via `localStorage` and `BroadcastChannel`.
3. **Operational Clarity:** Separated daily sales analytics allow canteen managers to balance the cash register at closing time with zero paperwork.

---

## 📄 License
This project is open-source under the [MIT License](LICENSE).