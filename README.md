# Furkan Tekkartal — Project Portfolio

Detailed, screenshot-driven documentation for every application running at [furkantekkartal.com](https://furkantekkartal.com). Each project page walks through every screen of the live app, with demo accounts you can try yourself.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

## Projects

| Project | What it is | Live app | Docs |
|---|---|---|---|
| 🥗 **HealthNHabits** | Health tracker with an AI food scanner: photograph a meal, get calories and macros | [Open](https://healthnhabits.furkantekkartal.com) | [English](HealthNHabits/README.md) · [Türkçe](HealthNHabits/README.tr.md) |
| 👗 **Wardrobe** | AI digital closet: auto-tagging, outfit canvas, weather-aware suggestions, virtual try-on | [Open](https://wardrobe.furkantekkartal.com) | [English](Wardrobe/README.md) · [Türkçe](Wardrobe/README.tr.md) |
| 🧾 **Receiptly** | Receipt scanner and household expense tracker with AI OCR | [Open](https://receiptly.furkantekkartal.com) | [English](Receiptly/README.md) · [Türkçe](Receiptly/README.tr.md) |
| 🎯 **HomeMadeKahoot** | Kahoot-style English learning platform with real-time multiplayer quizzes | [Open](https://homemadekahoot.furkantekkartal.com) | [English](HomeMadeKahoot/README.md) · [Türkçe](HomeMadeKahoot/README.tr.md) |
| 🔧 **Dükkanım** | Management system for Turkish auto repair shops: vehicles, service records, invoicing | [Open](https://dukkanim.furkantekkartal.com) | [English](Dukkanim/README.md) · [Türkçe](Dukkanim/README.tr.md) |
| 🏺 **Authentic Bazaar** | Zero-dependency vanilla-JS e-commerce storefront (demo shop) | [Open](https://authenticbazaar.furkantekkartal.com) | [English](AuthenticBazaar/README.md) · [Türkçe](AuthenticBazaar/README.tr.md) |
| 📊 **Exam Visualizer** | Mock-exam tracking: Excel result sheets become per-student dashboards and trend charts (login protected) | [Open](http://examvisualizer.furkantekkartal.com) | [English](ExamVisualizer/README.md) · [Türkçe](ExamVisualizer/README.tr.md) |

**Demo accounts:** every app that needs a login accepts username `demo`, password `demo1234`.

## How this ecosystem runs

All apps share one infrastructure, self-hosted on cloud VMs:

- Each project ships as **Docker containers** (separate dev and prod stacks).
- A single **Nginx gateway** routes `<project>.furkantekkartal.com` subdomains to the right container (`-dev` subdomains serve the development builds).
- A shared **PostgreSQL** instance holds a separate database per app and environment.
- AI features (food analysis, OCR, outfit recommendations, virtual try-on, quiz generation) run through OpenRouter, Gemini, Claude and FASHN APIs.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*All screenshots were taken on the live production apps using dedicated demo accounts.*
