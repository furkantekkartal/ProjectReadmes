# Wardrobe

An AI-powered digital wardrobe: photograph your clothes → the AI removes the background and auto-tags each piece → build outfits on a sticker canvas → get AI outfit recommendations with live weather → try garments on in a virtual try-on with your own photo.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Try it live
>
> **URL:** [https://wardrobe.furkantekkartal.com](https://wardrobe.furkantekkartal.com)
>
> **Demo login:** username `demo` · password `demo1234`
>
> **Note:** registration is **invite-only**. A new account needs an invite code from the owner, so please use the demo account to explore the app.

---

## Features

- **AI auto-tagging (Claude)** — upload one photo and the AI names the garment, picks its category, detects the main and secondary colors, and generates style tags.
- **Automatic background removal** — every clothing photo is cut out from its background (Photoroom / imgly), so the wardrobe looks like a clean product catalog.
- **Sticker outfit canvas** — compose outfits by dragging the cut-out garments on a canvas: one-finger drag, pinch to scale, layer controls.
- **Natural-language outfit recommender** — write one sentence ("I'm meeting friends for coffee...") and Claude suggests complete outfits from your own wardrobe, with reasoning, aware of the live weather in your city (OpenWeather).
- **Virtual try-on** — pick a photo of yourself, pick garments, pick an AI model (FASHN / Gemini), and see the clothes rendered on you.
- **Per-user AI credit system** — every AI call has a real USD price; each user has a credit balance and a monthly limit.
- **Invite-only access with admin tools** — admins mint single-use invite codes and top up user credits.
- **Built-in observability** — stats, an activity timeline, and a live log viewer right inside the app.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite 7, Tailwind CSS 4, React Router 7 |
| Backend | Node.js 20, Express 4, async AI job workers |
| Database | PostgreSQL (shared instance, separate dev/prod databases) |
| Auth | JWT, invite-gated registration |
| AI — tagging & outfits | Claude Sonnet |
| AI — virtual try-on | FASHN / Gemini (via OpenRouter) |
| AI — background removal | Photoroom / imgly |
| Weather | OpenWeather |
| Deployment | Docker Compose behind an Nginx reverse proxy |

## Screens

All screenshots are from the live app in a mobile viewport (390 px) — the UI is designed mobile-first. The interface is in Turkish, as this is an app for the Turkish market; each section below translates the key labels.

## Login

<img src="images/01-login.png" alt="Login screen" width="390">

- Pink-branded sign-in screen with the app logo and the tagline *"Akıllı dijital gardırop"* (smart digital wardrobe).
- You can log in with a username **or** an email address, plus a password.
- The link at the bottom asks *"Davet kodun var mı?"* — "Do you have an invite code?" — and leads to registration.
- Sessions use JWT tokens; logged-in users are redirected straight to the dashboard.

## Register

<img src="images/02-register.png" alt="Register screen" width="390">

- *"Hesap Oluştur"* (Create account) — registration is invite-only: the first field is the invite code (*Davet Kodu*, format `XXXX-XXXX`).
- The code is checked live against the server; only valid, unused codes pass.
- The rest is standard: full name, username, email, and a password of at least 6 characters.
- Invite codes are single-use and can only be created by an admin, which keeps the app private.

## Dashboard

<img src="images/03-dashboard.png" alt="Dashboard" width="390">

- The home screen greets the user by time of day (*"İyi akşamlar, demo"* — good evening, demo).
- Two stat cards show the wardrobe size: 4 *Parça* (pieces) and 2 *Kombin* (outfits).
- *"Son Eklenen Kıyafetler"* (recently added clothes) is a grid of the latest items — all already cut out from their backgrounds.
- *"Kombin Önerileri"* (outfit suggestions) is a horizontal row of saved outfit cards.
- A floating camera button adds a new garment from anywhere; the bottom bar has five tabs: *Ana Sayfa* (home), *Gardırop* (wardrobe), *Kombinlerim* (my outfits), *Dene* (try on), *Profil* (profile).

## Wardrobe

<img src="images/04-wardrobe.png" alt="Wardrobe grid" width="390">

- The full closet as a photo grid — *"4 / 4 parça"* means all 4 pieces are shown.
- A search bar (*"Kıyafet ara..."* — search clothes) plus category chips with live counts: *Tümü* (all), *Aksesuar* (accessories), *Dış Giyim* (outerwear), *Üst* (tops)...
- A filter drawer (top-right icon) adds tag and color filters.
- Every card shows the AI-generated name and category — for example *"Krem Beach baskılı t-shirt"* (cream Beach-print t-shirt), *Üst* (top).

## Clothing Detail

<img src="images/05-clothing-detail.png" alt="Clothing detail with AI tags" width="390">

- The garment is shown on a transparent checkerboard — proof of the automatic background removal.
- The name and category come from the AI and can be edited inline.
- *Etiketler* (tags) are AI-generated style chips — here *Rahat* (casual), *Plaj* (beach), *Yaz* (summer), *İlkbahar* (spring), *Renkli* (colorful) — with add/remove and an *"AI ile Yeniden Etiketle"* (re-tag with AI) button.
- *Renkler* (colors): the AI detected the main color *Krem* (cream) and secondary color swatches.
- Extra actions: *"Arka planı sil"* (remove background) and *"AI etiketle"* (AI tag) can be re-run on demand.

## Add Clothing

<img src="images/06-clothing-add.png" alt="Add clothing" width="390">

- *"Kıyafet Ekle"* (add clothing): take a photo or pick one from the gallery.
- The hint says it best: *"Düz arka planda, tek bir kıyafet fotoğrafı. AI otomatik etiketleyecek."* — one garment on a plain background; the AI will tag it automatically.
- Uploading starts an async pipeline: photo compression → background removal → Claude garment analysis → tag generation.
- The job runs in the background on the server; the UI animates through the stages and the finished item lands in the wardrobe.

## Outfits

<img src="images/07-outfits.png" alt="Outfits list" width="390">

- *"Kombinlerim"* (my outfits) lists saved outfits as collage cards built from the cut-out garments.
- Each card shows the outfit name, piece count and an occasion label — *Günlük* (everyday), *Özel gün* (special day).
- Filter between *Tümü* (all) and *Favoriler* (favorites); the heart on each card toggles favorite status.
- Search works on both outfit names and occasions.
- The **+** button opens the canvas builder; the sparkle button jumps to the AI recommender.

## Outfit Canvas

<img src="images/08-outfit-canvas.png" alt="Outfit canvas builder" width="390">

- The signature builder: a 3:4 canvas where background-free garments behave like stickers.
- Move each piece with one finger, pinch to resize, and reorder layers — here the cream Beach t-shirt is composed over petrol green shorts.
- The outfit gets a name (*"Günlük Kombin"* — daily outfit) and an occasion (*"Günlük"* — casual).
- *"Kullanılan Kıyafetler (3)"* (used clothes) lists the pieces with quick remove buttons and an *Ekle* (add) picker filtered by category.
- *Güncelle* (update) saves the composition; the same screen edits existing outfits.

## AI Outfit Recommender

The flagship AI feature. You describe your plan in one sentence, and Claude builds outfits from the clothes you actually own.

### 1. Input

<img src="images/09-ai-input.png" alt="AI recommender input" width="390">

- *"AI Kombin Önericisi"* (AI outfit recommender) — *"Aklındaki bir cümlede yaz"* (write what's on your mind in one sentence).
- The gradient card names the model: **Claude Sonnet** analyzes your wardrobe and suggests personalized outfits.
- Example prompt filled in: *"Yarın arkadaşlarımla dışarı çıkıyorum, rahat ve sportif bir kombin önerir misin?"* — "I'm going out with friends tomorrow, can you suggest a casual, sporty outfit?"
- An optional city field (here *Istanbul*) makes the suggestion weather-aware via OpenWeather.
- Example sentences below (*"Pikniğe gidiyorum..."* — I'm going on a picnic...) help first-time users.

### 2. Result

<img src="images/10-ai-result.png" alt="AI recommender result with live weather" width="390">

- The job runs asynchronously; a toast announces *"AI öneri hazır"* (AI suggestion ready).
- A live weather chip shows the forecast used: **"Karaköy: 27°C, açık"** (27°C, clear).
- The AI returns named outfits — the first is *"Sahil Enerjisi Kombini"* (Beach Energy outfit) with full reasoning in Turkish: the cream printed t-shirt and petrol green shorts make an eye-catching, fully casual-sporty look for the outdoors.
- Every suggestion is composed only of real items from the user's wardrobe, shown as thumbnails.
- A *"Bu Kombini Kaydet"* (save this outfit) button turns any suggestion into a saved outfit.

## Virtual Try-On

Pick a photo of yourself, pick garments, and the AI renders you wearing them.

### 1. Setup

<img src="images/11-tryon.png" alt="Virtual try-on setup" width="390">

- *"Sanal Deneme"* (virtual try-on) — the header shows the credit balance: *"Bakiye: $2.00 • ~50 deneme hakkı"* (balance $2.00, about 50 tries left).
- Step 1: choose one of your own body photos (*"Fotoğrafını seç"*).
- Step 2: choose the garments to try (*"Denemek istediğin kıyafetler"*) — multiple selection is allowed (top + bottom), and each extra garment costs one extra try.
- Step 3: choose the AI model — *Gemini 2.5 Flash* is the default (*Varsayılan*), "fast and economical" at $0.040 per try.

### 2. In Progress

<img src="images/12-tryon-progress.png" alt="Virtual try-on in progress" width="390">

- The model list with transparent pricing: Gemini 2.5 Flash $0.040, Gemini 3.1 Flash $0.070, Gemini 3 Pro Image $0.150 ("highest quality"), ChatGPT Image $0.120.
- *"Tahmini maliyet"* (estimated cost) is calculated before you start: $0.040 for 1 garment.
- The job runs in the background — the purple banner says *"1 işlem arka planda çalışıyor"* (1 job running in the background).
- You can leave the page and keep using the app; a notification arrives when the result is ready.

### 3. Result

<img src="images/13-tryon-result.png" alt="Virtual try-on result" width="390">

- The demo's cream Beach t-shirt is rendered onto the user's own mirror photo — pose, room and lighting are preserved.
- A toast announces *"Sanal deneme hazır"* (virtual try-on ready); the balance has dropped to $1.92 (~48 tries).
- *İndir* (download) saves the image; *Yeni Dene* (try again) starts a new run.
- *"Geçmiş Denemeler"* (past tries) keeps a history as "photo + garment = result" rows with timestamps and delete.

## Statistics

<img src="images/14-stats.png" alt="Statistics" width="390">

- *"İstatistikler"*: totals at the top — 4 *Kıyafet* (clothes), 2 *Kombin* (outfits), 0 *Favori* (favorites).
- *"Kategori Dağılımı"* (category distribution) draws a bar per category: tops 2, bottoms 2.
- *"AI Kullanımı (Bu Ay)"* (AI usage this month) counts tagging runs, recommendations and try-ons — and their real total cost ($0.097).
- The cost figure comes straight from the per-call credit accounting in the backend.

## Activity

<img src="images/15-activity.png" alt="Activity timeline" width="390">

- *"Hareketler"* (activity) is a date-grouped timeline of everything that happened in the account.
- Event types include *"Sanal deneme yapıldı"* (virtual try-on done), *"AI kombin önerisi istendi"* (AI outfit suggestion requested) and *"... gardıroba eklendi"* (... added to the wardrobe).
- Events carry image thumbnails that open in a lightbox — you can see exactly which garment or result each entry refers to.
- Timestamps make it easy to retrace a whole session.

## Logs

<img src="images/16-logs.png" alt="Log viewer" width="390">

- *"Loglar"* — a real log viewer inside the app, useful for a solo developer running AI pipelines in production.
- Filter by level (*error / warn / info / debug*) and by source (*http, fashn, claude, photoroom...*).
- The entries show real pipeline telemetry — for example `claude recommend.success 9937ms outfits=3` (the recommendation call took ~10 s and returned 3 outfits).
- Regular users see their own logs; admins can switch the scope to all users.

## Profile

<img src="images/17-profile.png" alt="Profile" width="390">

- The user card shows the avatar, display name and handle (*demo @demo*).
- Quick links lead to *İstatistikler* (statistics), *Hareketler* (activity) and *Hata Logları* (error logs).
- *"AI Bakiyem (OpenRouter)"* (my AI balance) is the credit dashboard: $3.46 left, $10.00 loaded in total, $6.544 spent, and a monthly limit of $3.00.
- *"Çıkış Yap"* logs out.
- Admin accounts see extra sections here (not visible on the demo account): creating and sharing invite codes, and topping up other users' AI credits.

## Architecture

- **Mobile-first SPA** — a React single-page app with a phone-width layout and a bottom tab bar, served by Nginx.
- **REST API + async job polling** — the Express backend exposes JSON endpoints; slow AI work (tagging, recommendations, try-on) runs as background jobs, and the frontend polls until a "ready" toast appears. The user can keep navigating while a job runs.
- **Shared PostgreSQL** — data lives in a shared Postgres instance with separate dev and prod databases; schema migrations run automatically on backend startup.
- **Per-user uploads on a Docker volume** — original photos, background-removed cutouts and try-on results are stored per user on a persistent volume, outside the containers.
- **Credit accounting per AI call** — every provider call (Claude, FASHN/Gemini, background removal) is priced in USD and charged against the user's balance, with monthly limits and admin top-ups.
- **Docker Compose behind Nginx** — separate dev and prod stacks; the reverse proxy routes `wardrobe.furkantekkartal.com` (prod) and `wardrobe-dev...` (dev) to the right containers.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*This document is part of the [ProjectReadmes](../) portfolio collection.*
