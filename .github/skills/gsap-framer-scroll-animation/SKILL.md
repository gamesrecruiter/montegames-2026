---
name: gsap-framer-scroll-animation
description: >-
  Use this skill whenever the user wants to build scroll animations, scroll effects,
  parallax, scroll-triggered reveals, pinned sections, horizontal scroll, text animations,
  or any motion tied to scroll position — in vanilla JS, React, or Next.js.
  Covers GSAP ScrollTrigger (pinning, scrubbing, snapping, timelines, horizontal scroll,
  ScrollSmoother, matchMedia) and Framer Motion / Motion v12 (useScroll, useTransform,
  useSpring, whileInView, variants). Also triggers for "animate on scroll", "fade in as I scroll",
  "parallax effect", "sticky section", "scroll progress bar", or "entrance animation".
  Pairs with the premium-frontend-ui skill for creative philosophy and design-level polish.
---

# GSAP & Framer Motion — Scroll Animations Skill

Production-grade scroll animations with ready-to-use code recipes and deep API references.

> **Design Companion:** This skill provides the *technical implementation* for scroll-driven motion.
> For the *creative philosophy*, design principles, and premium aesthetics that should guide
> **how** and **when** to animate, always cross-reference the **premium-frontend-ui** skill.
> Together they form a complete approach: premium-frontend-ui decides the **what** and **why**;
> this skill delivers the **how**.

## Quick Library Selector

| Need | Use |
|---|---|
| Vanilla JS, Webflow, Vue | **GSAP** |
| Pinning, horizontal scroll, complex timelines | **GSAP** |
| React / Next.js, declarative style | **Framer Motion** |
| whileInView entrance animations | **Framer Motion** |
| Both in same Next.js app | See notes in references |

## Setup (Always Do First)

### GSAP
```bash
npm install gsap
```
```js
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger); // MUST call before any ScrollTrigger usage
```

### GSAP via CDN (this project)
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js" defer></script>
```
When using CDN, `gsap` is available globally. Always check `typeof gsap !== 'undefined'` before use.

### Framer Motion (Motion v12, 2025)
```bash
npm install motion   # new package name since mid-2025
# or: npm install framer-motion  — still works, same API
```
```js
import { motion, useScroll, useTransform, useSpring } from 'motion/react';
```

## Workflow

1. Interpret the user's intent to identify if GSAP or Framer Motion is the best fit.
2. Suggest the required package installation if not already present.
3. Implement the scaffold for the animation structure.
4. Apply the correct tools (scrolling vs in-view elements) ensuring accessibility options are present.
5. Hooks must not cause infinite re-renders.

## The 5 Most Common Scroll Patterns

### 1. Fade-in on enter (GSAP)
```js
gsap.from('.card', {
  opacity: 0, y: 50, stagger: 0.15, duration: 0.8,
  scrollTrigger: { trigger: '.card', start: 'top 85%' }
});
```

### 2. Fade-in on enter (Framer Motion)
```jsx
<motion.div
  initial={{ opacity: 0, y: 40 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, margin: '-80px' }}
  transition={{ duration: 0.6 }}
/>
```

### 3. Scrub / scroll-linked (GSAP)
```js
gsap.to('.hero-img', {
  scale: 1.3, opacity: 0, ease: 'none',
  scrollTrigger: { trigger: '.hero', start: 'top top', end: 'bottom top', scrub: true }
});
```

### 4. Scroll-linked (Framer Motion)
```jsx
const { scrollYProgress } = useScroll({ target: ref, offset: ['start end', 'end start'] });
const y = useTransform(scrollYProgress, [0, 1], [0, -100]);
return <motion.div style={{ y }} />;
```

### 5. Pinned timeline (GSAP)
```js
const tl = gsap.timeline({
  scrollTrigger: { trigger: '.section', pin: true, scrub: 1, start: 'top top', end: '+=200%' }
});
tl.from('.title', { opacity: 0, y: 60 }).from('.img', { scale: 0.85 });
```

## Critical Rules (Apply Always)

- **GSAP**: always call `gsap.registerPlugin(ScrollTrigger)` before using it
- **GSAP scrub**: always use `ease: 'none'` — easing feels wrong when scrub is active
- **GSAP React**: use `useGSAP` from `@gsap/react`, never plain `useEffect` — it auto-cleans ScrollTriggers
- **GSAP debug**: add `markers: true` during development; remove before production
- **Framer**: `useTransform` output must go into `style` prop of a `motion.*` element, not a plain div
- **Framer Next.js**: always add `'use client'` at top of any file using motion hooks
- **Both**: animate only `transform` and `opacity` — avoid `width`, `height`, `box-shadow`
- **Accessibility**: always check `prefers-reduced-motion` — disable or simplify animations accordingly
- **Premium polish**: follow the **premium-frontend-ui** skill principles for motion timing, easing curves, and restraint — animation should enhance, never overwhelm

## Related Skills

| Skill | Relationship |
|---|---|
| **premium-frontend-ui** | Creative philosophy, design principles, and aesthetic guidelines — defines *when* and *why* to animate |
