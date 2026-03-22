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

# Digitize Exhibition

Transform ephemeral physical exhibitions into persistent digital experiences. A website is itself a form of exhibition — the digital counterpart of a physical show. The difference: physical space has a deadline, digital space does not.

This skill guides through a **4-phase process**: Brief → Design → Build → Deploy. The entire pipeline is designed for rapid turnaround (half a day or less) while maintaining high design quality.

**The most important phase is Design.** When AI makes coding nearly free, the differentiator is taste. Rushing past design to get to code is the single biggest mistake. Spend the majority of creative energy on Phase 2.

---

## Phase 1: Exhibition Brief

Before anything else, understand what you're working with. This is a structured conversation — ask these questions and don't proceed until you have clear answers.

### What to ask

**The Exhibition**
- What is being exhibited? (artworks, furniture, photography, products, installations...)
- Who is the designer/artist/creator?
- What is the exhibition's name or title?
- Where and when does/did it take place?
- Who is organizing or presenting it?

**The Narrative**
This is the most important input. Every exhibition has a story — a reason it exists beyond "here are some things to look at." Ask:
- What concept, philosophy, or idea does this exhibition communicate?
- Why should someone care about these works?
- What should a visitor feel or understand after seeing the exhibition?
- Is there historical, cultural, or design context that enriches the works?

Push the user to articulate this clearly. A vague "it's a furniture show" is not enough. "Twelve pieces of mid-century furniture that embody the tension between industrial rationalism and handcraft warmth" is a narrative.

**The Content**
Users provide two categories of material:
1. **Text** — exhibition descriptions, artist statements, individual work descriptions, provenance, dates, materials, dimensions
2. **Media** — photographs of works (often shot on-site during setup), video, floor plans, installation views

Ask explicitly: What images do you have? Are they final or will more come from the venue? (On-site photography often arrives last — the deployment pipeline must accommodate late-arriving images.)

**The Audience**
- Who will visit this site? Collectors, enthusiasts, general public, press?
- What language(s)? (If Chinese audience: plan for bilingual Chinese + English from the start)

**Brand & Identity**
- Does the organizer have a logo, existing website, or brand guidelines?
- Any existing design language to match or extend?

### Output of Phase 1

Synthesize into a concise **Exhibition Brief** — a short document (can be a markdown block in the conversation) that captures: what, who, why, for whom, and with what materials. Confirm with the user before proceeding.

---

## Phase 2: Design Direction

This is where the exhibition becomes a website. Design is not decoration — it's the structure that makes content intelligible and emotionally resonant. The goal is to create a digital space that has the same atmosphere as the physical exhibition.

### Step 2a: Aesthetic Positioning

Start by establishing the visual tone through **references and anti-references**:

**Ask the user:**
- What feeling should the site convey? (e.g., "restrained and trustworthy" vs. "energetic and playful")
- Are there websites, galleries, magazines, or physical spaces whose aesthetic you admire?
- What should the site absolutely NOT look like?

**If the user can't articulate this**, propose 2-3 directions based on the exhibition content. For example:
- **White Cube** — gallery walls, generous whitespace, works speak for themselves (suits fine art, design objects)
- **Editorial** — magazine-like, strong typography, narrative-driven (suits photography, cultural exhibitions)
- **Immersive** — dark background, full-bleed images, cinematic (suits installations, experiential shows)

Each direction implies different typography, color, spacing, and layout decisions. Get alignment before moving forward.

### Step 2b: Design Tokens

Once the direction is set, define the concrete design system:

**Typography** — Choose 2-3 fonts with clear roles:
- Display/titles (the voice of the exhibition)
- Body/information (readable, recedes behind content)
- Accent/signature (optional: designer attribution, captions)

Avoid generic AI defaults (Inter, Roboto, Arial as primary). Choose fonts that have character and match the exhibition's tone. Google Fonts is fine — the selection matters more than the source.

**Color** — Define a minimal palette:
- Background (sets the "room")
- Primary text
- Secondary text (for supporting information)
- Tertiary text (for metadata, captions)
- Borders/dividers
- Optional accent (used sparingly: CTA, links, highlights)

For gallery-like exhibitions, warm neutrals often work better than pure black/white. Avoid colored accents unless they connect to the exhibition content (e.g., a teak color for wood furniture).

**Spacing** — Establish a base unit (4px or 8px) and a vertical rhythm (typically tied to body line-height). Generous spacing signals confidence and quality. Cramped spacing signals commerce.

**Motion** — Less is more. Scroll-triggered fade-ins, subtle hover states. No bounce, no elastic, no gratuitous animation. Motion should feel like the content is gently revealing itself, not performing.

### Step 2c: Anti-Patterns (What to Avoid)

These destroy the credibility of a digital exhibition:

- **AI Slop aesthetics** — dark backgrounds with cyan/purple gradients, glassmorphism, neon accents, card-heavy layouts with drop shadows. These are the visual equivalent of stock photography.
- **E-commerce patterns** — "Add to Cart" buttons, price tags front-and-center, promotional banners, countdown timers. Even if works are for sale, the site should feel like a gallery, not a shop.
- **Over-decoration** — Excessive borders, gradients, rounded corners, background patterns. Every visual element must earn its place.
- **Information overload** — Showing everything at once. Exhibition design is about sequence, reveal, and pacing. The scroll is your gallery corridor.
- **Generic structure** — Cookie-cutter hero + 3-column grid + footer. The site structure should emerge from the content, not from a template.

### Step 2d: Design Brief

Compile the design decisions into a brief:

```
## Design Brief
- **Aesthetic**: [direction name and 1-sentence description]
- **Fonts**: [display] / [body] / [accent]
- **Colors**: [background] / [text levels] / [accent if any]
- **Spacing**: [base unit, vertical rhythm]
- **Tone**: [2-3 adjectives]
- **Anti-references**: [what to explicitly avoid]
```

Confirm with the user. This document governs all subsequent implementation.

---

## Phase 3: Build

Now translate the design brief into working code. The goal is a production-ready, single-file HTML page that loads fast and works on all devices.

### Architecture

**Single-file HTML** with inline `<style>` and `<script>`. This approach is ideal for exhibition sites because:
- Zero build tooling — no npm, no bundler, no framework
- Trivially deployable — one file, any hosting
- Self-contained — the entire exhibition in one document
- Easy to hand off — anyone can open and understand it

For larger exhibitions (50+ works, complex interactions), consider a lightweight framework. But for most pop-ups and gallery shows, a single HTML file is the right tool.

### Page Structure

A typical exhibition site flows like this:

```
Navigation        — Logo + minimal links
Hero              — Exhibition title, subtitle, dates, venue
Introduction      — The narrative (from Phase 1)
─── divider ───
Works             — Individual pieces, each with:
                    • Title (display font)
                    • Model/catalog number
                    • Image(s)
                    • Details (year, origin, material)
                    • Description (the story of this piece)
─── divider ───
About             — Exhibition context, organizer info
Group Image       — All works together (if available)
Footer            — Contact, credits, copyright
```

This is a starting point, not a mandate. Adapt the structure to the content.

### Implementation Principles

**Images are everything.** Exhibition sites live or die by their photography. Use:
- `loading="lazy"` on all images below the fold
- Explicit `width` and `height` attributes to prevent layout shift
- `object-fit: contain` (not `cover`) for artwork — never crop the work
- Subtle hover scale (1.02×) for interactivity
- Consider multiple views for 3D objects (front + side, grid layout)

**Typography hierarchy is the design.** In a minimal site, type does all the heavy lifting:
- Work titles: large, display font, commanding
- Designer/artist attribution: italic serif, slightly smaller, secondary
- Metadata (year, material, origin): small, uppercase, tertiary color
- Descriptions: comfortable reading size, generous line-height (1.8–1.9)

**Responsive from the start.** Exhibition sites are often shared via WeChat, Instagram, or messaging — most traffic is mobile. Design for phone first, then ensure desktop is equally considered.

**Scroll-triggered reveals.** Use IntersectionObserver to fade in sections as the user scrolls. This creates pacing — the digital equivalent of walking through gallery rooms. Keep transitions gentle (0.7–0.8s, ease-out).

**Performance.** The site must load fast, especially if targeting Chinese audiences on mobile. Minimize external dependencies. Google Fonts is acceptable (use `display=swap` and `preconnect`). Compress images before deployment.

### Content Writing

When writing or refining exhibition copy:
- Use **multiple AI agents in parallel** to research facts (dates, provenance, model numbers, historical context) from different sources, then cross-reference
- **Human review is mandatory.** Internet information about art and design objects is inconsistent across publications, auction records, and museum databases. AI-researched facts must be verified by a knowledgeable human before publishing. This step is not optional.
- Match the copy's voice to the exhibition's tone. Gallery copy is concise, authoritative, and avoids superlatives. It states rather than sells.

---

## Phase 4: Deploy

### Quick-Start Stack

| Tool | Role |
|------|------|
| GitHub | Code versioning and collaboration |
| Vercel / Netlify | Auto-deploy from git push |
| Cloudflare | CDN, DNS, and regional access optimization |
| A coding agent | AI-assisted development (Claude Code, Cursor, etc.) |

### Domain

If targeting a Chinese audience: 国内域名需要 ICP 备案（备案），如果时间充裕，优先完成备案——这对长期运营的站点更合规也更稳定。如果展览时间紧迫、备案来不及，可以选用国际域名和国际托管方案（如 `.com` 或 `.art` 配合 Cloudflare DNS），注册后即可使用。

### Deployment Flow

```
Local editing → git push → Auto-deploy (seconds) → Live site
```

This fast feedback loop is critical for exhibition sites because:
- On-site photos arrive during setup, often hours before opening
- Copy gets refined based on physical installation
- Last-minute changes (work substitutions, sequence adjustments) are common

Every `git push` should result in a live update within seconds.

### China Access Optimization

If the audience includes users in mainland China:
1. Use Cloudflare as DNS and CDN proxy
2. Optimize images aggressively (WebP, compressed JPEGs)
3. Minimize external resource dependencies
4. Test from within China before the exhibition opens

### Cross-Linking

If this exhibition site relates to a main website, gallery page, or other exhibition:
- Add navigation links between them
- Maintain consistent brand identity across pages
- Consider a "How This Was Made" companion page to document the process

---

## Workflow Summary

```
1. BRIEF    Ask → Listen → Synthesize → Confirm
                ↓
2. DESIGN   Position → Tokens → Anti-patterns → Brief → Confirm
                ↓
3. BUILD    Structure → Implement → Populate → Refine
                ↓
4. DEPLOY   Git → Vercel → Domain → CDN → Live
                ↓
            Iterate (on-site photos, copy refinements, human review)
```

The entire process is designed to complete in half a day. Phase 1 and 2 take the most human attention. Phase 3 and 4 are primarily AI-executed with human review checkpoints.
