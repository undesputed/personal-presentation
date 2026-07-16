# About Me Deck Redesign

**Date:** 2026-07-16  
**Status:** Approved for planning  
**Primary file:** `about-me.html`  
**Out of scope:** `index.html`, `qa-cheatsheet.html`

## Problem

`about-me.html` is a short cobalt-on-paper 5-slide intro that no longer matches Carrie’s fuller self-introduction or the sunrise visual language of the main presentation. The content needs a warmer, bilingual, photo-supported deck for a mixed audience (colleagues + stakeholders).

## Goals

- Replace all content in `about-me.html` with the approved introduction story.
- Restyle to match `index.html` sunrise identity (tokens, fonts, chapter backgrounds, chrome).
- Bilingual English + Japanese (EN headlines, JP subtitles; body primarily EN with JP support lines where natural).
- Medium length: **8 slides**, story-arc structure.
- Visual lifestyle/interest slides for sports, games, and anime using provided assets.
- Keep self-contained single HTML file; no build step.

## Non-goals

- Rewriting or restyling `index.html` / `qa-cheatsheet.html`.
- Adding a build toolchain, framework, or CMS.
- Inventing personal lifestyle photos the user did not provide.
- Perfect JP literary translation beyond clear, natural presentation Japanese.

## Decisions (locked)

| Topic | Choice |
|-------|--------|
| Photo intensity | Lifestyle mix — cover portrait + visual grids on interest slides |
| Audience | Mixed room — warm but polished |
| Visual identity | Match sunrise deck (`index.html`) |
| Length | Medium → finalized as **8 slides** |
| Language | Full bilingual EN + JP pattern like `index.html` |
| Structure | Story arc (Approach 1), with Games and Anime/manga as **separate** slides |

## Slide map

| # | `data-chap` | Theme | Slide | Media |
|---|-------------|-------|-------|-------|
| 1 | dawn | dark | Cover / hello | `personal.png` (circular portrait) |
| 2 | dawn | dark | Who I am | — |
| 3 | rise | dark | Career | tech chips only |
| 4 | day | light | Sports | `badminton.avif`, `tennis.jpg`, `table-tennis.webp` |
| 5 | day | light | Games | `minecraft.jpg`, `dota-2.jpg`, `valorant.jpeg` |
| 6 | day | light | Anime / manga | `tokyo-ghould.jpg`, `attack-on-titan.jpg` |
| 7 | day | light | Learning & family | no required image (optional family later) |
| 8 | day | light | Thank you / contact | — |

Chapter progression mirrors the main deck: dawn → rise → day.

## Content contract (per slide)

Copy is tightened from Carrie’s draft for slide density. Implementers may lightly polish wording for rhythm but must not change facts.

### 1 — Cover
- EN: Hi everyone — I’m Carrie.
- JP: みなさん、こんにちは。キャリーです。
- Role line: Software Engineer & Team Leader · from the Philippines
- JP support: ソフトウェアエンジニア / チームリーダー · フィリピン出身
- Portrait: `personal.png`
- Navigation hint (same spirit as `index.html`)

### 2 — Who I am
- Headline: Software Engineer & Team Leader
- JP: ソフトウェアエンジニア / チームリーダー
- Body: Originally from the Philippines; builds software and leads teams; excited to meet everyone.
- Keep short — credentials belong on slide 3.

### 3 — Career
- Headline: 6+ years building software
- JP: ソフトウェア開発歴 6年以上
- Points: Computer Science degree · web applications · lead development teams
- Closing: Enjoys solving technical challenges and helping the team deliver high-quality software.
- Chips: Java · React · Python · AWS

### 4 — Sports
- Headline: Staying active
- JP: 体を動かすことが好きです
- Body: Badminton, tennis, and table tennis — stay active and have fun.
- Layout: text + 3-image grid (one image per sport)

### 5 — Games
- Headline: Games I love
- JP: 好きなゲーム
- Body: Minecraft, Dota, Valorant, and more — relax after work and spend time with friends.
- Layout: text + 3-image grid

### 6 — Anime / manga
- Headline: Manga & anime
- JP: 漫画・アニメ
- Body: Enjoy reading manga and watching anime across genres; favorites include Tokyo Ghoul, Attack on Titan, and more.
- Layout: text + 2-image grid

### 7 — Learning & family
- Headline: Always learning · time with family
- JP: 学び続けること、そして家族との時間
- Two clusters:
  - Exploring AI and new software development tools
  - Quality time with family — going out, movies, relaxing at home
- No required photo; do not leave empty image frames

### 8 — Closing
- Headline: Excited to meet everyone
- JP: みなさんとお会いできてうれしいです
- Body: Looking forward to learning from others and contributing knowledge.
- Contact: `eirracyu12@gmail.com` · Cebu City, Philippines
- Closing thank-you treatment in the spirit of `index.html` (ありがとう / Thank you)

## Visual & interaction design

### Reuse from `index.html`
- CSS tokens: cream, ink, gold, teal, coral; Fraunces / Nunito Sans / Zen Maru Gothic
- Chapter backgrounds: `dawn`, `rise`, `day`
- Topbar chapter tag + bottom nav (arrows, progress trail/dots, counter)
- Reveal animation (`.r` + `--i` delays)
- Keyboard, click, and swipe navigation; URL hash slide index
- `prefers-reduced-motion` and print styles

### New / adapted for about-me
- Cover split: copy + circular portrait (not the monogram-only cover from `index.html`)
- Interest image grids for slides 4–6:
  - Object-fit cover, consistent radius matching sunrise day panels
  - Captions optional (sport/game/title) in small mono/label style if needed for clarity
  - Mobile: stack text above grid; grids become 1–2 columns
- No hero overlays, no card clutter on cover; cards only if needed for interaction (they are not needed)

### Missing assets
- If a listed interest image is missing at runtime, omit that cell and reflow the grid (no broken icons).
- Portrait: use `personal.png`. If absent, cover becomes text-only (no empty circle).

## Architecture / units

Single HTML file, three logical units:

1. **Design tokens & slide chrome** — shared visual system and navigation shell (adapted from `index.html`).
2. **Slide content sections** — 8 `<section class="slide">` blocks with bilingual copy and media.
3. **Deck controller script** — activate slide, update trail/counter/chapter, keyboard/touch/hash (same behavior as current about-me / index).

No external JS dependencies. Fonts from Google Fonts (same as `index.html`).

## File / asset inventory

| Path | Role |
|------|------|
| `about-me.html` | Full rewrite target |
| `personal.png` | Cover portrait |
| `badminton.avif` | Sports grid |
| `tennis.jpg` | Sports grid |
| `table-tennis.webp` | Sports grid |
| `minecraft.jpg` | Games grid |
| `dota-2.jpg` | Games grid |
| `valorant.jpeg` | Games grid |
| `tokyo-ghould.jpg` | Anime grid (filename typo kept unless renamed in implementation) |
| `attack-on-titan.jpg` | Anime grid |

Optional later: rename `tokyo-ghould.jpg` → `tokyo-ghoul.jpg` and update the `src` in the same change.

## Edge cases

- Narrow viewports: portrait below title; image grids stack.
- Reduced motion: disable decorative motion; keep opacity visibility switches.
- Print: one slide per page, chrome hidden (match existing about-me/index behavior).
- Hash deep links: `#1`–`#8` work on load.

## Success criteria

- Opening `about-me.html` shows an 8-slide bilingual sunrise deck.
- Content matches the approved story (identity, career, sports, games, anime, learning/family, close).
- Visual system is recognizably the same brand as `index.html`.
- Sports / Games / Anime slides each show their provided images in a grid.
- Keyboard and on-screen navigation work; hash updates.
- Looks acceptable on desktop and mobile.

## Implementation notes

- Prefer adapting patterns from `index.html` over inventing a third design language.
- Do not port the full 17-slide narrative content from `index.html` — only the visual/interaction system.
- Update `README.md` about-me description to reflect the new 8-slide sunrise bilingual deck (small docs sync as part of the same work).
