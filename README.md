# KimTech Premium Fashion Storefront

A responsive, single-page fashion storefront built with HTML, CSS and JavaScript. It is designed for fashion brands, clothing boutiques and online stores that want a polished storefront with product discovery and a WhatsApp-based order flow.

> **Please note:** this is a front-end template. It does not include a backend, database, customer accounts, inventory management or a card / mobile-money payment gateway. Orders are sent through WhatsApp. See [Limitations](#limitations).

---

## Contents

- [Features](#features)
- [Package contents](#package-contents)
- [Quick start](#quick-start)
- [Configuration](#configuration)
- [Customization](#customization)
- [WhatsApp ordering](#whatsapp-ordering)
- [Currency and pricing](#currency-and-pricing)
- [Shipping](#shipping)
- [Publishing](#publishing)
- [Before-launch checklist](#before-launch-checklist)
- [Limitations](#limitations)
- [Support and customization](#support-and-customization)
- [License](#license)

---

## Features

- Responsive layout for desktop, tablet and mobile
- Premium fashion presentation with a calm, minimal design
- Animated logo wordmark
- Product cards with portrait images and an optional hover image swap
- Quick-view panel with size selector and size guide
- Side cart drawer with quantity controls, a free-shipping progress bar and "Complete the look" suggestions
- Wishlist, remembered between visits
- Sorting by price
- Light and dark mode with a toggle (follows the visitor's device setting first)
- Scroll-reveal animations (disabled automatically for visitors who prefer reduced motion)
- Checkout form with contact, delivery and payment-preference fields
- Shipping-cost calculation by country, with a free-shipping threshold
- WhatsApp order-request flow
- Accessibility support: keyboard navigation, focus handling in dialogs, labelled controls
- Easy-to-edit HTML, CSS and JavaScript in a single file

---

## Package contents

```
KimTech-Premium-Fashion/
├── index.html     The complete storefront (HTML, CSS and JavaScript)
└── README.md      This file
```

The template is delivered as a self-contained HTML file. If your package includes additional assets or documentation, keep the supplied folder structure intact.

**Loaded from the internet:** Google Fonts (Cormorant Garamond and Inter), Remix Icon, and the demo product photos. The storefront needs an internet connection to display these correctly.

---

## Quick start

1. Download and extract the package.
2. Open `index.html` in a modern web browser to preview the storefront.
3. Edit the settings and content described below.
4. Upload the files to a static web host to publish (see [Publishing](#publishing)).

No build tools or package installation are required.

---

## Configuration

Open `index.html` in a code editor and scroll to the `<script>` near the bottom. The block marked **Settings (edit here)** controls the main store options:

| Setting | What it controls |
|---|---|
| `WA_NUMBER` | Your WhatsApp business number (digits only, with country code) |
| `FREE_SHIP_MIN` | Order value that unlocks free shipping, **in cents** (`15000` = $150.00) |
| `SHIPPING` | Shipping rate per country, **in cents** |
| `COUNTRY_NAMES` | Display names for the countries in the checkout dropdown |
| `CLOTHING_SIZES` | Sizes offered for clothing (accessories use "One size") |
| `SIZE_GUIDE` | The size chart shown in quick view |
| `products` | Your product catalogue |

---

## Customization

### Store name, logo and branding

Search for `KimTech` in `index.html` and replace it with your brand name. It appears in:

- the page title and meta tags in the `<head>`
- the header logo (set in the script, as `'KimTech'`)
- the footer
- the order message sent to WhatsApp

The animated logo styles the first three letters in bold and the rest in a light weight. Change `i<3` in the logo script to adjust the split.

Also add a favicon and a social-sharing image (see the `TODO` comment in the `<head>`).

### Products

Each product is an entry in the `products` array:

```js
{ id: 1, name: 'Oversized Blazer', price: 12900, was: null, img: 'photo.jpg', cat: 'men' }
```

| Field | Description |
|---|---|
| `id` | A unique number |
| `name` | Product name |
| `price` | Current price **in cents** (`12900` = $129.00) |
| `was` | Original price in cents for sale items, or `null`. Sale items are tagged and appear under **Sale** automatically. |
| `img` | Main product image URL |
| `cat` | `'men'`, `'women'` or `'accessories'` |
| `img2` | *Optional.* A second image, shown when the visitor hovers over the product |
| `desc` | *Optional.* A short description (fabric, fit, care), shown in quick view |

### Images

- Replace the demo photos with images you own or are licensed to use.
- Use consistent photography (same lighting, background and crop). Portrait images with a 4:5 ratio work best.
- Use optimized files (WebP or compressed JPEG) and host them yourself rather than linking to other sites.

### Colors and dark mode

Colors are set as CSS variables at the top of the `<style>` block. Edit the values in `:root` for light mode and in `[data-theme="dark"]` for dark mode.

### Contact details and footer links

Update the demo contact details, social links, policy pages and footer navigation. The Help and About links, and the Privacy and Terms links, are placeholders (`href="#"`) until you point them to real pages. Remove any link or claim that does not apply to your business.

### Placeholder content

Replace or remove the demo statistics (for example "50K+ Happy customers") and any other claims you cannot verify.

---

## WhatsApp ordering

### How it works

1. The customer adds products to the cart and clicks **Checkout**.
2. They complete the checkout form (contact, delivery and payment preference).
3. WhatsApp opens with the order details already written in a message.
4. The customer presses **Send** in WhatsApp. **The order is only placed once you receive the message.**
5. You confirm the total, payment and delivery with the customer in the chat.

### Setting your number

Find `WA_NUMBER` in the script and replace the placeholder with your business number: country code first, digits only, with no `+`, spaces or leading `0`.

For a Kenyan number such as 0712 345 678, use:

```js
const WA_NUMBER = '254712345678';
```

The same number is used for the floating WhatsApp chat button.

### Payment options

The checkout form includes a "Preferred payment method" dropdown (Pay on delivery, Bank transfer, Mobile money). These are examples. Edit the options in the HTML to match how you actually accept payment.

### Test before publishing

Test the whole order flow on both a phone and a desktop computer, including the case where WhatsApp is not installed.

> **Always verify totals yourself.** Prices are calculated in the visitor's browser, so confirm the order total and shipping with the customer before accepting payment.

---

## Currency and pricing

- Prices are stored in cents and displayed with a `$` symbol. To change the currency symbol or format, edit the `money` function in the script.
- All prices are fixed values that you set. There is no live exchange-rate conversion. If you sell in several markets, update converted prices manually and treat displayed conversions as estimates.
- Review every product price before launch. Demo prices are sample content.

---

## Shipping

- Edit the `SHIPPING` object with rates confirmed by your courier or delivery provider. The demo rates are placeholders.
- Only the countries listed in `SHIPPING` and `COUNTRY_NAMES` appear in the checkout dropdown. Add or remove countries to match where you deliver.
- Set `FREE_SHIP_MIN` to your free-shipping threshold, or to a very large number to switch the offer off. If you change it, also update the "Free shipping on orders over $150" text in the top bar and the shipping notice in the quick view.
- Clearly state your delivery areas, fees, estimated delivery times and conditions on a shipping policy page.

---

## Publishing

Because it is a static site, you can publish it with:

- GitHub Pages
- Netlify
- Vercel
- Any web host that supports static HTML files

Upload `index.html` (and any images you host yourself), then connect a custom domain through your hosting provider if you want one. Hosting and domain registration are separate services and are not included with the template.

---

## Before-launch checklist

- [ ] Replace the demo brand name and logo
- [ ] Add a favicon and a social-sharing image
- [ ] Add your product names, descriptions, prices and images
- [ ] Replace the demo photos with images you are licensed to use
- [ ] Set and test your WhatsApp business number
- [ ] Confirm the currency display and prices for each target market
- [ ] Confirm shipping rates and delivery coverage
- [ ] Replace the placeholder size chart with your real measurements
- [ ] Edit the payment-method options to match how you accept payment
- [ ] Update contact information and social links
- [ ] Replace or remove the demo statistics
- [ ] Add your privacy, returns, refund and shipping policies and link them in the footer
- [ ] Test the layout on mobile, tablet and desktop
- [ ] Test quick view, cart, wishlist, dark mode and the WhatsApp order flow
- [ ] Check all links and remove demo content
- [ ] Publish the site and test the live URL

---

## Limitations

This is a front-end starting point. Unless separately developed and integrated, it does not provide:

- Secure online payments
- Server-side order processing
- Database storage
- Stock or inventory synchronization
- Customer registration or login
- An admin dashboard
- Automated order emails
- Live currency conversion
- Courier API integration

These capabilities require suitable third-party services or custom backend development. The cart and wishlist are saved only in the visitor's own browser.

---

## Support and customization

The template can be adapted to match your brand, product catalogue and business workflow. Customization, deployment, payment integration and backend development can be provided as separate services.

---

## License

**Single-business license**

- You may customize the template for **one business or one end project**.
- You may **not** resell, redistribute, share or repackage the original template or its source files, or offer them as a competing template.
- You are responsible for making sure that the images, fonts, logos and other assets used on your published store are properly licensed.

---

**Created by KIMTECH PUBLISHER**
Digital templates and practical technology resources.
