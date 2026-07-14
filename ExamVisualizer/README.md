# Exam Visualizer (Deneme Takip Sistemi)

A web app for tracking students' mock-exam (deneme) results: upload the Excel result sheets that exam companies produce, and explore per-student dashboards with score trends, subject-level breakdowns and school/branch rankings across exams.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Live app
>
> **URL:** [http://examvisualizer.furkantekkartal.com](http://examvisualizer.furkantekkartal.com)
>
> **Login protected.** The app holds real student data (names, national ID numbers, photos), so there is no public demo account — every API endpoint and student photo requires an authenticated session.
>
> All screenshots below were taken from an instance seeded with **anonymized demo data** (fake names and ID numbers); no real student information appears in this document.

---

## Features

- **Drag-and-drop Excel upload** — drop the `.xlsx` result sheets straight into the app; files are stored on the server and reloaded automatically on restart.
- **Student list with filters** — search by national ID, school number, name or class/branch, per exam.
- **Per-student dashboard** — score bars (overall / numerical / verbal), class–school–general ranks with movement indicators, participant counts, subject score cards.
- **Progress across exams** — line, bar, radar and composed charts (Recharts) showing how each student trends over the exam series, per subject.
- **Subject analysis** — correct / wrong / empty / net breakdowns for Turkish, Maths, Science, History, English and Religion.
- **School & branch parsing** — free-form class labels like `OZL 8/D` or `8-E KZY` are parsed into school, grade and branch automatically.
- **Student photos** — shown on the student dashboard when a photo matching the ID exists (auth-protected endpoint).
- **Usage logging** — server-side tracking of sessions and actions with CSV/JSON export, plus optional Telegram notifications.
- **Single-login access control** — SHA-256-hashed credentials via environment variables; one login grants a persistent session token that guards every API route.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 (CRA), React Router 6, Recharts, Tailwind CSS |
| Backend | Node.js, Express 4, multer uploads, SheetJS (xlsx) parsing |
| Storage | File-based: Excel sheets + photos on a persistent Docker volume (no database) |
| Auth | SHA-256 hashed credentials, persistent session token, all endpoints guarded |
| Deployment | Docker (multi-stage build) behind an Nginx reverse proxy |

## Screens

Desktop screenshots are 1440 px, mobile 390 px. The UI is in Turkish. **All data shown is anonymized demo data.**

### Login

The whole app sits behind this screen — without a valid session, every API call (including student photos) returns 401.

<img src="images/01-login.png" alt="Login screen" width="800">

### Student list

Pick an exam, filter by ID / school number / name / branch, and jump to any student's dashboard.

<img src="images/02-dashboard.png" alt="Student list" width="800">

Filtering by name:

<img src="images/03-dashboard-filtered.png" alt="Filtered student list" width="800">

### Student dashboard

Rank movement, score bars, exam-wide participation stats and subject averages at a glance:

<img src="images/04-student-dashboard.png" alt="Student dashboard" width="800">

The full page adds per-subject performance rings, a radar chart and progress-over-time charts:

<img src="images/04b-student-dashboard-full.png" alt="Student dashboard - full page" width="800">

### Excel upload

<img src="images/05-upload.png" alt="Upload page" width="800">

### Mobile

<p>
<img src="images/06-mobile-dashboard.png" alt="Mobile student list" width="300">
<img src="images/07-mobile-student.png" alt="Mobile student dashboard" width="300">
</p>

## Architecture notes

- The backend parses each uploaded workbook once and keeps the processed exam data in memory; the original files persist in `storage/excel` and are re-parsed on startup.
- Runs as two containers (`examvisualizer-backend`, `examvisualizer-frontend`); the frontend Nginx proxies `/api` and `/images` to the backend, and the shared gateway routes the `examvisualizer.` subdomain to it.
- Storage, uploads and logs live on host volumes under the shared infrastructure data folder, so containers can be rebuilt without losing data.
