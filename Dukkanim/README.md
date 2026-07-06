# Dükkanım

A management app for Turkish auto repair shops — vehicles, service jobs, appointments, customer accounts and shop finances in one place.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Try it live
>
> **URL:** [https://dukkanim.furkantekkartal.com](https://dukkanim.furkantekkartal.com)
>
> **Demo login:** username `demo` · password `demo1234`
>
> The demo account has the owner role (**Yönetici**), so all nine tabs are visible. Registration exists, but it requires an authorization code from the shop owner — please use the demo account.

---

The UI is entirely in Turkish, because the app is built for Turkish auto repair shops (*sanayi*). In this document the key labels are translated inline.

## Features

- **Vehicle registry with photos** — when you add a car, the plate field autocompletes from existing customer records, and make / model / engine come from a built-in car database.
- **Service records** — each vehicle keeps dated service records; jobs are picked from operation templates and priced line by line (labor + material) with 18% VAT (KDV).
- **Appointment calendar** with day / week / month views on a working-hours grid that follows the shop settings.
- **Customer accounts (cari)** — one account per customer and plate, with a balance computed from jobs and payments.
- **Consumables catalog** — materials and labor prices with categories, stock counts and search.
- **Expense tracking** — monthly timeline with automatic recurring expenses and a category distribution bar.
- **Accounting overview** — every job with its payment state: paid, unpaid or overdue.
- **Personnel management** — a daily job log for each mechanic, with completed / total counters.
- **Role-based access** — the owner (*usta*) sees everything; a mechanic (*tamirci*) sees only the vehicle screens and their own profile.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite, Tailwind CSS 4 |
| Backend | Node.js, Express (~55 REST endpoints) |
| Database | PostgreSQL 16 |
| Auth | JWT (username + password, bcrypt hashing) |
| Uploads | multer + sharp for vehicle and shop photos |
| Deployment | Docker Compose (dev/prod) behind an Nginx reverse proxy |

## Screens

All screenshots are from the live app in a desktop viewport (1440 px). The demo shop **"Arya Mekanik Garaj"** is pre-loaded with realistic data: 13 vehicles with real photos, service records, customer accounts, appointments and expenses.

## Login

![Login screen](images/01-login.png)

- A single login card with a garage photo banner and the app subtitle: *Tamirci Takip Sistemi* (Mechanic Tracking System).
- Sign in with username (*Kullanıcı Adı*) and password (*Şifre*) — no email needed.
- The *Kayıt Ol* (Sign up) link at the bottom leads to registration.

## Register

![Register screen](images/02-register.png)

- The form asks for a username, first and last name, and a password with confirmation (show/hide toggle included).
- *Rol Seçiniz* (Choose your role) offers the two roles: owner or mechanic.
- After choosing a role, the form asks for an authorization code (*Yetki Şifresi*) that only the shop owner can share — this keeps registration closed to strangers, so visitors should use the demo account instead.

## Vehicle List (Araçlar)

![Vehicle list](images/03-araclar.png)

- The landing tab after login, and the one screen every role can see.
- Each card shows a real photo of the car, its model, a Turkish-style plate badge, the owner's name and a status badge — *Devam Ediyor* (In progress) in yellow or *Tamamlandı* (Completed) in green.
- A small corner badge (like *2 kayıt* — 2 records) appears when the same car has more than one record.
- The search bar filters by plate, model or owner; the *Aktif* toggle hides passive vehicles; *Araç Ekle* (Add vehicle) opens the add form, where the plate autocompletes from customer records and make / model / engine come from the built-in car database.

## Vehicle Detail (Araç Detay)

![Vehicle detail](images/04-arac-detay.png)

- The core screen of the app. A hero photo with the current status badge, the full identity of the car — *Toyota Auris, 1.33L Dual VVT-i (99 BG), 2011 Model* — plus plate and owner.
- *Teknik Detaylar* (Technical details) is an expandable panel with the car's specs.
- The *Servis Kaydı* (Service record) selector switches between dated records — each one is named by date and plate (e.g. `31.03.2026_16FR183`).
- A *Notlar* (Notes) card holds free-form notes about the vehicle ("White. Exhaust noise, needs checking").
- Below, *Yapılacak İşlemler* (Jobs to do) lists the operations of the selected record; new jobs are added from a template catalog.

![Service record pricing and payments](images/04b-arac-detay-islemler.png)

- Scrolling down reaches the money side of a service record. **Ücretlendirme** (Pricing) shows every job line with its labor (*işçilik*) and material (*malzeme*) amounts, an optional 18% VAT (KDV) toggle, and the grand total.
- One tap turns the quote into a **PDF** or sends it to the customer over **WhatsApp**.
- **Tahsilat** (Collection) tracks the record's total debt, the amount collected and the open balance, with each payment listed by method (here: cash, ₺2,670) — the record is marked *Ödeme Alındı* (payment received).

## Appointments (Randevu)

![Appointment calendar - week view](images/05b-randevu-hafta.png)

- The week view: an 08:00–18:00 grid (the hours follow the shop's working-hours setting) with color-coded appointment blocks, each labeled with the plate and time range.
- The header switches between *Gün / Hafta / Ay* (Day / Week / Month), and *Yeni Randevu* creates a new appointment.

![Appointment calendar - day view](images/05-randevu.png)

- The day view shows each appointment as a card: time range, plate, customer name and phone, the vehicle, the planned job (e.g. *Periyodik bakım* — periodic maintenance) and a *BEKLİYOR* (Waiting) badge.
- On the right, a mini month calendar marks busy days with dots, and *Bugünün Randevuları* (Today's appointments) lists the day at a glance.

## Customer Accounts (Cari Hesaplar)

![Customer accounts](images/06-cari.png)

- One row per customer: initials avatar, name, a short note (e.g. *"Düzenli müşteri"* — regular customer), phone number, plate badge and the account balance (*Bakiye*).
- The balance is tracked per plate and computed from the customer's jobs and recorded payments — in the demo shop all accounts are settled at ₺0.
- Search works across name, plate, phone and brand; *Cari Ekle* adds a new customer, and each row has edit / delete actions.

## Consumables (Sarf Malzeme)

![Consumables catalog](images/07-malzeme.png)

- The shop's price and stock catalog, split into two main groups: *Malzeme* (materials) and *İşçilik* (labor).
- Category chips with live counts filter the list: *Sarf* (consumables), *Motor Yağı* (motor oil), *Filtre* (filters), *Fren* (brakes), *Diğer* (other).
- The table lists each item with its category, stock count and price; a side panel shows the details of the selected item.
- *Yeni Ekle* (Add new) creates an item and *Dışa Aktar* (Export) exports the catalog.

## Expenses (Giderler)

![Expense timeline](images/08-giderler.png)

- *Gider Zaman Çizelgesi* (Expense timeline) shows one month at a time, with arrows to move between months.
- Summary cards on top: total spending (₺134,000 in the demo month), rent & bills, personnel and materials.
- *Kategori Dağılımı* (Category distribution) draws the month as a single stacked bar with a percentage legend — salaries 35%, rent 30%, personnel 13%, materials 9% and so on.
- Below, expenses appear on a timeline; fixed recurring items like salaries and the internet bill are added automatically and marked *Sabit* (fixed).

## Accounting (Muhasebe)

![Accounting overview](images/09-muhasebe.png)

- The money view of all service jobs: *Ödenmiş Toplam* (total collected — ₺27,738), *Bekleyen Ödemeler* (pending payments — ₺36,440 across 8 jobs) and *Toplam Borç Tutarı* (total open debt).
- Status tabs split the jobs into *Ödenmiş* (paid), *Ödenmemiş* (unpaid) and *Vadesi Geçmiş* (overdue), and the search bar finds a job by plate, customer or service.
- The table lists customer / vehicle, the service lines, date, amount and a status badge per row (*Ödendi* — paid — in the screenshot).

## Personnel (Personel Yönetimi)

![Personnel job log](images/10-personel.png)

- *Teknik İş Kaydı* (Technical job log) — the daily activity of the team.
- The left panel lists the staff with their role (*Usta Başı* — head mechanic, *Kalfa* — journeyman), online state and counters: completed vs. total jobs.
- Selecting a person shows their job history on the right, grouped by date — each entry has the plate, the vehicle model and a status badge (*SERVİS* / *TAMAMLANDI*).
- Two independent search bars: one for people, one for activity by plate, model or job.

## Profile & Shop Settings (Profil)

![Profile and shop settings](images/11-profil.png)

- The personal card at the top: avatar with photo upload, `@demo` username, role badge (*Yönetici*), name fields and a password change form.
- *Dükkan Bilgileri* (Shop info) belongs to the owner: shop name, rating (5.0, 1 review), address with an *Haritada Aç* (Open in map) link and a location preview.
- The shop settings feed the rest of the app — the sidebar branding and the appointment calendar's working hours come from here.

*The first sidebar tab, **Panel** (dashboard), is still under construction — shop-wide summary statistics are planned as the next step.*

## Architecture

- **Stateful SPA** — one React single-page app with a desktop sidebar; screens are tabs and stacked views under a single URL, with no URL router.
- **REST API** — the Express backend exposes about 55 JSON endpoints; the frontend talks to it with JWT-authenticated requests.
- **Role-based UI** — the owner (*usta*) gets all nine tabs; a mechanic (*tamirci*) gets a reduced interface with vehicles and profile only.
- **Shared PostgreSQL** — data lives in a shared Postgres 16 instance with separate dev and prod databases; SQL migrations run automatically at backend startup.
- **Docker + reverse proxy** — frontend and backend run as containers in separate dev and prod stacks; an Nginx gateway routes `dukkanim.furkantekkartal.com` to the right containers.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*This document is part of the [ProjectReadmes](../) portfolio collection.*
