# HomeMadeKahoot

A Kahoot-style English-learning platform: build quizzes by hand or with AI, host live multiplayer sessions that players join with a 4-digit PIN, and study vocabulary with flashcards, spelling practice and a 13,000+ word English–Turkish database.

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

---

> ### 🚀 Try it live
>
> **URL:** [https://homemadekahoot.furkantekkartal.com](https://homemadekahoot.furkantekkartal.com)
>
> **Demo login:** username `demo` · password `demo1234`
>
> You can also create your own account — registration is open (username + password only, no email).
>
> Players don't need an account at all: joining a live quiz only takes a 4-digit PIN and a nickname.

---

## Features

- **Live multiplayer quizzes** — the flagship feature. A host opens a lobby with a 4-digit PIN, players join from any device as guests, questions run in real time over Socket.IO with a countdown, points and a final leaderboard.
- **Quiz builder with AI import** — write questions by hand, or generate them from a PDF, a subtitle file (SRT/TXT) or a webpage/YouTube URL. Question images can be generated automatically.
- **Self-paced mode** — any quiz can also be taken alone, without a host.
- **Word database** — 13,000+ English–Turkish entries based on the Oxford-3000 list, with word type, CEFR level, categories, import/export and per-word learning status.
- **Flashcard decks** — flip cards with the English word, Turkish meaning, a sample sentence, audio buttons and a photo; mark each word as Learning or Known.
- **Spelling practice** — see the Turkish word, type the English one; progress is tracked per deck.
- **Pronunciation assessment** — speech scoring through Azure Speech, with an average pronunciation score in the analytics.
- **Dashboards and analytics** — levels, badges, study time and per-student quiz performance, visualized with Recharts.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 (CRA), React Router v6, Recharts, socket.io-client |
| Backend | Node.js, Express, Socket.IO |
| Database | PostgreSQL, Sequelize ORM |
| Auth | JWT (username + password, bcrypt hashing) |
| Real-time | Socket.IO game sessions with 4-digit PINs |
| AI & content | OpenRouter / Gemini (quiz generation), Unsplash (question images), Firecrawl (webpage extraction), Azure Speech (pronunciation) |
| Deployment | Docker Compose behind an Nginx reverse proxy |

## Screens

All screenshots are from the live app in a desktop viewport (1440 px), using a freshly created demo account. The demo content is small on purpose: a 10-word deck ("Basic English A1"), a 5-question quiz ("English Basics Quiz") and one played live session — so some counters still show zeros.

## Home (Guest)

![Guest landing page](images/01-home-guest.png)

- The public landing page: hero banner "Learn English the Fun Way!" with a short pitch about quizzes, live sessions and gamification.
- A green **Join Quiz** button is the main call to action — visitors can jump straight into a live game.
- Four feature cards summarize the platform: Create Quizzes, Live Sessions, Learn English and Track Progress.
- Login and Sign Up live in the top-right corner.

## Login

![Login screen](images/02-login.png)

- Simple sign-in with username and password — no email needed.
- A "Sign up" link below the form leads to open registration.

## Register

![Register screen](images/03-register.png)

- Anyone can create an account: username, password and password confirmation.
- After registration you get the full toolset — decks, quizzes, hosting and analytics.

## Dashboard

![Dashboard](images/05-dashboard.png)

- The logged-in home screen: stat cards for Total Words (13,321 in the shared database), flashcard progress (Known/Learning), spelling results and study time.
- **Your Current Level** shows a level badge ("Starter" for a fresh account) with a progress bar based on known words.
- **Badges Earned** displays gamification badges: level badges, word badges (every 1,000 words), study-time badges (every 5 hours) and a total.
- A **Quick Stats** rail on the right summarizes mastery rate, study streak, current level, badges and flashcard progress.
- The sidebar gives access to every module: Game, Deck/Quiz, Flashcards, Spelling, Words and Performance.

## Deck / Quiz Hub

![Deck and quiz hub](images/06-deck-quiz-hub.png)

- The content hub with two tabs — **Decks** and **Quizzes** — plus a **+** button to create new ones.
- The demo deck **Basic English A1** (10 cards, "Everyday English words with Turkish meanings for beginners") sits next to ready-made Oxford decks by CEFR level: A1, A2, B1 and B2 with 1,180 to 3,672 cards each.
- Every card shows Level / Skill / Task tags and counters for cards, known and spelled words.
- Action buttons on each deck open flashcards or spelling practice, or view, edit and delete the deck.
- Dropdown filters (level, skill, task) and a hide toggle keep large collections manageable.

## Create Quiz

![Create quiz page](images/07-create-quiz.png)

- Quizzes can be created two ways on the same page.
- **Import from Source** — the AI panel: upload a PDF, SRT or TXT file, or paste a webpage/YouTube URL, then press **Run** to generate questions automatically.
- **Quiz Information** — the manual path: title, description and Level / Skill / Task settings, then questions are added one by one.
- The create button shows the live question count ("Create Quiz (0 questions)").

## Edit Quiz

![Edit quiz page](images/08-edit-quiz.png)

- The demo quiz **English Basics Quiz** ("A beginner-friendly quiz on basic English vocabulary", level A1) opened in the editor.
- Quiz metadata (title, description, level, skill, task) is edited at the top and saved with one button.
- All 5 questions are editable in place: question text, four options (one per line), the correct answer index, points (100) and a time limit per question (20 seconds).
- Questions mix directions — Turkish meaning of an English word ("apple" → elma) and English word for a Turkish one ("kitap" → book).

## Live Multiplayer Quiz

The flagship feature. The host starts a session and gets a PIN; players join from their own devices — no account needed — and answer in real time while the leaderboard updates over Socket.IO.

### 1. Host opens the lobby

![Host lobby with PIN](images/12-host-lobby.png)

- Hosting "English Basics Quiz" creates a session with a game PIN (**8221**) and a live connection indicator.
- The lobby shows "Waiting for participants…" and the PIN to share with the group.
- Joined players appear in the participants list in real time — here the guest player **Ayşe** has arrived.
- The host launches the game with **Start Quiz**.

### 2. Player waits in the game room

![Player waiting room](images/13-player-join.png)

- After entering the PIN, the player lands in a waiting room: "You're all set! The host will start the quiz soon."
- A quiz info card shows what's coming: English Basics Quiz, Level A1, Skill Reading, Task Vocabulary.
- Note the guest navbar — this player joined without any account.

### 3. Players answer live

![Player question screen](images/14-player-question.png)

- When the host starts, questions appear on every player's screen at the same time.
- A status bar shows the running score, the question number (1 of 5) and a red countdown (16s left of the 20-second limit).
- Answers use Kahoot-style colored buttons (A/B/C/D); faster correct answers earn more points.
- Each question has a picture area — empty here, since the demo questions are text-only.

### 4. Host follows the questions

![Host question view](images/15-host-question.png)

- The host console lists all questions of the running session, with the correct option marked by a green **Correct** badge.
- This works as the host's answer key while players compete on their own screens.
- The session header keeps the PIN and connection status visible the whole time.

### 5. Final leaderboard

![Final leaderboard](images/16-leaderboard.png)

- When the last question closes, the host screen celebrates: "Quiz Completed! 🎉".
- The leaderboard ranks all players by points — **#1 Ayşe with 682 pts** in this one-player demo session.
- **Back to Quiz** returns to the quiz page to host another round.

## Join Quiz

![Join quiz page](images/04-join.png)

- The public entry point for players: enter the game PIN and a nickname, press **Join Quiz** — that's all.
- Works for guests and logged-in users alike; here "Ayşe" is about to join with a PIN.

## Self-Paced Quiz

![Self-paced quiz](images/17-self-paced.png)

- The same quizzes can be played solo, without a host or other players.
- One question per screen with the familiar colored options — here option **A (elma)** is selected.
- A **Next Question** button moves through the quiz at your own speed; progress ("Question 1 of 5") is shown at the top.

## Word Database

![Word database](images/09-words.png)

- The vocabulary backbone: **13,321 English–Turkish entries**, browsable over 1,333 pages.
- Each row shows the English word, Turkish meaning, word type, CEFR level tag and source — the base content comes from the **Oxford-3000** list.
- Tabs switch between All Words, Flashcard Progress and Spelling Progress; words can be filtered by Known / Learning status and selected in bulk.
- Import, Export CSV and Export JSON buttons make the whole database portable.

## Flashcards

![Flashcards](images/10-flashcards.png)

- Studying the "Basic English A1" deck: card 1 of 10, with a progress bar and an optional timer.
- The flipped card shows the pair **elma / apple**, a sample sentence ("Bir elma yiyordu.") and audio buttons for pronunciation.
- A photo above the card illustrates the word — a red apple for "elma".
- The right rail tracks totals, mastered and remaining words; **Mark as Learning / Known** feeds the dashboard statistics.

## Spelling

![Spelling practice](images/11-spelling.png)

- Spelling mode for the same deck: the app shows the Turkish word (**elma**, with audio) and asks you to type the English one.
- The answer field shows a partial attempt ("app") in progress.
- The picture gives a visual hint, and the right rail tracks spelled and remaining words for the deck.

## Student Performance

![Performance analytics](images/18-performance.png)

- The analytics page opens with stat cards: 9 total students, 38% quiz success rate, 3 quizzes completed, 4h total study time and an average pronunciation score.
- A **Filters** panel narrows results by student, quiz/deck, level, skill, task and date range.
- The **Quiz Performance** table breaks results down per player: points, quizzes, sessions, questions, correct/wrong counts and a success percentage — Ayşe's live session scored 100%, a "test" student sits at 40%.
- Each row expands with a **Show** button for details.

## My Profile

![Profile page](images/19-profile.png)

- Account settings in three cards: profile picture (upload via the camera button), profile information (username) and change password.
- Kept deliberately small — the account is just a username and a password.

## Architecture

- **SPA + REST + WebSocket** — a React single-page app talks to the Express API with JWT-authenticated JSON requests; live game sessions run over Socket.IO on the same backend.
- **PIN-based game rooms** — each hosted session gets a 4-digit PIN; players join a Socket.IO room as guests, and the server broadcasts questions, collects answers and computes scores in real time.
- **AI pipeline** — quiz generation converts PDFs to Markdown and extracts webpages via Firecrawl, then builds questions with OpenRouter/Gemini; Unsplash supplies question images and Azure Speech scores pronunciation.
- **Shared PostgreSQL** — data lives in a shared Postgres instance, with separate databases for dev and prod.
- **Docker containers** — frontend and backend run as containers, with separate dev and prod stacks.
- **Reverse proxy** — an Nginx gateway routes subdomains (`homemadekahoot.furkantekkartal.com` for prod, `homemadekahoot-dev...` for dev) to the right containers, including the WebSocket traffic.

---

🇹🇷 Türkçe versiyon: [README.tr.md](README.tr.md)

*This document is part of the [ProjectReadmes](../) portfolio collection.*
