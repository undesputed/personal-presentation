# About Me Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite `about-me.html` as an 8-slide bilingual sunrise intro deck that matches `index.html` and uses the interest images already in the repo.

**Architecture:** Single self-contained HTML file. Adapt the sunrise design tokens, chapter backgrounds, chrome, and deck controller from `index.html`. Replace slide content with the locked copy from the design spec. Interest slides use local image grids (no captions).

**Tech Stack:** Plain HTML/CSS/JS, Google Fonts (Fraunces, Nunito Sans, Zen Maru Gothic), no build step.

**Spec:** `docs/superpowers/specs/2026-07-16-about-me-redesign-design.md`

## Global Constraints

- Do not modify `index.html` or `qa-cheatsheet.html`.
- Keep one file: `about-me.html` (plus existing image assets + README sync).
- Use exact asset filenames already in the repo (including `tokyo-ghould.jpg`).
- Bilingual pattern: EN headline + JP `jp-sub` every slide; JP body only where the spec lists it.
- Image captions: none (alt text only).
- Desktop interest layout: text left, grid right; cover: text left, portrait right.
- Facts and contact must match the spec (`eirracyu12@gmail.com`, Cebu City, Philippines).

---

## File map

| File | Responsibility |
|------|----------------|
| `about-me.html` | Full rewrite — tokens, chrome, 8 slides, deck controller |
| `personal.png` | Cover portrait (existing) |
| `badminton.avif`, `tennis.jpg`, `table-tennis.webp` | Sports grid (existing) |
| `minecraft.jpg`, `dota-2.jpg`, `valorant.jpeg` | Games grid (existing) |
| `tokyo-ghould.jpg`, `attack-on-titan.jpg` | Anime grid (existing) |
| `README.md` | Update about-me description to 8-slide sunrise bilingual deck |

---

### Task 1: Sunrise shell + deck controller

**Files:**
- Modify: `about-me.html` (full replace of head/chrome/script; temporary empty slides ok)
- Reference: `index.html` (copy patterns only — do not edit)

**Interfaces:**
- Consumes: sunrise tokens / chap backgrounds / trail nav / `go(n)` behavior from `index.html`
- Produces: working 8-slot deck shell with `data-chap`, `data-theme`, `data-chapter`; body class `theme-dark`/`theme-light`; hash `#1`–`#8`

- [ ] **Step 1: Confirm assets on disk**

Run:

```bash
cd /Users/carrieyu/Desktop/Hipe/personal-presentation
ls personal.png badminton.avif tennis.jpg table-tennis.webp minecraft.jpg dota-2.jpg valorant.jpeg tokyo-ghould.jpg attack-on-titan.jpg
```

Expected: all nine paths listed with no “No such file” errors.

- [ ] **Step 2: Rewrite `about-me.html` shell**

Replace the entire file with a sunrise shell that includes:

1. Same Google Fonts link and `:root` tokens as `index.html` (cream, ink, gold, teal, coral, Fraunces/Nunito/Zen Maru).
2. Slide system + `data-chap` backgrounds (`dawn` / `rise` / `day`) + theme topbar/nav colors from `index.html`.
3. Type helpers: `.eyebrow`, `.h-xl`/`.h-lg`/`.h-md`, `.jp`, `.jp-sub`, `.lead`, `.r` reveal.
4. Topbar: `#chapTag` left, brand `Carrie A. Yu` right (not “Hipe Japan”).
5. Nav: prev/next, trail with `#trailFill` + `#dots`, `#counter` showing `01 / 08`.
6. Eight placeholder `<section class="slide">` elements with the locked attributes:

| # | data-chap | data-theme | data-chapter |
|---|-----------|------------|--------------|
| 1 | dawn | dark | *(empty string)* |
| 2 | dawn | dark | `Who I am · 自己紹介` |
| 3 | rise | dark | `Career · キャリア` |
| 4 | day | light | `Outside work · プライベート` |
| 5 | day | light | `Outside work · プライベート` |
| 6 | day | light | `Outside work · プライベート` |
| 7 | day | light | `Outside work · プライベート` |
| 8 | day | light | *(empty string)* |

Each placeholder can be a minimal `slide__inner` with eyebrow text `Slide N` for now.

7. Deck controller script copied from `index.html` (trail fill, theme class swap, keyboard, swipe, hash). Only change: initial counter text `01 / 08`.

8. Include reduced-motion + print CSS adapted from `index.html`.

9. `<title>About — Carrie A. Yu</title>`

Also add about-me-specific CSS stubs (empty rules ok until Task 2–4 fill them):

```css
.cover-split{ display:grid; grid-template-columns:1.1fr .9fr; gap:clamp(1.2rem,3vw,2.4rem); align-items:center; }
.cover-photo img{ width:100%; max-width:320px; aspect-ratio:1; object-fit:cover; border-radius:50%;
  border:2px solid rgba(255,255,255,.25); box-shadow:0 18px 40px rgba(0,0,0,.28); justify-self:end; }
.media-split{ display:grid; grid-template-columns:1fr 1.05fr; gap:clamp(1.2rem,3vw,2.2rem); align-items:center; }
.media-grid{ display:grid; gap:.7rem; }
.media-grid--3{ grid-template-columns:1fr 1fr; }
.media-grid--3 .media-grid__item:last-child{ grid-column:1 / -1; }
.media-grid--2{ grid-template-columns:1fr 1fr; }
.media-grid__item{ margin:0; border-radius:16px; overflow:hidden; aspect-ratio:4/3;
  box-shadow:0 12px 28px rgba(20,35,43,.12); background:#fff; }
.media-grid__item img{ width:100%; height:100%; object-fit:cover; display:block; }
.chips{ display:flex; flex-wrap:wrap; gap:.7rem; margin-top:1.4rem; }
.chip{ display:inline-flex; align-items:center; padding:.55rem 1rem; border-radius:999px;
  background:rgba(255,255,255,.1); border:1px solid rgba(255,255,255,.2); font-weight:700; font-size:.92rem; }
[data-chap="day"] .chip{ background:rgba(20,35,43,.05); border-color:rgba(20,35,43,.12); }
.two-col{ display:grid; grid-template-columns:1fr 1fr; gap:clamp(1.2rem,3vw,2rem); margin-top:1.6rem; }
.cluster__label{ font-family:var(--body); font-weight:900; text-transform:uppercase; letter-spacing:.12em;
  font-size:.72rem; color:var(--gold-deep); margin-bottom:.55rem; }
.cluster__label .jp{ display:inline; text-transform:none; letter-spacing:0; font-weight:500; opacity:.75; margin-left:.45em; }
.points{ list-style:none; display:grid; gap:.65rem; margin-top:1.2rem; max-width:48ch; }
.points li{ display:flex; gap:.75rem; align-items:baseline; font-size:clamp(1rem,2vw,1.2rem); font-weight:600; }
.points li::before{ content:"→"; color:var(--gold-2); font-weight:900; }
[data-chap="day"] .points li::before{ color:var(--gold-deep); }
.hint{ margin-top:2rem; display:inline-flex; align-items:center; gap:.7rem;
  font-weight:800; letter-spacing:.14em; text-transform:uppercase; font-size:.72rem; opacity:.72; }
.hint .key{ border:1.5px solid rgba(255,255,255,.5); border-radius:8px; padding:.15rem .55rem; }
.closing .arigato{ font-family:var(--display); font-weight:900; font-size:clamp(2.4rem,9vw,5.5rem);
  background:linear-gradient(120deg,var(--coral),var(--gold));
  -webkit-background-clip:text; background-clip:text; color:transparent; line-height:1; margin-top:1.2rem; }
.closing .thanks-en{ font-weight:800; letter-spacing:.08em; text-transform:uppercase; opacity:.7; margin-top:.4rem; }
.closing .contact{ margin-top:2rem; display:flex; flex-wrap:wrap; gap:.6rem 1.8rem; font-weight:700; }
.closing .contact a{ color:var(--ink); text-decoration:none; border-bottom:2px solid var(--gold); padding-bottom:1px; }
.closing .place{ color:var(--ink-soft); }
@media (max-width: 820px){
  .cover-split, .media-split, .two-col{ grid-template-columns:1fr; }
  .cover-photo img{ max-width:260px; }
}
@media (max-width: 480px){
  .media-grid--2{ grid-template-columns:1fr; }
}
```

Missing-image behavior: add this small script after building the DOM (inside the IIFE is fine):

```javascript
document.querySelectorAll('.media-grid__item img, .cover-photo img').forEach(img=>{
  img.addEventListener('error', ()=>{
    const cell = img.closest('.media-grid__item') || img.closest('.cover-photo');
    if(cell) cell.remove();
  });
});
```

- [ ] **Step 3: Smoke-check shell**

Run:

```bash
grep -c 'class="slide"' about-me.html
grep -E 'data-chapter="Who I am · 自己紹介"|data-chapter="Career · キャリア"|Outside work · プライベート' about-me.html | wc -l
grep -q 'theme-'+ about-me.html; grep -q 'trailFill' about-me.html && echo OK_TRAIL
```

Expected: `8` slides; at least 6 matching chapter lines; `OK_TRAIL`.

Open `about-me.html` in a browser, press `→` through all slides, confirm counter reaches `08 / 08` and day slides switch to light theme.

- [ ] **Step 4: Commit**

```bash
git add about-me.html
git commit -m "$(cat <<'EOF'
Scaffold sunrise about-me deck shell.

Replace cobalt styling with index-matched tokens, chrome, and 8-slide navigation.
EOF
)"
```

---

### Task 2: Cover, Who I am, Career (slides 1–3)

**Files:**
- Modify: `about-me.html` (replace placeholder sections 1–3)

**Interfaces:**
- Consumes: `.cover-split`, `.cover-photo`, `.chips`, `.chip`, `.points`, `.hint` from Task 1
- Produces: finished dawn/rise content for slides 1–3

- [ ] **Step 1: Implement slide 1 — Cover**

Replace slide 1 inner with:

```html
<section class="slide" data-chap="dawn" data-theme="dark" data-chapter="">
  <div class="slide__inner cover-split">
    <div>
      <h1 class="h-xl r" style="--i:0">Hi everyone — I’m Carrie.</h1>
      <p class="jp-sub r" style="--i:1">みなさん、こんにちは。キャリーです。</p>
      <p class="lead r" style="--i:2" style="margin-top:1.2rem">Software Engineer &amp; Team Leader · from the Philippines</p>
      <p class="jp r muted r" style="--i:3; font-size:1rem; margin-top:.45rem">ソフトウェアエンジニア / チームリーダー · フィリピン出身</p>
      <div class="hint r" style="--i:4"><span>Press</span><span class="key">→</span><span>to continue · 「→」で次へ</span></div>
    </div>
    <div class="cover-photo r" style="--i:1.2">
      <img src="personal.png" alt="Carrie Yu portrait" />
    </div>
  </div>
</section>
```

Fix duplicate `style` attributes if present — merge into one `style` on the lead paragraph: `margin-top:1.2rem` only on that `p.lead`.

- [ ] **Step 2: Implement slide 2 — Who I am**

```html
<section class="slide" data-chap="dawn" data-theme="dark" data-chapter="Who I am · 自己紹介">
  <div class="slide__inner">
    <div class="eyebrow r" style="--i:0">Who I am</div>
    <h2 class="h-lg r" style="--i:1">Software Engineer &amp; Team Leader</h2>
    <p class="jp-sub r" style="--i:2">ソフトウェアエンジニア / チームリーダー</p>
    <p class="lead r" style="--i:3" style="margin-top:1.4rem">I’m originally from the Philippines. I work as a software engineer and team leader — building software and supporting the people I work with.</p>
    <p class="jp r muted" style="--i:4; font-size:1rem; margin-top:.7rem; max-width:48ch">フィリピン出身です。ソフトウェアエンジニアおよびチームリーダーとして、プロダクトづくりとチームのサポートに取り組んでいます。</p>
  </div>
</section>
```

Again merge duplicate styles into single attributes when writing the file.

- [ ] **Step 3: Implement slide 3 — Career**

```html
<section class="slide" data-chap="rise" data-theme="dark" data-chapter="Career · キャリア">
  <div class="slide__inner">
    <div class="eyebrow r" style="--i:0">Career</div>
    <h2 class="h-lg r" style="--i:1">6+ years building software</h2>
    <p class="jp-sub r" style="--i:2">ソフトウェア開発歴 6年以上</p>
    <ul class="points r" style="--i:3">
      <li>Graduated with a degree in Computer Science</li>
      <li>Build web applications and lead development teams</li>
      <li>Enjoy solving technical challenges and helping the team deliver high-quality software</li>
    </ul>
    <p class="jp r muted" style="--i:4; font-size:1rem; margin-top:1rem; max-width:48ch">コンピュータサイエンスを専攻し、Webアプリ開発やチームリードに携わってきました。</p>
    <div class="chips r" style="--i:5">
      <span class="chip">Java</span>
      <span class="chip">React</span>
      <span class="chip">Python</span>
      <span class="chip">AWS</span>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Verify slides 1–3**

Run:

```bash
grep -F "Hi everyone — I’m Carrie." about-me.html
grep -F 'src="personal.png"' about-me.html
grep -F 'ソフトウェア開発歴 6年以上' about-me.html
grep -E 'chip">Java|chip">React|chip">Python|chip">AWS' about-me.html
```

Expected: all matches found. In browser: portrait visible on `#1`; chips visible on `#3`.

- [ ] **Step 5: Commit**

```bash
git add about-me.html
git commit -m "$(cat <<'EOF'
Add cover, identity, and career slides to about-me.

Lock bilingual intro copy and tech chips for the opening arc.
EOF
)"
```

---

### Task 3: Sports, Games, Anime (slides 4–6)

**Files:**
- Modify: `about-me.html` (replace placeholder sections 4–6)
- Use existing assets (do not re-download):
  - Sports: `badminton.avif`, `tennis.jpg`, `table-tennis.webp`
  - Games: `minecraft.jpg`, `dota-2.jpg`, `valorant.jpeg`
  - Anime: `tokyo-ghould.jpg`, `attack-on-titan.jpg`

**Interfaces:**
- Consumes: `.media-split`, `.media-grid`, `.media-grid--3`, `.media-grid--2`
- Produces: visual interest slides with local images

- [ ] **Step 1: Implement slide 4 — Sports**

```html
<section class="slide" data-chap="day" data-theme="light" data-chapter="Outside work · プライベート">
  <div class="slide__inner media-split">
    <div>
      <div class="eyebrow r" style="--i:0">Outside work</div>
      <h2 class="h-md r" style="--i:1">Staying active</h2>
      <p class="jp-sub r" style="--i:2">体を動かすことが好きです</p>
      <p class="lead r" style="--i:3; margin-top:1.2rem">I like playing badminton, tennis, and table tennis — they help me stay active and have fun.</p>
    </div>
    <div class="media-grid media-grid--3 r" style="--i:2">
      <figure class="media-grid__item"><img src="badminton.avif" alt="Badminton" /></figure>
      <figure class="media-grid__item"><img src="tennis.jpg" alt="Tennis" /></figure>
      <figure class="media-grid__item"><img src="table-tennis.webp" alt="Table tennis" /></figure>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Implement slide 5 — Games**

```html
<section class="slide" data-chap="day" data-theme="light" data-chapter="Outside work · プライベート">
  <div class="slide__inner media-split">
    <div>
      <div class="eyebrow r" style="--i:0">Outside work</div>
      <h2 class="h-md r" style="--i:1">Games I love</h2>
      <p class="jp-sub r" style="--i:2">好きなゲーム</p>
      <p class="lead r" style="--i:3; margin-top:1.2rem">I enjoy Minecraft, Dota 2, Valorant, and many other games. Gaming is one of my favorite ways to relax after work and spend time with friends.</p>
    </div>
    <div class="media-grid media-grid--3 r" style="--i:2">
      <figure class="media-grid__item"><img src="minecraft.jpg" alt="Minecraft" /></figure>
      <figure class="media-grid__item"><img src="dota-2.jpg" alt="Dota 2" /></figure>
      <figure class="media-grid__item"><img src="valorant.jpeg" alt="Valorant" /></figure>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Implement slide 6 — Anime / manga**

```html
<section class="slide" data-chap="day" data-theme="light" data-chapter="Outside work · プライベート">
  <div class="slide__inner media-split">
    <div>
      <div class="eyebrow r" style="--i:0">Outside work</div>
      <h2 class="h-md r" style="--i:1">Manga &amp; anime</h2>
      <p class="jp-sub r" style="--i:2">漫画・アニメ</p>
      <p class="lead r" style="--i:3; margin-top:1.2rem">I enjoy reading manga and watching anime across different genres. Favorites include Tokyo Ghoul, Attack on Titan, and more.</p>
    </div>
    <div class="media-grid media-grid--2 r" style="--i:2">
      <figure class="media-grid__item"><img src="tokyo-ghould.jpg" alt="Tokyo Ghoul" /></figure>
      <figure class="media-grid__item"><img src="attack-on-titan.jpg" alt="Attack on Titan" /></figure>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Verify image wiring**

Run:

```bash
for f in badminton.avif tennis.jpg table-tennis.webp minecraft.jpg dota-2.jpg valorant.jpeg tokyo-ghould.jpg attack-on-titan.jpg; do
  grep -q "src=\"$f\"" about-me.html && echo "OK $f" || echo "MISSING REF $f"
done
```

Expected: eight `OK …` lines. In browser open `#4`, `#5`, `#6` and confirm all images render (no broken icons).

- [ ] **Step 5: Commit assets + HTML**

```bash
git add about-me.html badminton.avif tennis.jpg table-tennis.webp minecraft.jpg dota-2.jpg valorant.jpeg tokyo-ghould.jpg attack-on-titan.jpg
git commit -m "$(cat <<'EOF'
Add sports, games, and anime slides with local images.

Wire the interest grids to assets already in the repo.
EOF
)"
```

---

### Task 4: Learning & family, Closing, README

**Files:**
- Modify: `about-me.html` (slides 7–8)
- Modify: `README.md` (about-me blurb)

**Interfaces:**
- Consumes: `.two-col`, `.cluster__label`, `.closing`, `.arigato`, `.contact`
- Produces: finished deck + docs sync

- [ ] **Step 1: Implement slide 7 — Learning & family**

```html
<section class="slide" data-chap="day" data-theme="light" data-chapter="Outside work · プライベート">
  <div class="slide__inner">
    <div class="eyebrow r" style="--i:0">Outside work</div>
    <h2 class="h-md r" style="--i:1">Always learning · time with family</h2>
    <p class="jp-sub r" style="--i:2">学び続けること、そして家族との時間</p>
    <div class="two-col r" style="--i:3">
      <div class="cluster">
        <div class="cluster__label">Exploring tech <span class="jp">新しい技術</span></div>
        <p class="lead">I like exploring new technology — especially AI and new software development tools — and trying things that help me grow as a developer.</p>
      </div>
      <div class="cluster">
        <div class="cluster__label">Family <span class="jp">家族</span></div>
        <p class="lead">I also enjoy spending quality time with my family — going out together, watching movies, or simply relaxing at home.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Implement slide 8 — Closing**

```html
<section class="slide" data-chap="day" data-theme="light" data-chapter="">
  <div class="slide__inner closing">
    <div class="eyebrow r" style="--i:0">Thank you</div>
    <h2 class="h-lg r" style="--i:1">Excited to meet everyone</h2>
    <p class="jp-sub r" style="--i:2">みなさんとお会いできてうれしいです</p>
    <p class="lead r" style="--i:3; margin-top:1.2rem; max-width:42ch">I’m excited to learn from your experiences and hopefully contribute my own knowledge as well.</p>
    <p class="jp r muted" style="--i:4; font-size:1rem; margin-top:.6rem; max-width:42ch">みなさんの経験から学び、私も知識を共有できたらうれしいです。</p>
    <div class="arigato r" style="--i:5">ありがとう</div>
    <div class="thanks-en r" style="--i:6">Thank you</div>
    <div class="contact r" style="--i:7">
      <a href="mailto:eirracyu12@gmail.com">eirracyu12@gmail.com</a>
      <span class="place">Cebu City, Philippines</span>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Update README about-me line**

In `README.md`, replace the about-me bullet with:

```markdown
- **[about-me.html](about-me.html)** — An 8-slide bilingual (EN + JP) self-introduction in the same sunrise visual language as the main deck — who I am, career, sports, games, anime, learning & family, thank you & contact.
```

- [ ] **Step 4: End-to-end verification**

Run:

```bash
# slide count + key copy + contact
test $(grep -c 'class="slide"' about-me.html) -eq 8 && echo SLIDES_OK
grep -F 'mailto:eirracyu12@gmail.com' about-me.html && echo MAIL_OK
grep -F 'Always learning · time with family' about-me.html && echo FAMILY_OK
grep -F '8-slide bilingual' README.md && echo README_OK

# no leftover cobalt tokens from old deck
! grep -q 'Space Grotesk\|--accent:#1B44FF\|Currently · Software Developer' about-me.html && echo NO_OLD_THEME
```

Expected: `SLIDES_OK`, `MAIL_OK`, `FAMILY_OK`, `README_OK`, `NO_OLD_THEME`.

Manual browser checklist:
1. Open `about-me.html` — cover portrait + bilingual hello
2. Arrow through all 8 slides; counter `08 / 08`
3. Dawn → rise → day backgrounds feel like `index.html`
4. `#4`–`#6` show all interest images
5. Narrow the window: cover stacks; grids become 2+1 / stack; two-col stacks
6. `#8` shows ありがとう + mailto

- [ ] **Step 5: Commit**

```bash
git add about-me.html README.md
git commit -m "$(cat <<'EOF'
Finish about-me closing slides and README sync.

Complete the bilingual sunrise intro with learning, family, and contact.
EOF
)"
```

---

## Spec coverage checklist

| Spec requirement | Task |
|------------------|------|
| Sunrise visual system from `index.html` | 1 |
| 8 slides, chapter attrs, bilingual chrome | 1–4 |
| Cover portrait `personal.png` | 2 |
| Who I am + Career + chips | 2 |
| Sports / Games / Anime grids with repo assets | 3 |
| Learning & family two-column | 4 |
| Closing thank-you + mailto | 4 |
| Missing-image remove cell | 1 |
| Reduced motion + print | 1 |
| README update | 4 |
| No edits to `index.html` / `qa-cheatsheet.html` | all |

## Self-review notes

- No TBD/placeholder steps remain; asset filenames match the repo (`tokyo-ghould.jpg` kept).
- Verification is grep + browser (no unit-test harness for this static HTML project).
- CSS class names introduced in Task 1 are the ones consumed in Tasks 2–4.
