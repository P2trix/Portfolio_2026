# Responsive Design Benchmark — Portfolio 2026

## Breakpoint Strategy

| Breakpoint | Target | Container Padding |
|------------|--------|-------------------|
| >1024px | Desktop | `0 80px` |
| 769–1024px | Small desktop / Tablet landscape | `0 40px` |
| 481–768px | Tablet portrait | `0 24px` |
| ≤480px | Mobile | `0 16px` |
| ≤360px | Small mobile | `0 12px` |

Max container width: `1440px` (content-box — total may exceed viewport, clipped by `overflow-x: hidden`).

---

## Component Behaviour Matrix

### Navigation (`.cs-nav`)
| Breakpoint | Behaviour |
|------------|-----------|
| >768px | Horizontal inline links |
| ≤768px | Hamburger toggle → fullscreen overlay. Toggle fixed-position when open |
| ≤480px | Same as 768px; nav links font-size 26px |

Touch target: toggle 40×40px (≥44×44 at ≤768px — verify).

### Hero (`.cs-hero`)
| Breakpoint | Image | Title | Padding |
|------------|-------|-------|---------|
| >1024px | Fixed 700px height | 60px/68px | 64px |
| 769–1024px | `min-height: 500px` | 40px/48px | 40px |
| 481–768px | `min-height: 320px` | 32px/40px | 24px |
| ≤480px | `min-height: auto`, border-radius 12px | 26px/34px | 16px |
| ≤360px | `min-height: auto`, border-radius 10px | 22px/28px | 12px |

### Content Sections (`.cs-section`)
| Breakpoint | Layout | Number size |
|------------|--------|-------------|
| >1024px | Two-column (left 500px fixed, right max 720px) | 128px |
| 769–1024px | Stacked column | 80px |
| 481–768px | Stacked column | 64px |
| ≤480px | Stacked column | 40px |

Section padding: 64px desktop → 32px at 768px → 20px at 480px. Gap follows same scale.

### Details Card (`.cs-details`)
| Breakpoint | Layout | Padding |
|------------|--------|---------|
| >1024px | Horizontal flex, gap 47px | 28px 22px |
| 769–1024px | Stacked column, wrap | same |
| ≤480px | Column, gap 16px | 20px 16px |

### Process Cards (`.cs-process`)
| Breakpoint | Grid | Card height |
|------------|------|-------------|
| >1024px | 4 per row (`flex: 1`) | 400px |
| 769–1024px | 2 per row (`flex: 1 1 280px`) | 400px |
| 481–768px | 2 per row (`flex: 1 1 calc(50% - 8px)`) | auto (min 200px) |
| ≤480px | Stacked column (`width: 100%`) | auto (min 160px) |
| ≤360px | Same as 480px | auto |

**Note**: `box-sizing: border-box` on cards prevents overflow with `width: 100%` + padding.

### Image Rows
| Breakpoint | Behaviour |
|------------|-----------|
| >1024px | Flex row (`cs-image-row`) or grid (`cs-image-row-2`: 2-col, `cs-image-row-3`: 3-col) |
| 769–1024px | Grid collapses to single column |
| ≤480px | `overflow-x: auto` with scroll-snap, `touch-action: pan-x pan-y` |

### Floating ToC Widget
| Breakpoint | Position | Panel |
|------------|----------|-------|
| >768px | `right: 24px; top: 50%; translateY(-50%)` | Opens rightward, `translateY(-50%)` |
| ≤768px | `right: 20px; bottom: 68px; transform: none` | Opens upward from toggle, `transform-origin: bottom right` |

Toggle: 40×40px desktop → 44×44px mobile.

### Back-to-top
| Breakpoint | Position | Size |
|------------|----------|------|
| >768px | `bottom: 32px; right: 32px` | 44×44 |
| ≤768px | `bottom: 16px; right: 20px` | 44×44 |

**Spacing**: On mobile, ToC is at `bottom: 68px` and back-to-top at `bottom: 16px` — 52px gap, safe.

---

## Baseline Standards

| Rule | Value | Source |
|------|-------|--------|
| Touch targets | ≥44×44px | WCAG 2.5.8 / Apple HIG |
| Body text (mobile) | ≥16px | iOS Safari auto-zoom prevention |
| Line length | 45–75 chars | Typographic best practice |
| Spacing unit | 8px base / 4px grid | Design system token |
| Border radius | 28px (hero/cards), 21px (sm), 1000px (tags) | Design system |
| Container max | 1440px | Layout width |

---

## Mobile Testing Checklist

### Layout
- [ ] No horizontal scroll at any viewport ≥320px
- [ ] Container padding correct at each breakpoint
- [ ] Content does not overflow cards/sections
- [ ] Footer spacing adequate

### Navigation
- [ ] Hamburger visible at ≤768px
- [ ] Fullscreen overlay covers entire viewport
- [ ] Close button (X) reachable (top-right, fixed)
- [ ] Nav links legible and tappable (≥44px height)
- [ ] Click outside closes menu

### Hero
- [ ] Image background fully visible, no cropping
- [ ] Title/subtitle readable against background
- [ ] Tags wrap correctly
- [ ] CTA buttons tappable

### Process Cards
- [ ] 2 per row on tablet, stacked on mobile
- [ ] Cards have enough vertical space for content
- [ ] Hover effects don't break touch interaction

### ToC Widget
- [ ] Toggle visible and tappable
- [ ] Panel opens upward on mobile (doesn't go off-screen)
- [ ] Active section highlighted
- [ ] Smooth scroll works on tap

### Back-to-top
- [ ] Appears after scrolling
- [ ] Tappable (not overlapping ToC)
- [ ] `.at-bottom` state works when at end of page

### Images
- [ ] No broken images (case-sensitive paths: `Figma/` not `figma/`)
- [ ] WebP format loads correctly
- [ ] Images don't overflow container
- [ ] Scrollable rows work with touch

### Typography
- [ ] Font sizes legible without zoom
- [ ] Line heights don't cause clipping
- [ ] Contrast meets WCAG AA (4.5:1 body, 3:1 large text)

---

## Known Issues / Future Work

- [x] ~~360px breakpoint not implemented~~ — added 23.06.2026
- [x] ~~Hero `min-height: 500px` at 768px~~ — reduced to 320px
- [x] ~~Process cards fixed 280px height~~ — changed to auto/min-height
- [x] ~~Duplicate `.back-to-top` in home.css~~ — removed, only in case-study.css
- [x] ~~Touch targets (nav links)~~ — added `padding: 10px 0` at ≤768px
- [ ] `<360px` devices may still have edge issues
- [ ] No landscape orientation specific styles
- [ ] No `prefers-reduced-motion` queries
- [ ] No print stylesheet
- [ ] Nav hamburger `right` calculation on open uses `max(24px, ...)` — simplify for mobile
