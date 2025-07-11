---
description: "A pedagogical tutor that provides Socratic or Structured help for beginner programmers in C#, .NET, and web development."
alwaysApply: "false"
mustuseReferenceMaterial: "context7.json"
---

# Improvement for Responsive Mobile Design
## Responsive Mobile Design Plan (Media Queries)

**Total Estimated Time:** ~4–6 hours (can be split across two work sessions)

| Phase | Task | Est. Time |
|-------|------|-----------|
| 1 | Audit current layout on real devices & DevTools, list major break-points that break (e.g. ≤480 px, 481–768 px) | 45 min |
| 2 | Decide mobile-first breakpoints ¹ and create a `styles/mobile.css` import or section in `style.css` | 30 min |
| 3 | Refactor base styles so they work on narrow viewports (single-column grid, full-width images, font-scaling already in vars) | 1 h |
| 4 | Add `@media (min-width:48em)` (≈768 px) rules to progressively enhance sidebar grid (`grid-template-columns:12rem 1fr`), nav layout, and project grid (`repeat(auto-fill,minmax(200px,1fr))`) | 1 h |
| 5 | Add `@media (min-width:64em)` (≈1024 px) tweaks for large screens (max-width, bigger gaps) | 30 min |
| 6 | Cross-browser/device testing & Lighthouse mobile audit; iterate | 1 h |
| 7 | Commit & push; verify on GitHub Pages/Netlify preview | 15 min |

> ¹ Reference: MDN “Using Media Queries” & CSS-WG Media Queries Level 4 spec.

### Key Best-Practice Notes
* **Mobile-First:** Define mobile styles as default, then layer `min-width` queries.
* **Use `em`/`rem` Breakpoints:** Keeps breakpoints tied to font-size, improving accessibility.
* **Avoid Fixed Heights/Widths:** Replace with `%`, `auto`, or `minmax()`.
* **Test Real Devices:** Emulators can miss touch/viewport quirks.
* **Performance:** Combine media-query blocks to reduce duplicate code.

### Suggested Starting Snippet
```css
/* Base (mobile-first) */
.page-layout { grid-template-columns: 1fr; }
.sidebar { position:static; width:100%; margin:0; }

/* ≥48em (~768 px) – tablets & up */
@media (min-width:48em) {
  .page-layout { grid-template-columns: 12rem 1fr; }
  .sidebar { position:sticky; width:auto; margin:var(--space-4); }
}
```

---
_Added by BeginnerCodingTutor — see context7.json for study resources on responsive design._