---
name: exhibit-to-web
description: >
  Rapidly convert offline exhibitions, pop-ups, gallery shows, and ephemeral events into polished
  digital exhibition websites. Use this skill whenever the user wants to create or build a website
  for an exhibition, gallery show, pop-up event, art show, market, or any time-limited physical
  event that needs digital preservation. Also triggers on keywords like "exhibition website",
  "gallery site", "pop-up site", "digitize exhibition", "online exhibition", "展览网站",
  "线上展览", "展览线上化", "数字展览", "展览页面", "做一个展览网页", or when someone describes
  a physical event and wants to bring it online. Even if they just say "build a site for my show"
  or "I need a page for this weekend's event" — this skill applies.
---

# exhibit-to-web

Transform ephemeral physical exhibitions into persistent digital experiences. A website is itself a form of exhibition — the digital counterpart of a physical show. Physical space has a deadline; digital space does not.

**Four-phase workflow**: Brief → Design → Build → Deploy. Designed for half-a-day turnaround.

**The most important phase is Design.** When AI makes coding nearly free, the differentiator is taste. Rushing past design to get to code is the single biggest mistake.

---

## Phase 1: Brief

Structured conversation to understand the exhibition. Don't proceed until answers are clear.

**Ask about:**
- **The exhibition** — What's shown, by whom, where, when, who's presenting
- **The narrative** — The concept/philosophy behind the works. Push for specificity: "twelve pieces embodying the tension between industrial rationalism and handcraft warmth" > "a furniture show"
- **Content inventory** — Two categories: text (descriptions, provenance, dates, materials) and media (photos, video). Ask if images are final or if more will arrive from venue setup
- **Audience** — Collectors, enthusiasts, press? Language needs? (Chinese audience → bilingual from the start)
- **Brand** — Existing logo, website, design guidelines to match?

**Output:** A concise Exhibition Brief confirming what, who, why, for whom, with what. Get user sign-off before proceeding.

---

## Phase 2: Design

Design is not decoration — it's the structure that makes content intelligible and emotionally resonant. The goal: a digital space with the same atmosphere as the physical exhibition.

### Aesthetic Positioning

Ask for references and anti-references. If the user can't articulate preferences, propose 2-3 directions:

| Direction | Suits | Character |
|-----------|-------|-----------|
| **White Cube** | Fine art, design objects | Gallery walls, generous whitespace, works speak |
| **Editorial** | Photography, cultural shows | Magazine-like, strong typography, narrative-driven |
| **Immersive** | Installations, experiential | Dark background, full-bleed images, cinematic |

### Design Tokens

Once direction is set, define:

- **Typography** — 2-3 fonts with clear roles (display / body / accent). Avoid generic defaults (Inter, Roboto as primary). Choose fonts with character.
- **Color** — Minimal palette: background, 3 text levels, borders, optional accent. Warm neutrals > pure black/white for gallery sites.
- **Spacing** — 4px or 8px base unit, vertical rhythm tied to line-height. Generous spacing = confidence. Cramped = commerce.
- **Motion** — Scroll-triggered fade-ins, subtle hovers. No bounce, no elastic. Content reveals itself gently.

### Anti-Patterns

These destroy credibility:
- **AI Slop** — dark + cyan/purple gradients, glassmorphism, neon, card-heavy drop shadows
- **E-commerce** — cart buttons, price tags, promotional banners, countdown timers
- **Over-decoration** — excessive borders, gradients, rounded corners. Every element earns its place
- **Information overload** — the scroll is a gallery corridor, not a data dump

### Design Brief

Compile decisions, confirm with user before coding:

```
Aesthetic:      [direction + 1-sentence description]
Fonts:          [display] / [body] / [accent]
Colors:         [background] / [text levels] / [accent]
Spacing:        [base unit, vertical rhythm]
Tone:           [2-3 adjectives]
Anti-references: [what to avoid]
```

---

## Phase 3: Build

Single-file HTML with inline `<style>` and `<script>`. Zero build tooling, trivially deployable, self-contained.

### Page Structure

```
Navigation    Logo + minimal links
Hero          Title, subtitle, dates, venue
Introduction  The narrative
─── divider ───
Works         Each: title → image(s) → details → description
─── divider ───
About         Exhibition context, organizer
Footer        Contact, credits, copyright
```

### Implementation Rules

- **Images** — `loading="lazy"`, explicit `width`/`height`, `object-fit: contain` (never crop artwork), subtle hover scale (1.02×)
- **Typography hierarchy** — Display font for titles, italic serif for attribution, small uppercase for metadata, comfortable body (line-height 1.8–1.9)
- **Mobile first** — Most traffic arrives via WeChat/messaging. Phone → desktop, not the reverse
- **Scroll reveals** — IntersectionObserver, 0.7–0.8s ease-out. Digital equivalent of walking between gallery rooms
- **Performance** — Compress images, `preconnect` Google Fonts, minimize external dependencies

### Content Research

- Use **multiple AI agents in parallel** to research facts from different sources, then cross-reference
- **Human review is mandatory** — internet information about art/design objects is inconsistent. AI-researched facts must be verified by a knowledgeable human. Not optional.
- Gallery copy is concise, authoritative. It states, not sells.

---

## Phase 4: Deploy

### Stack

| Tool | Role |
|------|------|
| GitHub | Version control |
| Vercel / Netlify | Auto-deploy on push |
| Cloudflare | CDN + China access optimization |
| Coding agent | Claude Code, Cursor, etc. |

### Key Decisions

- **Domain** — 国内域名需要 ICP 备案，时间充裕时优先完成。时间紧迫时，国际域名（`.com` / `.art`）配合 Cloudflare DNS 可即时使用
- **Deploy loop** — `git push` → live in seconds. Critical because on-site photos often arrive hours before opening
- **China access** — Cloudflare CDN, aggressive image compression, minimize external resources, test from within China before opening
- **Cross-linking** — Connect to main website, other exhibitions. Consider a "How This Was Made" companion page

### Workflow

```
BRIEF   → Ask, listen, synthesize, confirm
DESIGN  → Position, tokens, anti-patterns, brief, confirm
BUILD   → Structure, implement, populate, refine
DEPLOY  → Git, Vercel, domain, CDN, live
          ↓
        Iterate (on-site photos, copy refinements, human review)
```

Phase 1–2: most human attention. Phase 3–4: primarily AI-executed with human review checkpoints.
