# NIBM iOS Module — Submission & Viva Management System

A static GitHub Pages site for managing student submissions and oral exam (viva) scheduling for NIBM's iOS module (batch 24.2). Three pages, pure HTML/CSS/JS, backed by Supabase.

## Pages

**`index.html` — Final Submission Form**
Students fill in their details (name, index no, batch, project title), confirm deliverable checklists (ZIP upload, Git commit URL, final report, demo video), paste their GitHub commit URL and YouTube demo link, accept a declaration, then submit. On success, they receive a unique 4-character code like `IOS-WKRP` to paste into the LMS.

**`book.html` — Viva Slot Booking**
Students enter their submission token (from index.html) to verify identity, then pick a viva day (Sat 10 May or Sun 11 May 2025) and an hour-long time window. Slots have a capacity of 5 students each, with lab-computer users blocked from evening slots (7pm–11pm on Sundays).

**`queue.html` — Live Viva Queue**
On viva day, students enter their token to join the live queue. Shows their position, estimated wait, and the full queue list (names masked). When the examiner calls them, a full-screen overlay fires with a Google Meet link and optionally a browser push notification. Includes an admin panel (password-protected via Supabase `config` table) for managing the queue, calling/marking-done students, drag-reordering, and reading student messages.

## Data Model (Supabase tables)

| Table | Purpose |
|---|---|
| `ios_submissions` | Submission form data + unique token |
| `bookings` | Slot reservations (day + hour) |
| `sessions` | Available time slots with capacity |
| `queue` | Live queue state (position, status, meet link) |
| `messages` | Student → examiner messages |
| `config` | Admin password, current Google Meet link |

## Known Issues

- `queue.html` lines 304–305 still have placeholder Supabase credentials (`YOUR_PROJECT_ID` / `YOUR_ANON_PUBLIC_KEY`). The real credentials are already in `index.html` and `book.html` — `queue.html` must be updated to match before the queue page will work.

## Tech Stack

- Pure HTML/CSS/JavaScript (no frameworks)
- Supabase REST API for all data operations
- Google Fonts: IBM Plex Mono, DM Sans, Syne
- Dark theme throughout
- Hosted on GitHub Pages
