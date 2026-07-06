# Receiptly

A mobile-first web app for scanning receipts and tracking household expenses — photograph a receipt and AI OCR turns it into an editable expense record.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Try it live
>
> **URL:** [https://receiptly.furkantekkartal.com](https://receiptly.furkantekkartal.com)
>
> **Demo login:** username `demo` · password `demo1234`
>
> A second account, `demo2` · `demo1234`, is a member of the same household — log in with it to see the shared-household feature.
>
> You can also create your own account — registration is open to everyone.

---

## Features

- **AI receipt scanning** — photograph or upload a receipt; an AI OCR pipeline (OpenRouter / Gemini vision) reads the store, date, total and line items and puts them into an editable form.
- **Dashboard** with a weekly / monthly / yearly toggle, a monthly budget progress bar, a 6-month spending trend and a category breakdown.
- **Receipt list** with search, a date-range filter and one-tap CSV export.
- **Normalization** — spread a big one-time purchase over a number of days (1–365) and see it as a TL/day daily average instead of a single spike.
- **Neutralization** — track money you lend; when it comes back, link the two receipts and the pair cancels out of your spending.
- **Households** — share expenses with family: create a household and let others join with a 4-digit invite code.
- **Bilingual UI** — Turkish by default, with an English toggle on the Profile page.
- **JWT auth** with short-lived access tokens and refresh tokens.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite 7, React Router 7, i18next (TR/EN) |
| Backend | Node.js, Express 4, multer file uploads |
| Database | PostgreSQL |
| Auth | JWT (access + refresh tokens, username + password) |
| AI | OpenRouter / Gemini vision APIs for receipt OCR |
| Deployment | Docker behind an Nginx reverse proxy |

## Screens

All screenshots are from the live app in a mobile viewport (390 px) — the UI is designed mobile-first. The interface is shown in Turkish (the default); an English toggle lives on the Profile page. The currency is Turkish lira (TL).

## Login

<img src="images/01-login.png" alt="Login screen" width="390">

- Simple sign-in with username and password — the username is the login identifier, not the email.
- Clean screen with the Receiptly logo and nothing else to distract.
- A "Kayıt Ol" (Sign up) link at the bottom leads to open registration.

## Register

<img src="images/02-register.png" alt="Register screen" width="390">

- Anyone can create an account: first and last name are optional; username, email, password and password confirmation are required.
- Required fields are marked with an asterisk.
- After a successful sign-up the app logs you in automatically.

## Dashboard

<img src="images/03-dashboard.png" alt="Dashboard" width="390">

- The home screen sums up your spending for the selected period — a **weekly / monthly / yearly** toggle sits at the top.
- Three summary cards follow: total spending (₺6.672,15, with an 8% down badge vs. the previous period), receipt count, and the average amount per receipt.
- The **Monthly Budget** card compares spending against the budget set on the Profile page (₺6.672,15 / ₺20.000,00) — a color-coded progress bar shows 33% used and ₺13.327,85 remaining.
- The **Monthly Trend** chart shows the last six months as bars with exact totals on top.
- Further down the page there is a **category breakdown** with percentages and a **recent receipts** list that links to the full receipt list.
- The bottom tab bar (Home / Receipts / Scan / Reports / Profile) is always visible; the camera button in the middle opens the scanner.

## Receipt Scanning (AI OCR)

The flagship feature. Instead of typing a receipt by hand, you photograph it and let the AI do the reading. The scan below uses a real photo of a real printed receipt.

### 1. Scan entry

<img src="images/07-scan.png" alt="Scan receipt entry" width="390">

- The scan page offers three ways in: **Kamera** (take a photo), **Galeri** (upload an image) and **Manuel** (skip OCR and type the receipt yourself).
- The large dashed area shows a preview of the selected image before the upload.

### 2. Scan result — editable draft

<img src="images/07c-scan-ocr-result.png" alt="Scan result with attached receipt photo" width="390">

- After the upload, the AI reads the photo and opens a **prefilled New Receipt form**: here it extracted the store ("Coles"), the purchase date, the total (55.98) and every line item with its quantity and unit price.
- The OCR pipeline runs on the backend (OpenRouter / Gemini vision models); a long receipt takes about 10-30 seconds.
- Nothing is saved automatically — you review the draft, fix anything the AI misread, pick a category and press **Fişi Kaydet** (Save Receipt).
- If a receipt is unreadable, the same form works as a manual fallback.

## My Receipts

<img src="images/04-receipts.png" alt="Receipt list" width="390">

- All receipts in one paginated list: store name, date, category chip and total.
- A debounced search box finds receipts as you type; the gear icon opens a collapsible date-range filter.
- The export button next to **+ Fiş Tara** (Scan Receipt) downloads the list as CSV.
- Normalized receipts carry an extra badge with their daily average — here the Teknosa receipt shows ₺38,88/day.

## Receipt Detail

<img src="images/05-receipt-detail.png" alt="Receipt detail" width="390">

- The full view of one receipt: store (Migros), date, category and the ₺923,15 total.
- **Kalemler** (Items) lists each line item with quantity, unit price and line total — milk, bread, fruit & vegetables, coffee.
- The **Normalleştirme** (Normalization) card takes a number of days and converts the receipt into a daily average.
- Action buttons below: **Düzenle** (Edit), **Sil** (Delete) and **Borç Olarak İşaretle** (Mark as Lent), which sends the receipt to the neutralization pool.

## Normalized Receipt

<img src="images/05b-receipt-normalized.png" alt="Normalized receipt" width="390">

- A ₺3.499,00 Bluetooth headphone purchase from Teknosa, spread over 90 days.
- The header now carries a badge: **90d · ₺38,88/day**.
- The Normalization card shows the day count and the daily average, with a **Ham Veriyi Göster** (Show Raw Data) button to see the original numbers.
- This keeps one big electronics purchase from distorting a whole month's statistics.

## New Receipt (manual form)

<img src="images/06-receipt-new.png" alt="New receipt form" width="390">

- The same form used by the scanner, starting empty for manual entry.
- Fields: store name, a category dropdown, date, total and free-text notes.
- **Kalemler** (Items) grows dynamically with **+ Ekle** — each row takes a product name, quantity, unit price and line total, and the form shows a running total.

## Reports

<img src="images/08b-reports-full.png" alt="Reports page (full)" width="390">

- The **Monthly Trend** chart repeats the 6-month spending bars from the dashboard.
- **En Çok Harcanan Mağazalar** (Top Stores) ranks up to 10 stores by total spending, with receipt counts and progress bars — Shell leads here with ₺5.060,00 across 2 receipts.
- **Ürün Tüketimi** (Product Consumption) ranks the top 10 products with purchase counts and average prices — useful for spotting where the money really goes, from fuel to groceries.

## Neutralizations

<img src="images/09-neutralizations.png" alt="Neutralization pool" width="390">

- The **Nötrleme Havuzu** (Neutralization Pool) tracks lent money so it does not count as real spending forever.
- The summary card shows the pending amount: ₺750,00 lent to a sibling, still waiting.
- Each pending entry has a **Bağla** (Link) button — it opens a picker to pair the lent receipt with the repayment receipt.
- The **Bağlı** (Linked) section shows settled pairs: "Arkadaşa Borç ↔ Borç İadesi" with the ₺1.500,00 amount struck through — the pair cancels out.

## Household

<img src="images/10-household.png" alt="Household page" width="390">

- A household ("Demo Evi") shares expenses between its members.
- The 4-digit **invite code** is shown large — tap to copy, and others join by entering it.
- The member list shows avatars and roles; the creator carries an **Admin** badge and can generate a new code with **Yeni Kod**.
- Any member can leave with **Haneden Ayrıl** (Leave Household).

## Profile

<img src="images/11-profile.png" alt="Profile page" width="390">

- Account overview: avatar, display name and email.
- The **TR | EN** toggle switches the whole UI language instantly.
- The **monthly budget** is edited inline right here — it drives the dashboard's budget bar.
- Navigation rows lead to Change Password, Household and the Neutralization Pool.
- Logout and a double-confirm Delete Account button sit at the bottom.

## Change Password

<img src="images/12-change-password.png" alt="Change password" width="390">

- A focused form: current password, new password (minimum 6 characters) and confirmation.
- Reached from the Profile page and protected like every other authenticated screen.

## Architecture

- **Mobile-first SPA** — a React single-page app with a phone-width layout and a persistent bottom tab bar.
- **REST API** — the Express backend exposes JSON endpoints; requests are validated server-side and authenticated with JWT.
- **Token refresh** — short-lived access tokens plus database-stored refresh tokens; an axios interceptor renews sessions silently.
- **AI OCR pipeline** — receipt images are uploaded with multer, sent to OpenRouter / Gemini vision, and the structured result prefills the receipt form.
- **Shared PostgreSQL** — data lives in a shared Postgres instance, with separate databases for dev and prod.
- **i18n** — all UI strings go through i18next, with Turkish as the default and English as a full translation.
- **Docker + reverse proxy** — frontend and backend run as containers; an Nginx gateway routes `receiptly.furkantekkartal.com` (prod) and `receiptly-dev...` (dev) to the right stacks.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*This document is part of the [ProjectReadmes](../) portfolio collection.*
