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
| Language | Bilingual like `index.html`: EN headlines + JP `jp-sub` on every slide; EN body; JP body line only where noted |
| Structure | Story arc (Approach 1), with Games and Anime/manga as **separate** slides |

## Slide map

| # | `data-chap` | Theme | `data-chapter` (topbar) | Slide | Media |
|---|-------------|---------|-------------------------|-------|-------|
| 1 | dawn | dark | *(empty)* | Cover / hello | `personal.png` (circular portrait) |
| 2 | dawn | dark | Who I am · 自己紹介 | Who I am | — |
| 3 | rise | dark | Career · キャリア | Career | tech chips only |
| 4 | day | light | Outside work · プライベート | Sports | `badminton.avif`, `tennis.jpg`, `table-tennis.webp` |
| 5 | day | light | Outside work · プライベート | Games | `minecraft.jpg`, `dota-2.jpg`, `valorant.jpeg` |
| 6 | day | light | Outside work · プライベート | Anime / manga | `tokyo-ghould.jpg`, `attack-on-titan.jpg` |
| 7 | day | light | Outside work · プライベート | Learning & family | no required image |
| 8 | day | light | *(empty)* | Thank you / contact | — |

Chapter progression mirrors the main deck: dawn → rise → day.

### Page chrome (locked)
- `<title>`: `About — Carrie A. Yu`
- Topbar brand: `Carrie A. Yu` (same spirit as current about-me; no need to force “Hipe Japan” into the brand line)
- Image captions on slides 4–6: **none** (alt text only for accessibility)

## Content contract (per slide)

Copy is tightened from Carrie’s draft for slide density. Implementers may lightly polish wording for rhythm but must not change facts.

### 1 — Cover
- Headline EN: Hi everyone — I’m Carrie.
- JP sub: みなさん、こんにちは。キャリーです。
- Role line EN: Software Engineer & Team Leader · from the Philippines
- JP support: ソフトウェアエンジニア / チームリーダー · フィリピン出身
- Portrait: `personal.png` — alt: `Carrie Yu portrait`
- Navigation hint (locked): `Press` + `→` + `to continue · 「→」で次へ`

### 2 — Who I am
- Headline EN: Software Engineer & Team Leader
- JP sub: ソフトウェアエンジニア / チームリーダー
- Body EN: I’m originally from the Philippines. I work as a software engineer and team leader — building software and supporting the people I work with.
- JP body: フィリピン出身です。ソフトウェアエンジニアおよびチームリーダーとして、プロダクトづくりとチームのサポートに取り組んでいます。
- Keep short — credentials belong on slide 3.

### 3 — Career
- Headline EN: 6+ years building software
- JP sub: ソフトウェア開発歴 6年以上
- Points EN:
  - Graduated with a degree in Computer Science
  - Build web applications and lead development teams
  - Enjoy solving technical challenges and helping the team deliver high-quality software
- JP body (one line under points): コンピュータサイエンスを専攻し、Webアプリ開発やチームリードに携わってきました。
- Chips: Java · React · Python · AWS

### 4 — Sports
- Headline EN: Staying active
- JP sub: 体を動かすことが好きです
- Body EN: I like playing badminton, tennis, and table tennis — they help me stay active and have fun.
- Layout: text column + 3-image grid (equal cells). Alts: `Badminton`, `Tennis`, `Table tennis`. No captions.

### 5 — Games
- Headline EN: Games I love
- JP sub: 好きなゲーム
- Body EN: I enjoy Minecraft, Dota 2, Valorant, and many other games. Gaming is one of my favorite ways to relax after work and spend time with friends.
- Layout: text column + 3-image grid. Alts: `Minecraft`, `Dota 2`, `Valorant`. No captions.

### 6 — Anime / manga
- Headline EN: Manga & anime
- JP sub: 漫画・アニメ
- Body EN: I enjoy reading manga and watching anime across different genres. Favorites include Tokyo Ghoul, Attack on Titan, and more.
- Layout: text column + 2-image grid. Alts: `Tokyo Ghoul`, `Attack on Titan`. No captions.
- Asset path: use `tokyo-ghould.jpg` as currently named (optional rename can be a follow-up).

### 7 — Learning & family
- Headline EN: Always learning · time with family
- JP sub: 学び続けること、そして家族との時間
- Layout: **two-column split on desktop** (stack on mobile). No images.
  - Left cluster label EN: Exploring tech · JP: 新しい技術
    - Body EN: I like exploring new technology — especially AI and new software development tools — and trying things that help me grow as a developer.
  - Right cluster label EN: Family · JP: 家族
    - Body EN: I also enjoy spending quality time with my family — going out together, watching movies, or simply relaxing at home.
- Do not leave empty image frames.

### 8 — Closing
- Headline EN: Excited to meet everyone
- JP sub: みなさんとお会いできてうれしいです
- Body EN: I’m excited to learn from your experiences and hopefully contribute my own knowledge as well.
- JP body: みなさんの経験から学び、私も知識を共有できたらうれしいです。
- Large thank-you line: `ありがとう` with smaller EN `Thank you`
- Contact: mailto link `eirracyu12@gmail.com` · place text `Cebu City, Philippines`

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
  - Desktop: text left, image grid right
  - Object-fit cover, consistent radius matching sunrise day panels
  - No visible captions — accessibility via `alt` only (see content contract)
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
