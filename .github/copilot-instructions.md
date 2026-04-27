# MonteGames Sponsorship Deck — Copilot Context

## Project Overview
Ultra-premium single-file interactive sponsorship deck for MonteGames 2026, a gaming industry conference (Oct 2–4, Porto Montenegro). Pitched to ByteDance, NetEase, Apple, Google, and similar tier-1 companies.

## Architecture
- **Single file**: `index.html` — all HTML, CSS, and JS in one self-contained file
- **CDN dependencies only**: Google Fonts (Inter, Playfair Display), GSAP 3.x
- **No build system**: No npm, no bundler, no framework. Vanilla JS + CSS
- **9 slides**: Cover, Opportunity, Who's in the Room, Why It Works, Outcomes, Tiers, Comparison, Branding, CTA

## Design Language
- **Aesthetic**: Cyber/Technical + Cinematic Pacing (per premium-frontend-ui skill)
- **Colors**: Dark bg (#0a0a0f), gold accents (#c8a45c), off-white text (#f0ede6)
- **Typography**: Inter for UI/body, Playfair Display for serif headline accents
- **Effects**: Canvas particle system, gradient orbs, film grain overlay, cursor glow, GSAP transitions

## Key Features
- GSAP-powered slide transitions with staggered reveal animations
- Company personalization via `?for=bytedance|apple|google|netease` URL params
- Animated stat counters on slide 2
- Feature card tilt on hover (CSS perspective)
- Presenter mode (P key), fullscreen (F key), shortcuts (? key)
- Web Audio synthesized transition sounds (off by default)
- Progress bar + dot navigation + arrow buttons + keyboard + touch + scroll

## Performance Rules
- Animate only `transform` and `opacity` — never `width`, `height`, `top`, `margin`
- Canvas particles < 2ms/frame, pause when tab hidden
- Wrap cursor/tilt effects in `@media (hover: hover) and (pointer: fine)`
- Respect `prefers-reduced-motion: reduce`
- Print stylesheet renders all slides vertically

## Installed Skills (`.github/skills/`)

### Production Skills
| Skill | Purpose |
|-------|---------|
| **premium-frontend-ui** | Cinematic pacing, editorial typography, cursor interactions, atmospheric filters, performance imperatives. Defines the Cyber/Technical + Cinematic Pacing aesthetic. |
| **gsap-framer-scroll-animation** | GSAP ScrollTrigger recipes, timeline patterns, staggered reveals. Technical companion to premium-frontend-ui. |
| **web-coder** | 15-competency web expert: Canvas API, SVG, Web Audio, performance (Core Web Vitals), accessibility (WCAG), responsive design. |
| **web-design-reviewer** | Visual QA: layout, responsiveness at 375/768/1280/1920px, accessibility contrast, visual consistency. |
| **game-engine** | Canvas particle system, requestAnimationFrame game loop, Web Audio API for synthesized sound, real-time rendering optimization. |
| **publish-to-pages** | One-shot GitHub Pages deployment: creates repo, pushes index.html, enables Pages, returns live URL. |
| **karpathy-guidelines** | Four behavioral rules to cut LLM coding mistakes: Think Before Coding, Simplicity First, Surgical Changes, Goal-Driven Execution. Apply on every code edit. |

### GTM Strategy Skills
| Skill | Purpose |
|-------|---------|
| **gtm-partnership-architecture** | Three-Tier Partner Model, value exchange clarity, partnership charter, co-marketing checklists. Shapes sponsorship tier structure. |
| **gtm-positioning-strategy** | Word choice that converts, headline/sub-headline testing, Crawl-Walk-Run rollout. Shapes deck copy and pitch approach. |
| **gtm-enterprise-account-planning** | Personal Win Mapping per target company (ByteDance, Apple, Google), MEDDICC framework, MAP health tracking. |
| **gtm-0-to-1-launch** | Direct outreach > press, 2-week experiment cycle, three-layer diagnosis if engagement stalls. |

### Marketing Skills (from coreyhaines31/marketingskills)
| Skill | Purpose |
|-------|---------|
| **product-marketing-context** | Foundation skill — defines product, audience, positioning. Other marketing skills check this first. |
| **sales-enablement** | Pitch decks, one-pagers, objection handling, demo scripts. Most directly relevant to this sponsorship deck. |
| **copywriting** | Marketing page copy frameworks for headlines, hero sections, CTAs. Apply to deck slide copy. |
| **page-cro** | Conversion optimization for the deck page itself — hero clarity, CTA placement, friction reduction. |
| **cold-email** | B2B cold outreach to sponsor decision-makers (ByteDance, Apple, Google, NetEase) with reply-driving sequences. |
| **marketing-psychology** | Mental models, persuasion principles, behavioral science applied to deck framing and tier presentation. |
| **launch-strategy** | Plan the deck rollout / outreach launch as a coordinated campaign. |

## When Editing
- All changes go in `index.html` — there are no other source files
- Keep self-contained: no external files except CDN links
- Maintain existing CSS variable system (--bg, --surface, --border, --gold, etc.)
- Test at 375px, 768px, 1280px, 1920px viewports
