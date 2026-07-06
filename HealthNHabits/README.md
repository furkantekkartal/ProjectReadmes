# HealthNHabits

A mobile-first web app for tracking food, water, steps and weight — with an AI food scanner that turns a photo of your meal into calories and macros.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Try it live
>
> **URL:** [https://healthnhabits.furkantekkartal.com](https://healthnhabits.furkantekkartal.com)
>
> **Demo login:** username `demo` · password `demo1234`
>
> You can also create your own account — registration is open to everyone.

---

## Features

- **AI food analysis** — take a photo of your meal (or just describe it in text) and the AI detects the foods, estimates portions and calculates calories and macros.
- **Daily dashboard** with an interactive balance-scale visualization of calories burned vs. consumed.
- **Food catalog** — a personal product library with per-item calories and macros, one-tap logging by meal type.
- **Hydration, steps and weight tracking**, each with its own goal and progress view.
- **Energy gap analysis** — daily calorie deficit/surplus (BMR + activity vs. food) with a projected weekly weight change.
- **Progress reports** — multi-day charts for energy gap, hydration, steps and weight over 7 / 14 / 30 days.
- **Personal profile** with body data, activity level, and an automatic BMR / TDEE calculation that drives the daily goals.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite, Tailwind CSS 4, React Router 7 |
| Backend | Node.js, Express 5, Sequelize ORM |
| Database | PostgreSQL |
| Auth | JWT (username + password, bcrypt hashing) |
| AI | OpenRouter AI for food photo / text analysis |
| Deployment | Docker Compose behind an Nginx reverse proxy |

## Screens

All screenshots are from the live app in a mobile viewport (390 px) — the UI is designed mobile-first.

## Login

<img src="images/01-login.png" alt="Login screen" width="390">

- Simple sign-in with username and password — no email needed.
- Show/hide toggle on the password field.
- App logo and a short "Sign in to continue tracking" message keep the screen clean.
- A "Sign up" link at the bottom leads to open registration.

## Register

<img src="images/02-register.png" alt="Register screen" width="390">

- Anyone can create an account: username, password and password confirmation.
- Inline hints show the rules: at least 3 characters for the username, at least 6 for the password.
- After a successful sign-up the app logs you in automatically.
- A "Login" link takes existing users back to the sign-in page.

## Dashboard

<img src="images/03-dashboard.png" alt="Dashboard" width="390">

- The home screen greets the user by name and shows one full day at a glance.
- A date navigator at the top lets you browse back through past days.
- The centerpiece is the **Energy Gap Insights** card: an animated balance scale that weighs calories burned (2,970) against calories consumed (1,558) and shows the net gap (1,412 kcal ≈ −183 g fat) with a status label ("Excellent").
- A water intake bar shows daily progress toward the hydration goal (1,530 / 2,500 ml).
- Macro bars track carbs, protein, fat and fiber against personal targets.
- Further down the page there are calories, steps and weight summary cards; the floating camera button opens the AI food scanner from anywhere.

## AI Food Analysis

The flagship feature. You give the app a photo, a text description, or both — and it returns a full nutrition breakdown you can log with one tap.

### 1. Input

<img src="images/07-ai-analysis.png" alt="AI food scan input" width="390">

- The **AI Food Scan** page accepts a camera photo or an uploaded image.
- A small tip banner explains a practical trick: put your thumb in the photo for scale, so portion estimates are more accurate.
- You can also skip the photo and just type what you ate (e.g. "KFC Zinger Burger" or "2 eggs with cheese").

### 2. Ready to analyze

<img src="images/08-ai-analysis-ready.png" alt="AI food scan ready" width="390">

- The attached photo (avocado toast with cheese and boiled eggs) is shown as a preview, with an X to remove it.
- The text description can be edited before analysis to give the AI extra context.
- One tap on **Analyze with AI** sends both the image and the text to the backend.

### 3. Result

<img src="images/09b-ai-analysis-result-full.png" alt="AI food scan result" width="390">

- A "Scan complete" badge appears over the photo and the AI suggests a meal name ("Avocado toast and eggs").
- The total card sums it up: 480 kcal, 32 g protein, 48 g carbs, 16 g fat, 3 g fiber.
- **Detected Items** lists each food separately — whole grain toast, mashed avocado, hard-boiled eggs, sliced cheese — with its own calories, macros and a gram-based portion stepper you can adjust.
- Every item can be edited or removed, and missing foods can be added from the catalog.
- You pick the meal type (breakfast / lunch / dinner / snack) and press **Save as Meal** to log it.

## Product Catalog

<img src="images/04-catalog.png" alt="Product catalog" width="390">

- A personal food library: every product shows its portion size, calories and P/C/F macros.
- The meal-type selector at the top decides where a food is logged (breakfast, lunch, dinner or snack).
- Search plus category chips (Meal, Fruit, Coffee, Snack…) make it quick to find items.
- The green **+** button logs a product to the selected day and meal in one tap.
- **+ New** creates a new product; the camera button jumps to the AI scanner.

## Meal Detail / Edit

<img src="images/05-product-detail.png" alt="Meal detail and edit" width="390">

- A saved meal (here: a latte) opens in an edit view with its picture, name and totals.
- The total card shows 150 kcal with protein, carbs, fat and fiber values.
- The meal type can be changed with the same four-button selector.
- Items inside the meal can be edited, deleted or extended with **Add Item**.
- **Save as Meal** stores the changes back to the log.

## Add Product

<img src="images/06-add-product.png" alt="Add product form" width="390">

- New catalog items can be created by hand or with help from AI.
- **Quick Add with AI**: type something like "1 large banana" and the AI fills in the name, category, portion and macros automatically.
- A photo can be attached to the product.
- Manual fields cover product name, category, portion size and unit; calorie and macro fields follow below.

## Hydration

<img src="images/10-hydration.png" alt="Hydration tracker" width="390">

- A large progress ring shows today's water intake: 1,530 ml, 61% of the daily goal.
- Motivational messages change with your progress ("Keep it up! You're halfway there.").
- Quick-add tiles log a glass or a bottle with one tap; a custom amount input covers everything else.
- Small minus buttons on the tiles undo a tap; the date bar lets you check past days.

## Steps

<img src="images/11-steps.png" alt="Steps tracker" width="390">

- A progress ring shows 4,888 steps against the daily goal of 10,000.
- The app estimates distance (3.61 km) and calories burned (241 kcal) from the step count.
- Steps are entered manually with a large on-screen number pad.
- The date bar at the top allows logging steps for previous days.

## Log Weight

<img src="images/12-weight.png" alt="Weight entry" width="390">

- A big, readable display shows the current entry (86.2 kg); tap it to type a value directly.
- A scroll picker with plus/minus buttons adjusts the weight in 0.1 kg steps.
- A trend chip gives instant feedback: "0.3 kg down since 7 days ago", with the start weight below.
- The date selector supports backdated entries, and a **History** link opens the full record.

## Weight History

<img src="images/13-weight-history.png" alt="Weight history" width="390">

- The summary card shows minimum, current and maximum weight, plus a live BMI value with its category (BMI 27.2 · Overweight).
- **Weight Change** chips summarize the trend over 7 days, 2 weeks, 1/3 months and 1 year.
- Every measurement is listed with its date and the difference from the previous entry.

## Activity Log

<img src="images/14-activity-log.png" alt="Activity log" width="390">

- A chronological timeline of everything logged on the selected day.
- Swipeable stat cards at the top summarize the day: calories (1,558 kcal), protein (92.5 g), steps.
- Food entries show the meal type, product name, calories and timestamp.
- Water, steps and weight entries appear in the same timeline further down.
- Each entry can be edited or deleted in place; the **+** button adds a new one.

## Energy Gap Analysis

<img src="images/15-energy-gap.png" alt="Energy gap analysis" width="390">

- A focused view of the day's energy balance: net gap of −1,412 kcal.
- The estimate is translated into something practical: "Estimated Loss: 1.3 kg/week".
- An IN vs. OUT bar chart compares food intake (1,558 kcal) with total burn (2,970 kcal), split into resting metabolism (BMR) and activity.
- A **Weekly Projection** card repeats the expected weight change per week.

## Progress Reports

<img src="images/16-reports.png" alt="Progress reports" width="390">

- Multi-day charts with a 7d / 14d / 30d period switch.
- **Energy Gap**: daily deficit/surplus bars with the period total (−16,500 kcal) and daily average (−1,179 kcal).
- **Hydration**: daily bars against a goal line, with total (31.5 L) and average (2.2 L) — days that hit the goal are highlighted.
- **Steps**: the same pattern for steps (139.2k total, 9.9k average per day).
- A weight trend chart follows below the fold.

## Profile Settings

<img src="images/17-profile.png" alt="Profile settings" width="390">

- Personal data that powers all calculations: display name, gender, birth year, height and weight.
- A profile photo can be uploaded and cropped.
- Below the fold: an activity-level selector (Sedentary ×1.2 up to Very Active ×1.7) and an automatic **TDEE card** that explains the math — BMR 1,820 kcal × activity factor = 2,730 kcal daily energy.
- Password change and logout live at the bottom of the same page.

## Architecture

- **Mobile-first SPA** — a React single-page app with a centered, phone-width layout and a bottom tab bar.
- **REST API** — the Express backend exposes JSON endpoints; the frontend talks to it with JWT-authenticated requests.
- **Shared PostgreSQL** — data lives in a shared Postgres instance, with separate databases for dev and prod.
- **Docker containers** — frontend and backend run as containers, with separate dev and prod stacks.
- **Reverse proxy** — an Nginx gateway routes subdomains (`healthnhabits.furkantekkartal.com` for prod, `healthnhabits-dev...` for dev) to the right containers.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*This document is part of the [ProjectReadmes](../) portfolio collection.*
