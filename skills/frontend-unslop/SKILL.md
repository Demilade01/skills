---
name: frontend-unslop
description: Design and build distinctive, non-generic frontends (landing pages, marketing sites, dashboards, web apps, mobile app screens, UI components) by planning before coding (PRD, section copy, design tokens, layout) so the result does not look AI-generated. Use this whenever the user wants to design, build, restyle, polish or review any frontend or UI, mentions a landing page, hero, dashboard, sidebar, pricing section, design system, component or screen, says "make it look less AI", or has a backend/API/schema mapped and needs the frontend built on it. Use it even if they only say "build the UI" or "make the frontend" and never mention design.
---

# Frontend Unslop

Default AI output has a recognisable look. Layout is the biggest tell, bigger than colour, icons or fonts. The fix is planning before building. Never go from a bare prompt straight to UI.

Numeric caps below (weights, line counts, colour counts) are defaults. If the user or brand needs otherwise, the user wins.

## Modes

- **Site mode**: landing or marketing site. Input is the idea.
- **App mode**: product UI (web, mobile, dashboard). Input is the backend map: entities, endpoints or API contracts, roles, async/realtime behaviour. If it is missing, read the repo (schema, OpenAPI, types, routes) or ask for it. Never invent endpoints. List gaps as "needs backend".

Both modes run the same pipeline. App mode adds step 2b.

## Pipeline

Keep every planning file as Markdown in `/design`. Reuse files that already exist, do not regenerate them. Do not build UI until `design.md` exists and the design-system page is approved (or the user says skip).

1. Idea. Rough is fine.
2. PRD → `design/prd.md`
2b. App map (app mode) → `design/app-map.md`
3. Copy → `design/copy/<section>.md`
4. Tokens + design-system page → `design/design.md` + `/design-system` route
5. Build, one section or screen at a time
6. Mobile and polish pass, one section at a time

## 2. PRD

Contents: must-haves, nice-to-haves, functional requirements, non-functional requirements, audience, colour suggestions with hex codes, design direction (tone, corner style: fully rounded or fully sharp, 3 reference adjectives).

## 2b. App map (app mode)

Derive from the backend map:

- **Roles/permissions** decide which nav items and actions each role sees.
- **Entities** become list, detail and create/edit screens. Field types pick the control: enum → select/segmented, bool → switch, date → date picker, money → formatted with currency.
- **Enums/status fields** become status tokens. One colour per state, used only where the state is shown.
- **Endpoints** map to screen data needs. Mark each as list, detail, mutation or stream. Note pagination, filter and sort.
- **Every data view gets four designed states**: loading (skeleton), empty (with next action), error (with retry), populated. Add stale/partial for realtime.
- **Mutations**: optimistic or not, confirm on destructive, visible success and failure feedback.
- **Flows**: write the 3 to 5 primary user flows as screen sequences. One primary action per screen.
- **Navigation**: 7 top-level destinations at most. Mobile uses a bottom tab bar of 5 or fewer, touch targets 44px or larger.
- **Async/realtime** (jobs, websockets): live indicators and progress UI.
- **Auth**: login, signup, reset, session expiry.

Frontend contract: generate a typed API client from OpenAPI or the schema when available. Build a mock layer matching the contract so UI can ship before the backend does. Keep fixtures in one place, never hardcoded in components.

## 3. Copy

One `.md` per section (`hero.md`, `features.md`, `pricing.md`). In app mode add `microcopy.md` for empty states, errors, buttons and onboarding.

- Headings 2 lines max, subtitles 3 lines max. AI over-talks and long text wrecks layout.
- Say the point directly. Ban: "Revolutionize", "Unlock the full potential", "seamless", "Lightning fast", "It's not just X, it's Y".
- No invented stats, testimonials or logos. Use real numbers or cut the section.
- Read it as the audience would. If it would confuse them, rewrite.
- Run the `humanizer` skill if installed, otherwise do a manual pass removing AI-sounding patterns.

## 4. Tokens and design-system page

`design/design.md` defines:

- **Colour**: 2 brand colours max, calm neutrals, status colours. Named tokens: `--background --card --muted --border --foreground --muted-foreground --subtle --brand` plus `--status-*`. Components use token names, never raw hex. Forbid any colour outside the tokens. One job per colour.
- **Contrast**: body text 4.5:1, large text 3:1. Test pairs (WebAIM or similar) before saving. AI picks palettes fine and applies them badly. Define light and dark sets if dark mode is wanted.
- **Type**: one font, or one heading plus one body. Regular 400 and medium 500 only, titles regular, nothing heavier than `font-medium`. Start scale: heading 32 / body 16 / caption 12.
- **Radius**: fully rounded or fully sharp, one scale. Icon corners must match it.
- **Spacing**: one scale.
- **Gradients**: 2 token colours max, soft, linear or one radial glow from the bottom. Never decorative rainbow.
- **Shadows**: none on hover.
- **Motion**: named durations and easings.

Build the design-system page before any real screen. It opens with one plain line: the tokens and components the product is built from, and that changes happen here first. It shows colours, type, spacing and radius, buttons, fields, controls, tabs, status chips, icons and feedback (toast/alert). In app mode also table, list row, sidebar, modal, and loading/empty/error states.

Then stop and show the user. If they dislike a piece (button, input), they may bring a reference from 21st.dev or React Bits. Adapt it to the tokens. After approval, every later screen reads colours, type, radius and spacing from this page and nowhere else. An optional assets page holds logos, images and illustrations.

## 5. Build

One section or screen at a time from the `/design` files.

**Borrowed references** (screenshot or component code): take the layout only. Text comes from `copy/`, colours from `design.md`. First describe what the reference shows (cards, tags, colours, shadows) so details are not missed. If you cannot browse inspiration sites, ask the user for screenshots instead of guessing.

### Site layout

Order: Header, Hero, Trust, Problem, Solution, Pricing, FAQ, CTA, Footer. Keep every section short.

- **Header**: floating pill, or no background until scroll, or logo plus menu button. Text 2 lines max.
- **Hero**: centred. 2-line headline, 3-line subtitle, 1 or 2 buttons, product image peeking in from the bottom or side. Title never bold. For a left/right split, bring the image in from the edge so it does not float alone.
- **Background**: never bland. Grid, animated pattern or soft gradient. Reuse it in the CTA.
- **Trust**: logo marquee or a few real testimonials. No customers yet means skip the section.
- **Problem**: show you understand their pain, with an image or illustration.
- **Solution**: bento grid with small illustrations. Never six identical icon cards.
- **Pricing**: lift a card layout from a reference, apply own tokens and copy.
- **FAQ**: calm, narrow column, plain dividers not a card per question, first answer open.
- **CTA**: centred, 2 lines max, one button, hero background, no unrelated illustration. Best place to show design skill.
- **Footer**: 4 columns max (nav, contact/about, legal). Social icons under the logo. No careers column unless real and hiring.
- **Optional signature section**: one unusual section reused as the personal style.
- **Illustrations**: unDraw (recolour to tokens), custom SVG, or generated. One style per page.

### App layout

Never ship the default: sidebar + header + 4 metric cards + 2 charts.

- Custom sidebar: floating, or collapsible to icons with tooltips. Clear active state (tinted row plus edge marker), small group labels, settings and log out pinned at the bottom. Design icon rail, full sidebar, profile menu and workspace switcher as one set.
- Move the header inside the content area.
- Lead with one large work surface (main chart, table or board) instead of equal metric cards.
- Tables: sticky header, row hover, filters above, bulk actions where multi-select makes sense.
- Forms: labels above, inline validation, one primary action, loading and disabled state on submit.
- Status chips come from the enum tokens.
- Native mobile (React Native, Flutter, Swift): same tokens, platform navigation patterns.

### Buttons and motion

- Fully rounded or fully sharp. More than a colour: icon inside that animates on hover (slides).
- Border beam or texture buttons (React Bits, 21st.dev, Cult UI) are the fastest non-AI look. Adapt to tokens first or they clash.
- Micro-interactions go on buttons, cards and text. Name the effect exactly ("icon slides 4px right on hover, 150ms ease-out", "typing text animation").
- Restraint. Too much animation makes people watch effects and forget why they came. Honour `prefers-reduced-motion`.
- Keyboard focus states on everything interactive.

## 6. Mobile and polish

Most visitors are on phones. Never ask for the whole page at once. Per section or screen, run:

"[Section]: make this more responsive on mobile and tablet without changing the desktop layout."

It mostly reduces padding, text size and button size. Repeat for every section. Then check long names, empty lists and a slow network.

## Slop tells (never ship)

| Tell | Fix |
|---|---|
| Gradients and transparency everywhere | 2 brand colours max, soft gradient |
| Inter in heavy weights | One other font, max medium |
| Default Lucide icons (shadcn ships them) | Swap library, match corners to button radius |
| Image left, text right hero | Centred hero, image peeks in |
| Sidebar, header, 4 metric cards | Custom shell, one large surface |
| Headings wrapping to many lines | 2 lines max, shorter copy |
| Fake stats (1M+, 99.9%, 24/7) | Real numbers or remove |
| Six identical gradient-emoji feature cards | Bento grid with illustrations |
| Card-in-card in every section | Plain dividers, flat sections |
| Hover shadows | Icon or colour motion instead |
| Emoji in badges and buttons | Icons from the chosen set |

## Resources (pick one per need, do not dump)

Prefer free options unless the user has licences. Check licences before shipping fonts and illustrations commercially.

- **Fonts**
  - Headings: Funnel Display, Instrument Serif, Playfair Display, Syne, Chakra Petch, PP Kyoto, PP Radio Grotesk, Pitanga, Neulis, Vivaldi
  - Body: DM Sans, Hanken Grotesk, Instrument Sans, Avenir Next
  - Both: Geist, Satoshi, Outfit, Schibsted Grotesk, Host Grotesk, Onest, Aspekta, ES Rebond Grotesque
  - Free sources: Google Fonts, Fontshare, Geist, Aspekta. Skip Inter.
- **Icons**: Hugeicons (Rounded Stroke is free, Sharp family for sharp layouts), Iconsax (free, credit author, React and React Native), Phosphor, Tabler, Remix, Iconoir, Radix, Nucleo. React Icons for colourful brand logos.
- **Colour**: Coolors, Realtime Colors, Huemint, Adobe Color, Radix Colors, OKLCH.com, WebAIM Contrast Checker.
- **Components**: 21st.dev, React Bits, Aceternity UI, Magic UI, Cult UI, Skiper UI, shadcn/ui (base layer). Motion: Motion, LottieFiles, Rive.
- **Inspiration**: Pinterest, Dribbble, Mobbin (real app screens, best for app mode), Land-book, Godly, Saaspo, SaaS UI, Lapa Ninja, Awwwards, Refero.
- **Illustration**: unDraw, Open Peeps, Storyset, Blush.
- **Companion skills (optional)**: Impeccable (anti-slop design), humanizer (blader/humanizer), Emil Kowalski skills (motion), Jakub Krehel skills (better-ui, better-typography, better-colors, better-layout, interface-review). Verify repo names before installing.

## Done checklist

- [ ] `prd.md`, `copy/`, `design.md` exist, plus `app-map.md` in app mode
- [ ] Design-system page approved, all screens read from it
- [ ] No raw hex or off-token colours in components
- [ ] No slop-table items remain
- [ ] Every data view has loading, empty, error states (app mode)
- [ ] Contrast passes, focus states present
- [ ] Mobile checked per section
- [ ] No invented stats, logos or testimonials
