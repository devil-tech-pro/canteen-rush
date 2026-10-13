# Cyberhunt CanteenPulse — Firebase-enabled website

This is your existing single-file HTML/CSS/JavaScript interface connected to Firebase Authentication and Cloud Firestore (Firebase Web SDK v13 compat CDN). Orders, menu stock, user profiles, saved notifications, rush stats, and the order token counter are stored in the Firebase project configured in `index.html`.

## Important before running

1. Open Firebase Console for project `canteen-49cb5`.
2. In **Authentication → Sign-in method**, enable **Email/Password**.
3. In **Firestore Database**, create a database.
4. Open **Firestore → Rules**, paste the contents of `firestore.rules`, and click **Publish**.
5. In **Authentication → Users**, manually create the staff account:
   - Email: `staff101@staff.canteenpulse.com`
   - Password: choose a strong password for the demo, then enter that password in the Staff login form. Do not deploy with `admin`.
6. Run the website via VS Code Live Server, not by opening `index.html` as a `file://` URL. In Firebase Authentication Settings, add `localhost` and `127.0.0.1` to Authorized domains if they are not listed.
7. Sign in once through **Kitchen Staff**. This seeds the initial menu, the rush stats document, and the order-token counter. Then students can register and place orders.

## Run locally

- Extract this folder and open it in VS Code.
- Install the VS Code extension **Live Server**.
- Right-click `index.html` → **Open with Live Server**.
- Common local address: `http://127.0.0.1:5500/index.html`.

Internet is required for Firebase CDN scripts and Firebase services, Tailwind CDN, fonts, icons, and external food images.

## Firebase collections

- `users/{uid}` — student profile, no passwords stored in Firestore.
- `menuItems/{itemId}` — shared menu and availability.
- `orders/{orderId}` — order item snapshots, token, total, payment choice/status, student UID, order status, timestamps.
- `notifications/{notificationId}` — persistent in-app order/payment notifications.
- `stats/rush` — shared active order count and rush level.
- `counters/orders` — sequential token counter.

Students read only their own orders and notifications. The kitchen staff account can read/manage all orders and menu data. Use the supplied rules; do **not** use open test-mode rules.

## Existing browser-only data

The previous version used `localStorage`. This version does not automatically upload old localStorage accounts or orders, because the old user records include plain-text passwords and do not have Firebase Auth UIDs. New registrations/orders are stored in Firestore and can be reviewed in the Firebase Console.

## Payment note

The UI contains a QR/UPI intent for demonstration. It is not a verified payment gateway. The current demo marks UPI orders as `Paid` when submitted, which should be changed before any real deployment. Real payments require a gateway integration and trusted payment verification; never trust a client-side “paid” flag.

## Prototype / security caveat

The provided Firestore rules reduce cross-student access and require Firebase Authentication. `stats/rush` is still updated by browser clients in this hackathon prototype. A production system should move authoritative active-count/token updates to trusted backend code (Cloud Functions or a server), strengthen rate-limits and App Check, and use real staff identity/roles rather than a fixed staff email.
