# SATC Fan App

A mobile fan companion app for **Sex and the City**, both films, and **And Just Like That** — covering episodes, characters, NYC filming locations, fashion/outfits, and a social layer for fan discussion.

## Project Status
**Phase 1 — POC & Validation** (Active)

## Feature Scope
- Episode guide (94 SATC + 33 AJLT + 2 films)
- Character profiles and relationship tracking
- NYC filming locations on live map (including closed/historical)
- Fashion / outfit tracker with designer profiles
- Watch tracker per user
- Comments, likes/dislikes, and ratings on all content
- Gamification — badges, achievements, trivia (Phase 3)

## Tech Stack

| Layer | Tool | Phase |
|---|---|---|
| POC / Prototypes | Claude + HTML artifacts | Phase 1 |
| Database | Airtable | Phase 1–2 |
| Mobile App | Adalo Pro | Phase 2 |
| Maps | Google Maps API | Phase 2 |
| Image Hosting | Cloudinary | Phase 2 |
| Backend (scale) | AWS or Supabase | Phase 3 |

## Repository Structure

```
satc-fan-app/
├── README.md
├── prototypes/
│   ├── episode-browser/     # Interactive episode guide POC
│   └── location-map/        # NYC filming locations map POC
├── data/
│   ├── episodes.csv         # All SATC + AJLT episodes
│   ├── locations.csv        # 35+ NYC filming locations
│   ├── characters.csv       # Main + recurring cast
│   └── designers.csv        # Fashion designers featured
└── docs/
    ├── data-model.md        # Airtable schema design
    └── decisions.md         # Architecture decision log
```

## Data Sources
Episode and character data sourced from Wikipedia, IMDb, and the Sex and the City Fandom Wiki (Creative Commons). Location data compiled from multiple fan location guides and cross-referenced with Google Maps coordinates.

## Open Questions
- Monetization model (free/freemium/subscription)
- IP/licensing considerations for fan app
- App name and brand identity
- Target audience definition
- Content moderation approach for user comments

## Project Lead
Anthony Vanlandingham — Fractal LLC
