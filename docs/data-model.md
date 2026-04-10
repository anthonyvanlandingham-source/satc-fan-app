# SATC Fan App — Data Model

## Overview
This document describes the Airtable schema for the SATC Fan App. All tables are designed to be relational, linking content types together through Airtable's linked record fields.

---

## Tables

### 1. Episodes
Core episode catalog for all content.

| Field | Type | Notes |
|---|---|---|
| episode_id | Auto number | Primary key |
| title | Single line text | Episode title |
| series | Single select | SATC / AJLT / FILM |
| season | Number | Season number (0 for films) |
| episode_number | Number | Episode within season |
| episode_overall | Number | Overall episode number 1-117 |
| air_date | Date | Original air date |
| writer | Single line text | |
| director | Single line text | |
| synopsis | Long text | Episode summary |
| scenes | Link to Scenes | All scenes in this episode |
| outfits | Link to Outfits | All outfits in this episode |
| avg_rating | Formula | Average of linked ratings |
| rating_count | Formula | Count of linked ratings |

---

### 2. Scenes
Individual scene records linked to episodes.

| Field | Type | Notes |
|---|---|---|
| scene_id | Auto number | Primary key |
| episode | Link to Episodes | Parent episode |
| scene_title | Single line text | Brief scene name |
| description | Long text | What happens |
| location | Link to Locations | Where filmed |
| characters | Link to Characters | Who appears |
| outfits | Link to Outfits | What is worn |
| scene_type | Single select | Iconic / Regular / Memorable quote |
| memorable_quote | Long text | Notable dialogue |

---

### 3. Locations
NYC filming locations — real and historical.

| Field | Type | Notes |
|---|---|---|
| location_id | Auto number | Primary key |
| name | Single line text | Location name |
| address | Single line text | Street address |
| neighborhood | Single select | NYC neighborhood |
| latitude | Number | For map pin |
| longitude | Number | For map pin |
| type | Single select | Restaurant / Bar / Retail / Landmark / Hotel / Park / Apartment |
| status | Single select | Open / Closed / Never Existed (Fictional) / Changed Name |
| iconic | Checkbox | Featured in curated iconic list |
| still_open | Checkbox | Currently operating |
| closed_notes | Long text | Why/when it closed |
| whats_there_now | Single line text | Current occupant if closed |
| scenes | Link to Scenes | Scenes filmed here |
| carrie_connection | Checkbox | Directly tied to Carrie's story |
| scene_description | Long text | What happened here |
| google_maps_url | URL | Direct Maps link |
| image | Attachment | Photo of location |

---

### 4. Characters
Main and recurring characters across all series.

| Field | Type | Notes |
|---|---|---|
| character_id | Auto number | Primary key |
| character_name | Single line text | |
| actor_name | Single line text | |
| type | Single select | Main / Recurring / Guest |
| series | Multiple select | SATC / AJLT / FILM |
| occupation | Single line text | |
| neighborhood | Single line text | Where they live in show |
| description | Long text | Character bio |
| outfits | Link to Outfits | All outfits worn |
| scenes | Link to Scenes | All scenes appeared in |
| image | Attachment | Character photo |

---

### 5. Outfits
Fashion tracker — outfits worn by characters.

| Field | Type | Notes |
|---|---|---|
| outfit_id | Auto number | Primary key |
| outfit_name | Single line text | Brief descriptive name |
| character | Link to Characters | Who wears it |
| episode | Link to Episodes | Which episode |
| scene | Link to Scenes | Which scene |
| designer | Link to Designers | Brand/designer |
| description | Long text | Detailed description |
| iconic | Checkbox | Curated iconic outfit |
| image | Attachment | Outfit photo |
| avg_rating | Formula | Average user rating |

---

### 6. Designers
Fashion designers and brands featured in the show.

| Field | Type | Notes |
|---|---|---|
| designer_id | Auto number | Primary key |
| name | Single line text | Designer/brand name |
| nationality | Single line text | |
| description | Long text | About the designer |
| outfits | Link to Outfits | All outfits in show |
| times_featured | Formula | Count of outfits |
| website | URL | Official website |
| image | Attachment | Logo or photo |

---

### 7. User Reactions (Social Layer)
Single table handles all likes, dislikes, ratings, and comments across all content types.

| Field | Type | Notes |
|---|---|---|
| reaction_id | Auto number | Primary key |
| user_id | Link to Users | Who reacted |
| content_type | Single select | Episode / Scene / Location / Outfit / Designer / Character |
| content_id | Number | ID of the linked content item |
| reaction_type | Single select | Like / Dislike / Rating / Comment |
| rating_value | Number | 1-5 stars (if type = Rating) |
| comment_text | Long text | Comment content (if type = Comment) |
| created_at | Created time | Auto timestamp |
| parent_reaction_id | Number | For nested replies (V2) |

---

### 8. Users
App user profiles.

| Field | Type | Notes |
|---|---|---|
| user_id | Auto number | Primary key |
| username | Single line text | Display name |
| email | Email | For auth |
| joined_date | Created time | Auto |
| episodes_watched | Link to Episodes | Watch tracker |
| locations_visited | Link to Locations | Visited tracker |
| badge_count | Formula | Count of earned badges |

---

### 9. Lexicon
Show-specific terms, references, and running jokes.

| Field | Type | Notes |
|---|---|---|
| term_id | Auto number | Primary key |
| term | Single line text | The word or phrase |
| definition | Long text | What it means in SATC context |
| category | Single select | Fashion / Slang / Character / Reference / Location |
| first_appeared | Link to Episodes | Episode where introduced |
| examples | Long text | How it is used in the show |

---

## Key Relationships

```
Episodes ──< Scenes >── Locations
Episodes ──< Outfits >── Designers
Scenes ──< Characters
Characters ──< Outfits
Users ──< Reactions (polymorphic → any content type)
Users ──< Episodes (watch tracker)
```

---

## Airtable Setup Notes
- Create tables in the order listed above to avoid broken links
- Set up linked record fields after all tables exist
- Import CSV files for Episodes, Locations, Characters as starting point
- Reactions table starts empty — populated by user activity
- Use Airtable Automations to calculate running average ratings
