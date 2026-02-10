<div align="center">
  <img src="public/web-app-manifest-512x512.png" alt="Logo" width="120" />
  <h1>Sagi Menahem - Portfolio</h1>
  <p>High-performance portfolio with immersive 3D visuals</p>
  <br />
  <a href="https://sagimenahem.tech">
    <img src="https://img.shields.io/badge/View_Live-sagimenahem.tech-0D2440?style=for-the-badge&logo=vercel&logoColor=white" alt="Live Site" />
  </a>
  <br /><br />
  <img src="https://img.shields.io/badge/Lighthouse-95+-4ade80?style=flat-square&logo=lighthouse&logoColor=white" alt="Lighthouse" />
  <img src="https://img.shields.io/badge/Accessibility-100-4ade80?style=flat-square" alt="Accessibility" />
  <br /><br />
  <img src="https://img.shields.io/badge/Astro_5-FF5D01?style=flat-square&logo=astro&logoColor=white" alt="Astro" />
  <img src="https://img.shields.io/badge/React_19-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React" />
  <img src="https://img.shields.io/badge/Three.js-000000?style=flat-square&logo=threedotjs&logoColor=white" alt="Three.js" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tailwind_v4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" alt="Tailwind" />
  <img src="https://img.shields.io/badge/GSAP-88CE02?style=flat-square&logo=greensock&logoColor=black" alt="GSAP" />
</div>

<br />

## Overview

A portfolio website combining modern web technologies with immersive 3D visuals. Features GPU-accelerated particle backgrounds, scroll-synchronized animations, and a cinematic preloader.

- Custom GLSL shaders for real-time particle physics (12,000 particles at 60fps)
- Infinite fly-through animation synced to scroll
- Progressive SVG line drawing
- Terminal boot preloader with typewriter effect

<br />

## Architecture

### Canvas/DOM Separation

Strict boundary between 3D and DOM concerns:

```
src/components/
├── canvas/     # Three.js only — no HTML
└── dom/        # React only — no Three.js
```

### Dual-Frequency State

| System | Rate | Purpose |
|:-------|:-----|:--------|
| `scrollRef` | 60fps | 3D animations (no re-renders) |
| Zustand | ~1fps | UI state (nav, sections) |

### Staggered Initialization

| Component | Desktop | Mobile |
|:----------|:--------|:-------|
| DataParticles | 100ms | 500ms |
| ScrollLine | 2000ms | 3000ms |
| Effects | 2500ms | 4000ms |

Heavy components deferred via `setTimeout` to avoid TBT impact. `React.lazy` only defers loading, not execution.

<br />

## Design Decisions

**Astro + React** — Static generation for content, React islands for interactivity. Zero JS by default.

**Custom GLSL** — GPU-side particle animation. No runtime overhead from shader generators.

**Hybrid Scroll** — Lenis on desktop, native scroll on mobile for best UX. Address bar stays visible.

**Web Workers** — Particle geometry computed off main thread. Eliminates 50ms blocking.

<br />

## Performance

### Core Web Vitals

| Metric | Target | Result |
|:-------|:-------|:-------|
| LCP | < 2.5s | ~1.8s |
| FID | < 100ms | < 50ms |
| CLS | < 0.1 | < 0.05 |

### Optimizations

1. Staggered 3D init (outside TBT window)
2. Web Worker geometry generation
3. Ref-based scroll (zero re-renders)
4. Throttled ScrollTrigger (30fps mobile)
5. Conditional post-processing
6. Self-hosted fonts

<br />

## Visual System

### Sapphire Veil Palette

| Token | Value | Usage |
|:------|:------|:------|
| Background | `#0D2440` | Deep Navy |
| Primary | `#7BA4D0` | Steel Blue |
| Accent | `#4B7CB0` | Mid-tone |
| Text | `#E7F0FA` | Ice Blue |

### Typography

| Role | Font |
|:-----|:-----|
| Display | Space Grotesk |
| Hero | Chakra Petch |
| Body | Inter |
| Code | JetBrains Mono |

<br />

## Tech Stack

| Layer | Technology |
|:------|:-----------|
| Framework | Astro 5 |
| UI | React 19 |
| 3D | Three.js 0.181, @react-three/fiber 9 |
| Animation | GSAP, Lenis (desktop), Framer Motion |
| State | Zustand 5 |
| Styling | Tailwind CSS 4 |
| Language | TypeScript 5.9 |

<br />

## Accessibility

- Reduced motion support (respects OS preference)
- WCAG AA color contrast
- Full keyboard navigation
- Visible focus indicators

<br />

<div align="center">
  <a href="https://sagimenahem.tech">
    <img src="https://img.shields.io/badge/sagimenahem.tech-0D2440?style=for-the-badge&logo=vercel&logoColor=white" alt="Visit Site" />
  </a>
  <br /><br />
  <b>Built by Sagi Menahem</b>
  <br /><br />
  <a href="https://github.com/sagi-menahem">
    <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" />
  </a>
  <a href="https://www.linkedin.com/in/sagi-menahem/">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
</div>
