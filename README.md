# KimTech — Premium Fashion Storefront

> **A single-file, dependency-free e-commerce storefront for premium fashion.**
> Built with vanilla HTML, CSS, and JavaScript — designed to feel like a boutique, not a template.

---

## 📖 Overview

KimTech is a **complete, self-contained fashion storefront** that runs from a single `index.html` file. No build step, no framework, no npm install. Open it in a browser and it works.

It's designed around a **WhatsApp-first checkout model** — perfect for independent boutiques, fashion entrepreneurs, and small brands who want a beautiful storefront without the complexity and monthly fees of Shopify or WooCommerce.

The entire shopping experience — browsing, filtering, cart management, wishlist, quick view, promo codes, currency conversion, and order submission — happens client-side, then hands off to WhatsApp with a **pre-formatted order message** the moment the customer is ready to buy.

---

## ✨ Features at a Glance

### 🛍️ Shopping Experience
| Feature | Description |
|---|---|
| **Multi-currency display** | 13 currencies (KES, USD, EUR, GBP, JPY, and more) with locale-aware formatting |
| **Product grid** | 24 demo products across Men / Women / Accessories with hover image swap |
| **Advanced filtering** | Live search + price bands + size filter, all combinable |
| **Sorting** | Featured, price low→high, price high→low |
| **Category navigation** | Nav links, footer links, and clickable category cards |
| **Recently viewed** | Persistent strip tracks the last 6 products you opened |

### 🛒 Cart & Wishlist
| Feature | Description |
|---|---|
| **Slide-out cart drawer** | Add/remove/adjust quantities without leaving the page |
| **Live subtotal** | Updates on every change in your selected currency |
| **Free-shipping progress bar** | Visual nudge toward the free-shipping threshold |
| **Persistent cart** | Survives page refresh via `localStorage` |
| **Wishlist drawer** | Heart icon in header with count badge; add-to-cart directly from wishlist |
| **Upsell suggestions** | "Complete the look" accessories appear in cart drawer |

### 🎨 Product Cards
| Feature | Description |
|---|---|
| **Hover image swap** | Second photo crossfades in on hover (desktop) |
| **Flag badges** | Sale / New / Bestseller / Limited |
| **Stock states** | "Sold out" overlay, "Only N left" urgency note |
| **Color swatches** | See available colors directly on the grid tile |
| **Quick view** | Full-size image gallery, size guide, color picker, share button |
| **Broken image fallback** | Elegant SVG placeholder — no broken-image icons, ever |

### 💳 Checkout & Ordering
| Feature | Description |
|---|---|
| **WhatsApp order submission** | Formatted message with items, subtotal, shipping, discount, gift wrap, ETA |
| **Promo codes** | `WELCOME10` (10%), `VIP20` (20%), `FREESHIP` |
| **Gift wrap option** | +$5 add-on, reflected in total and WhatsApp message |
| **Fit preference** | Regular / Slim / Relaxed — carried into the order message |
| **Delivery ETA** | Country-specific estimate ("5–8 business days") shown pre-purchase |
| **Per-country shipping rates** | 17 destinations with independent shipping cost |
| **Payment method selector** | M-Pesa (Kenya), bank transfer, cash on delivery, or "other" |
| **Form validation** | Inline errors, focus management, no page reload |

### 🎁 Polish & Accessibility
| Feature | Description |
|---|---|
| **Dark mode** | Toggle in header, persists via `localStorage`, respects `prefers-color-scheme` |
| **Reduced-motion support** | Respects `prefers-reduced-motion` throughout |
| **Keyboard-first** | Full tab navigation, `Escape` closes overlays, focus trapped inside modals |
| **Screen-reader friendly** | `aria-label`, `aria-pressed`, `aria-live`, `role="dialog"`, `sr-only` helpers |
| **Semantic markup** | Single `<a>` per card (avoids 120+ tab stops on a 24-product grid) |
| **Lazy-loaded images** | `loading="lazy"` + explicit width/height (no layout shift) |
| **Scroll-reveal animations** | Subtle fade-up, disabled for reduced-motion users |
| **Toast notifications** | Non-blocking feedback for cart and wishlist actions |

---

## 🚀 Quick Start

### 1. Download the file
Save the HTML file as `index.html`.

### 2. Configure your store
Open `index.html` in any text editor. At the top of the `<script>` block, find the **Store Settings** section:

```js
/* ===== Store settings ===== */
const WA_NUMBER = '2547XXXXXXXX'; // ⚠️ REQUIRED: replace with your number
const FREE_SHIP_MIN = 15000;      // USD cents — 15000 = $150
```

**The store will not submit orders until `WA_NUMBER` is set to a real number.**

Format: digits only, including country code, **no `+`, no spaces, no dashes.**
- ✅ `254712345678`
- ❌ `+254 712 345 678`
- ❌ `2547XXXXXXXX`

### 3. Test the WhatsApp connection
Add a product to cart, open checkout, fill the form, and click **Send order via WhatsApp**. You should see a new WhatsApp tab with the pre-formatted order message. If it opens correctly, the store is live.

### 4. Open in a browser
Double-click `index.html` or serve it locally:

```bash
# Option A: just open it
open index.html

# Option B: local server (recommended for localStorage testing)
python3 -m http.server 8000
# then visit http://localhost:8000
```

No build step, no dependencies, no `npm install`. It just works.

---

## ⚙️ Customization

All configuration lives in two blocks at the top of the `<script>`:

### Store settings

```js
const WA_NUMBER = '254712345678';   // Your WhatsApp business number
const FREE_SHIP_MIN = 15000;        // $150 USD cents — set to Infinity to disable
const GIFT_WRAP_USD_CENTS = 500;    // $5 gift wrap add-on
```

### Shipping rates (per destination, in USD cents)

```js
const SHIPPING_USD_CENTS = {
  US: 1000,   // $10
  GB: 1800,   // $18
  KE: 2500,   // $25
  OTHER: 3000 // fallback
};
```

### Currencies (indicative FX rates)

```js
const FX = {
  USD: 1,
  KES: 130,   // 130 KES per 1 USD
  EUR: 0.92,
  // ...
};
```

⚠️ These are **static rates** — update them periodically or replace with a live FX API.

### Delivery estimates

```js
const ETA = {
  KE: '1–3 business days',
  US: '5–8 business days',
  OTHER: '7–12 business days'
};
```

### Promo codes

```js
const PROMOS = {
  WELCOME10: { pct: 10, label: '10% off your order' },
  VIP20:     { pct: 20, label: '20% VIP discount' },
  FREESHIP:  { ship: 0, label: 'Free shipping' }
};
```

Add your own — keys are matched case-insensitively.

### Products

The `products` array is the heart of the catalog. Each object supports:

```js
{
  id: 1,
  name: 'Oversized Blazer',
  price: 12900,              // USD cents → $129.00
  was: 15900,                // optional — shows strikethrough + Sale badge
  img: 'https://...',        // primary image
  img2: 'https://...',       // optional — hover swap image
  cat: 'men',                // 'men' | 'women' | 'accessories'
  flag: 'new',               // optional — 'new' | 'bestseller' | 'limited'
  stock: 8,                  // integer — 0 = sold out, ≤5 = "Only N left"
  colors: ['#1a1a1a', ...]   // optional — color swatches on card + QV
}
```

**To add a product**: append to the array.
**To remove one**: delete it — the cart automatically sanitizes against the array on load.

---

## 🧱 Tech Stack

| Layer | Choice | Why |
|---|---|---|
| Markup | **HTML5** | Semantic, accessible, no compilation |
| Styling | **CSS custom properties** | Themeable via `data-theme="dark"` |
| Scripting | **Vanilla JavaScript (ES2015+)** | Zero dependencies, ~500 lines |
| State | **`localStorage`** | Cart + wishlist + recently-viewed + theme persist across sessions |
| Fonts | **Google Fonts** | Cormorant Garamond (serif) + Inter (sans) |
| Icons | **Remix Icon CDN** | Single line of HTML |
| Images | **Unsplash** | Demo content only — replace with your own |

**Total size**: ~95 KB unminified. No frameworks, no bundlers, no runtime.

---

## 📁 File Structure

```
index.html          ← everything lives here
  ├── <head>
  │   ├── Meta tags (SEO, Open Graph, theme-color)
  │   ├── Theme loader (prevents dark-mode flash)
  │   ├── Fonts + icons
  │   └── <style> — ~1,200 lines of CSS
  ├── <body>
  │   ├── Header (nav, currency, theme, wishlist, cart)
  │   ├── Hero section
  │   ├── Value props strip
  │   ├── Category cards
  │   ├── Product section (filter bar, grid, recently viewed)
  │   ├── Promo banner
  │   ├── Stats + features
  │   ├── Footer
  │   ├── Checkout modal
  │   ├── Cart drawer
  │   ├── Wishlist drawer
  │   ├── Quick view modal
  │   └── Toast + floating WhatsApp button
  └── <script> — ~700 lines, single IIFE
      ├── Store settings (WA_NUMBER, FX, shipping, ETA, promos)
      ├── Product catalog
      ├── Utilities (money, escape, storage)
      ├── State (cart, wishlist, recent, filters)
      ├── Render functions (products, cart, wishlist)
      ├── Event handlers (filters, add, remove, checkout)
      └── Init
```

Everything in one file means **one HTTPS upload** and you have a store.

---

## ♿ Accessibility Notes

This storefront deliberately exceeds typical template accessibility:

- **Focus trapping** inside every modal and drawer, with `Escape` to close.
- **ARIA state** on toggles (`aria-pressed`, `aria-expanded`, `aria-hidden`).
- **Live regions** for cart updates (`aria-live="polite"` on summary).
- **Single tab stop per product card** — a link wrapper, not five separate interactive elements.
- **`prefers-reduced-motion`** disables all animations and reveals.
- **Visible focus rings** via `:focus-visible` with the accent gold color.
- **Color-independent state** — sold-out uses both color *and* text ("Sold out").

---

## 🌐 Deployment

Because it's a single static file, you can host it anywhere:

| Host | Steps |
|---|---|
| **GitHub Pages** | Push `index.html` to a repo → Settings → Pages → enable |
| **Netlify** | Drag-and-drop the file → instant HTTPS URL |
| **Vercel** | `vercel` in the folder |
| **Cloudflare Pages** | Upload the file |
| **Any web host** | FTP the file to `public_html/` |

**No server, no database, no backend.**

---

## 🔒 Security & Privacy Notes

- **No analytics** are embedded — add your own (Plausible, Fathom, GA4) as needed.
- **No cookies** are used — persistence is via `localStorage` only (cart, wishlist, recent, theme).
- **No payment data** ever touches this page — the customer pays you via whatever method they choose after WhatsApp confirmation.
- **No customer data** is sent anywhere except the WhatsApp message they explicitly send.
- Your `WA_NUMBER` is public in the HTML source. Use a **dedicated business WhatsApp number**, not a personal one.

---

## ⚠️ Before Launch Checklist

- [ ] Replace `WA_NUMBER` with a real business WhatsApp number (digits only, no `+`)
- [ ] Replace all demo Unsplash images with your own product photos
- [ ] Add a **favicon** (`<link rel="icon" ...>`)
- [ ] Add a **canonical URL** (`<link rel="canonical" ...>`)
- [ ] Add an **OG image** (`<meta property="og:image" content="...">`)
- [ ] Update `FX` rates to current values (or integrate a live FX API)
- [ ] Update `SHIPPING_USD_CENTS` with real rates from your carrier
- [ ] Update `ETA` estimates with real dispatch-to-door timelines
- [ ] Add **real return / privacy / terms pages** (footer links currently point to `#contact`)
- [ ] Review the `PROMOS` codes — remove demo codes, add your own
- [ ] Test the full flow on mobile (iOS Safari + Android Chrome)
- [ ] Verify the WhatsApp message formatting looks correct on both sender and receiver
- [ ] Consider adding a `<noscript>` fallback or minimal message for JS-disabled browsers
- [ ] Run [Lighthouse](https://pagespeed.web.dev/) on the deployed URL

---

## 🧪 Testing the Store

Everything below works in the demo without any configuration (except WhatsApp submission, which requires a real `WA_NUMBER`):

| Test | Expected result |
|---|---|
| Click **Men** in nav | Grid filters to men's products |
| Type `jacket` in search | Only jacket products show |
| Click **Add to wishlist** heart | Header count increments; item appears in wishlist drawer |
| Click product image | Quick View opens with image gallery |
| Change Quick View size → **Add to cart** | Cart drawer opens; item appears |
| Open cart → click **+** on qty | Quantity increments; subtotal updates |
| Apply `WELCOME10` in checkout | 10% discount row appears; total drops |
| Apply `FREESHIP` | Shipping becomes `Free` |
| Select **Gift wrap** in checkout | +$5 row appears in summary |
| Change country to **United States** | Currency switches to USD; ETA updates |
| Toggle **dark mode** in header | Theme persists on refresh |
| Open **Recently viewed** | Last 6 products shown |
| Toggle sold-out item | "Sold out" flag; Add button disabled |
| Reload page | Cart, wishlist, recent, theme, currency all persist |

---

## 🛠️ Extending the Store

The single-file design makes extension straightforward:

- **Add a currency** → one entry in `FX` and `CURRENCY_LOCALES`
- **Add a country** → one entry in `COUNTRY_CONFIG`, `SHIPPING_USD_CENTS`, and `ETA`
- **Add a promo** → one entry in `PROMOS`
- **Add a category** → add the `cat` value to products, add to `TITLES`, add a nav link
- **Add a flag** → pass any string to `flag` (e.g. `'editor's pick'`)
- **Change brand colors** → edit the `:root` CSS variables at the top of `<style>`
- **Add product descriptions** → set `desc` on a product; it appears in Quick View
- **Add a second image for hover** → set `img2`

For larger catalogs, consider:
- Moving the `products` array to a separate `products.js` file (still no build step)
- Splitting CSS into `styles.css`
- Migrating to a static-site generator (Astro, Eleventy) that outputs a single HTML file

---

## 🤝 Why WhatsApp Checkout?

For boutique fashion brands, a full e-commerce backend is often overkill:

- **No payment gateway fees** (2.9% + $0.30 per transaction adds up)
- **No PCI compliance** burden
- **No abandoned cart** tracking to build
- **Conversational trust** — customers can ask questions before paying
- **Familiar UX** for African, South Asian, and Middle Eastern markets where WhatsApp is the default commerce channel
- **Instant setup** — no merchant account, no bank integration, no waiting for approval

The tradeoff is manual order processing. For a boutique shipping 10–100 orders per week, that's a feature, not a bug.

---

## License

**Single-business license**

- You may customize the template for **one business or one end project**.
- You may **not** resell, redistribute, share or repackage the original template or its source files, or offer them as a competing template.
- You are responsible for making sure that the images, fonts, logos and other assets used on your published store are properly licensed.

---

---

## 💡 Credits

- Fonts: [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) & [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts
- Icons: [Remix Icon](https://remixicon.com/)
- Demo images: [Unsplash](https://unsplash.com/) (replace with your own before launch)

---

<div align="center">

**Built for independent fashion brands who want a storefront that feels like a boutique — not a template.**

[⬆ back to top](#kimtech--premium-fashion-storefront)

</div>
```


**Created by KIMTECH PUBLISHER**
Digital templates and practical technology resources.
