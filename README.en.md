[🇧🇷 Português](README.md) | 🇺🇸 English

# 🏃 Strava Dashboard
A personal activity dashboard synced with real Strava data in real time — no backend, no build step, just open it and go.

It reads data directly from a Google Sheet and renders interactive, Power-BI-style charts: filterable by year and activity type, with click-to-filter charts.

**[→ Live demo](https://andrescultori.github.io/stravadashboard)**

> This is my personal dashboard — the data shown is real, synced automatically from my own Strava activities.

## The original problem

Strava's own app shows one activity at a time, with no consolidated view: comparing pace trends, monthly volume by sport, or cross-referencing heart rate with distance over time meant exporting everything by hand and charting it manually.

## The solution

```
Strava (recorded activities)
        ↓
Google Apps Script (periodic sync)
        ↓
Google Sheets ("STRAVA" sheet)
        ↓
index.html (direct read via Sheets API)
        ↓
Chart.js (interactive, filterable charts)
```

The result: I open the link and see the full, up-to-date history — no manual export needed.

## The dashboard itself

- Interactive filters by year and activity type — clicking a chart also filters the others
- Highlighted KPIs: total distance and total time
- Charts: monthly distance, distribution by activity type, yearly distance, average pace, heart rate
- Paginated table of all activities, with a direct link to each one on Strava
- Light/dark theme, with saved preference
- Mobile responsive

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | HTML + CSS + vanilla JavaScript |
| Charts | [Chart.js 4](https://www.chartjs.org/) |
| Data | Google Sheets API v4 |
| Sync | Google Apps Script (Strava API → Sheets) |
| Hosting | GitHub Pages / Netlify |

## Why no framework, no backend

The whole dashboard runs from a single `index.html`, with no build step. For a personal project of this scope — reading a spreadsheet and drawing charts — a framework or a dedicated API would add complexity without real benefit: there's no complex state to manage, no routing, no need for SSR. The trade-off is simplicity and zero infrastructure maintenance.

## Architecture

- [`index.html`](./index.html) — the whole frontend: data fetching, parsing, chart and table rendering

## Running locally

1. Clone the repository
2. Open `index.html` directly in your browser (no server needed)

## Using it with your own data (fork)

1. Fork this repository
2. Create a project in the [Google Cloud Console](https://console.cloud.google.com) and enable the **Google Sheets API**
3. Create an **API Key** and restrict it by HTTP referrer to your domain
4. Replace `API_KEY` and `SID` in `index.html` with your own
5. Set up your spreadsheet following the schema below
6. Deploy to GitHub Pages or Netlify

## Spreadsheet schema

The spreadsheet needs a sheet named `STRAVA` with the following columns:

| Col | Field | Type |
|---|---|---|
| A | ID | Text (Strava activity ID) |
| B | DATA | Date (DD/MM/YYYY HH:MM) |
| C | ATIV | Text (Run, Walk, Ride, Hike...) |
| D | KM | Number |
| E | TEMPO | Duration (fraction of a day) |
| F | PACE | Duration (fraction of a day, min/km) |
| G | VEL | Number (km/h) |
| ... | ... | ... |
| M | BPM AVG | Number |
| O | GEAR | Text |
| Q | LOCAL | Text (city) |
| R | ELEV | Number (meters) |
| S | CALORIAS | Number |
| T | NOME | Text (activity name) |
| W | LINK | URL (Strava link) |

---

Built by [André Scultori](https://github.com/andrescultori) · © 2026 · [GitHub](https://github.com/andrescultori/stravadashboard)

*Personal project — real data, synced automatically from Strava via Google Apps Script.*
