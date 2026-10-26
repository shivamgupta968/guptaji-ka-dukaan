# Guptaji Ka Dukaan — Saree Collection

Full-stack beginner project: responsive storefront, product search/category/price sorting, quantity-aware cart, Express API, SQLite database, and Razorpay checkout integration.

## Run on Windows
1. Install Node.js 18+ from https://nodejs.org/.
2. Extract the ZIP and open the `guptaji-saree-collection` folder in VS Code.
3. VS Code → Terminal → New Terminal.
4. Run `npm.cmd install` then `npm.cmd start`.
5. Open http://localhost:3000. Keep the terminal open.

The server creates `data/store.sqlite` and seeds 16 sample sarees on first run.

## Razorpay test payment
1. Create/sign into a Razorpay account and enable Test Mode.
2. Copy `.env.example` to `.env` in the project root.
3. Add your Razorpay **test** Key ID and Key Secret to `.env`; never put the secret in frontend files or GitHub.
4. Restart the server, then test checkout. Without keys, checkout creates a clearly marked demo order and WhatsApp follow-up; it does not collect money.

Payment flow follows Razorpay's server-created order and server-side signature verification guidance. Official docs: https://razorpay.com/docs/payments/payment-gateway/web-integration/standard/build-integration/

## Stack explained
- Frontend: HTML (page structure), CSS (responsive visual design), JavaScript (search, filters, cart and checkout UI).
- Backend: Node.js runs JavaScript on the server; Express defines routes and validates requests.
- Database: SQLite stores the catalogue and orders in `data/store.sqlite`.
- API: `GET /api/products`, `POST /api/checkout`, `POST /api/verify-payment`, `GET /api/orders/:ref`.
- Payment: Razorpay checkout. The server calculates the total from database prices and verifies the payment signature.
- Cart persistence: browser `localStorage` remembers quantities on that browser/device.

## Before public launch
- Sample images/prices/descriptions are illustrative. Replace them with real, store-owned/authorized product photos and confirm all prices/stock.
- Location is currently only the city/town: Machhlishahr, Jaunpur, Uttar Pradesh. Add exact shop address only after confirming it.
- For production configure HTTPS, live gateway onboarding, environment secrets, webhook reconciliation, secure order tracking/admin login, privacy and return policies, backups and monitoring. The demo order lookup route should not expose customer details (it currently returns only reference, total and status).
- SQLite needs persistent storage on the deployment host. If the host has ephemeral filesystems, migrate to managed PostgreSQL or another managed database.


## Catalogue photos and setup notes

This version includes 25 locally stored product reference images supplied by the shop owner in `public/images/`. The images are cropped from supplied social-media screenshots for a cleaner catalogue display. Please confirm the exact fabric, colour, stock, and price with the shop before accepting a real order. Product names and prices are demo catalogue entries and can be edited in `server.js`.

### Run on Windows
1. Open this project folder (the one containing `package.json` and `server.js`) in VS Code.
2. In Terminal run `npm.cmd install`.
3. Run `npm.cmd start`.
4. Open `http://localhost:3000`. Keep the terminal open while testing.

### Important for existing installations
If you already ran an earlier version, its SQLite database may still contain the old 16 demo products. Stop the server first, then delete `data/store.sqlite` inside this project folder before restarting to seed the new 25-product catalogue. This deletes only the local demo database and its test orders. Back it up first if you need any existing order records.

### Payments
Checkout works in demo mode until you add Razorpay **test** credentials to `.env` (copy `.env.example` to `.env`). Never paste secret keys into public files or share them in screenshots. Do not enable live payments until the business account and delivery/payment process are ready.


## Update: 28 more catalogue photos and banner photo
- 28 new product photos added as `public/images/saree-26.jpg` to `saree-53.jpg`, cropped from the supplied WhatsApp and social-media screenshots. Originals are kept in `public/images/original-uploads/batch-2026-10-24-late/`.
- Product names, categories, tags and prices for these 28 items are placeholders written from the photos. Confirm fabric, colour, stock and the real price with the shop, then edit them in `server.js`.
- The Diwali banner is a single designed image, `public/images/banner-diwali.jpg` (1600×600). It contains the headline, motivation line, price range, WhatsApp number and two photos. To change the text or photos, edit the image in any design tool and replace that file.
- The product list is seeded only when the database is empty. If you ran an earlier version, stop the server, back up and delete `data/store.sqlite`, then restart to load all 53 products.https://guptaji-ka-dukaan.onrender.com
