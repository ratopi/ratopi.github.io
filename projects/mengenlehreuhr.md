---
title: Mengenlehreuhr
description: A Berlin Set Theory Clock implemented in HTML/SVG/JS
layout: page
---

A pure HTML/SVG/JS implementation of the famous **Berlin Set Theory Clock** (_Mengenlehreuhr_), located at the Europa-Center in Berlin since 1975. Designed by Dieter Binninger, it is the world's first public clock to display time using set theory principles.

### How to Read the Clock

The clock consists of **5 rows** that encode hours, minutes, and seconds:

| Row | Elements | Color | Value |
|-----|----------|-------|-------|
| **Top circle** | 1 lamp | Yellow | Blinks every even second |
| **Row 1** | 4 blocks | Red | Each = **5 hours** (max 20h) |
| **Row 2** | 4 blocks | Red | Each = **1 hour** (max 4h) |
| **Row 3** | 11 blocks | Yellow / Red | Each = **5 minutes** — every 3rd block (quarter hours) is red |
| **Row 4** | 4 blocks | Yellow | Each = **1 minute** (max 4 min) |

**Hours** = (lit lamps in Row 1 × 5) + (lit lamps in Row 2)
**Minutes** = (lit lamps in Row 3 × 5) + (lit lamps in Row 4)
**Seconds** = top circle ON → even second, OFF → odd second

### Features

- Pure **SVG** rendering — crisp at any resolution
- CSS **glow effects** for an authentic neon look
- **Digital time** display below the clock
- Updates every second
- **Progressive Web App (PWA)** — installable on mobile and desktop
- Works **offline** via Service Worker caching
- Zero dependencies — just a single self-contained HTML file

Try it out: [Live Demo](https://ratopi.github.io/mengenlehreuhr/)

Source code on [GitHub](https://github.com/ratopi/mengenlehreuhr).

