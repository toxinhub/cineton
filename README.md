# CineTon

> **Some of the films I've watched. Rest of the drama? I'm living it...**

A lightweight, GitHub Pages–based personal cinema diary with a GitHub-managed library and a Supabase-backed public interaction layer for visitor ratings, comments, and admin activity monitoring.

## 🎬 Live Site

**CineTon:** https://toxinhub.github.io/cineton/

**Admin:** https://toxinhub.github.io/cineton/admin.html

---

## ✨ Features

### Public cinema diary
- **Watched / Watchlist** tabs
- Responsive **grid view** and compact **list view**
- Search by **title, actor, director, or year**
- Filter by **Movie / TV / Show**
- Sort by:
  - Newest first
  - My rating
  - IMDb rating
  - Release year
  - Title (A–Z)
- Quick statistics:
  - Movie count
  - TV count
  - My average rating
  - Rated-title count
- **Surprise Me** random-title button
- Movie/TV detail modal with:
  - Poster
  - IMDb rating
  - My rating
  - Director / creator
  - Cast
  - Story / overview
  - Personal note
  - Watched date
- Click a director or actor to filter the library by that person
- Skeleton loading state and graceful loading/error handling
- Responsive layout for desktop and mobile
- Warm, muted **cream / brown / gold** visual theme with a subtle film-grain texture
- **Mina** + **Cormorant Garamond** typography

### 🛠️ Admin panel
The separate `admin.html` page provides browser-based library management:

- GitHub connection and `data.json` loading
- Add a single movie or TV show through **TMDB search**
- Optional **OMDb** enrichment for IMDb ratings
- Add personal rating, watched date and note
- Bulk-add a personal movie list
- Automatic title matching/review workflow for bulk imports
- Search and filter the existing library
- Edit, delete and mark titles as watched
- Saves changes directly back to GitHub

---

## 📁 Repository Structure

| File | Purpose |
|---|---|
| `index.html` | Public CineTon interface |
| `admin.html` | Library management interface |
| `data.json` | Movie/TV library data |
| `README.md` | Project documentation |

The project remains buildless and framework-free, but public interaction features use Supabase Database, Realtime Broadcast, and Edge Functions.

---

## 🚀 Setup

### 1. GitHub Pages

Upload these files to a GitHub repository:

```text
index.html
admin.html
data.json
README.md
```

Then enable:

**GitHub → Settings → Pages → Deploy from branch → main / root**

Your public site will be available at:

```text
https://USERNAME.github.io/REPOSITORY/
```

### 2. TMDB API key

The Admin panel uses **TMDB** to search for titles and retrieve metadata such as:

- Poster
- Release year
- Overview
- Director / creator
- Cast
- IMDb ID

Create a TMDB API key from your TMDB account settings and enter it in **Admin → Connection**.

### 3. Optional OMDb API key

OMDb is used to retrieve the IMDb rating when an IMDb ID is available.

An OMDb key is optional. CineTon can still add titles using TMDB alone.

### 4. GitHub token

The Admin panel saves the library by updating `data.json` through the GitHub Contents API.

Create a **fine-grained GitHub personal access token** with access limited to this repository and:

```text
Repository permissions
└── Contents → Read and write
```

Enter the repository as:

```text
USERNAME/REPOSITORY
```

Then connect from `admin.html`.

---

## 🔐 Security Notes

- **Do not commit your GitHub token or API keys into the repository.**
- The Admin page stores the repository and API-key values locally in the browser.
- The GitHub token is kept in **session storage** for the current browser session.
- Use a fine-grained token restricted to this repository rather than a broad classic token.
- Anyone who can access the Admin page **and obtain valid credentials** could modify the library, so treat the Admin page as a private management interface.
- `data.json` is public when the repository is public, so do not store sensitive personal information in it.

---

## 🧩 Data Format

Each library entry follows a structure similar to:

```json
{
  "id": "movie-27205",
  "type": "movie",
  "title": "Inception",
  "year": "2010",
  "poster": "/poster-path.jpg",
  "overview": "Story overview...",
  "director": "Christopher Nolan",
  "cast": [
    "Leonardo DiCaprio",
    "Joseph Gordon-Levitt"
  ],
  "imdb": "8.8",
  "my_rating": 9,
  "watched_on": "2026-10-02",
  "comment": "Personal note",
  "status": "watched",
  "needs_review": false
}
```

### Supported status values

- `watched`
- `watchlist`

### Supported type values

- `movie`
- `tv`

---

## 🧠 How It Works

```text
                    ┌──────────────┐
                    │   TMDB API   │
                    └──────┬───────┘
                           │ metadata
                           ▼
┌─────────────┐     ┌──────────────┐
│  admin.html │ ───▶ │   data.json  │   ← personal library
└─────────────┘     └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Supabase   │   ← public comments / ratings / activity
                    └──────────────┘
                           │
                           ▼
                     CineTon UI
```

The public page reads `data.json` and renders the cinema diary. The Admin page uses GitHub's API to read and update that same file.

---

## 🎨 Design Direction

CineTon currently follows a **warm luxury** visual direction:

- Cream background
- Brown typography
- Muted gold accents
- Soft borders and shadows
- Subtle grain texture
- Minimal controls
- Responsive desktop/mobile layout
- Editorial-style **Cormorant Garamond** headings
- **Mina** for interface text

The goal is a calm, readable cinema diary rather than a conventional streaming-service clone.

---

## 🧰 Technology

- HTML5
- CSS3
- Vanilla JavaScript
- JSON
- GitHub Pages
- GitHub Contents API
- Supabase Database / Realtime / Edge Functions
- TMDB API
- OMDb API
- Google Fonts

No React, Node.js, build step or backend server is required.

---

## 🔔 Public Activity & Admin Notifications

Visitor interaction is intentionally separated from the personal library.

- Visitors can submit anonymous **public comments** and **1–10 public ratings**.
- Admin has a dedicated **Activity** section showing recent comments and ratings.
- A header **🔔 notification indicator** shows unread activity.
- Activity can be marked as read and is remembered locally in the admin browser.
- A Supabase Edge Function returns the activity feed only after verifying the existing GitHub admin token.
- Supabase Realtime Broadcast provides a low-latency refresh signal while the Edge Function remains the source of truth.
- The live signal carries only minimal identifiers; it does not expose the full comment/rating feed.

The database triggers are defensive: if Realtime is temporarily unavailable, a visitor comment or rating must still be saved successfully.

## 📌 Notes

CineTon is designed primarily as a **personal film diary and library**, with the personal library kept in a simple GitHub-managed JSON file and visitor interaction data kept separately in Supabase.

For future changes, preserve the separation between:

```text
Public UI → index.html
Admin / editing → admin.html
Library data → data.json
Documentation → README.md
```

That keeps the project easy to maintain and deploy.
