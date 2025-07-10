# Masterclass Review: Building a Maintainable Portfolio Site  
*for our enthusiastic beginner web-dev*  

---

## 1 High-Level Overview — What You Did & Where We’re Heading
You’ve shipped a **four-page** portfolio with navigation, custom fonts, Grid layouts, and cheeky copy. ✨  
That alone deserves a polite round of applause (and maybe a coffee-powered fist-bump).

**Things done well**

1. Semantic ingredients: `<nav>`, `<section>`, heading tags, `alt` attributes.  
2. Exploration of CSS Grid and custom properties (`:root` variables).

**Biggest growth themes**

* Consistency & scalability (variables, re-usable components, unit choices).  
* Semantic precision & accessibility (proper hierarchy, keyboard paths).  
* Responsive thinking vs. fixed pixels (rem units, clamp(), media queries).  

Keep those three themes in mind; they’ll echo through every section below.

---

## 2 A. The HTML Blueprint — Structure, Semantics, Accessibility
We start with the bones of the site. A beautiful paint job can’t fix a crooked house.

### A-1 Document Skeleton & `<head>` Hygiene
Your pages **duplicate** the entire `<head>` boilerplate. That’s harmless in a tiny repo, fatal in a big one.

```1:9:index.html
<link rel="stylesheet" href="style.css">
<!-- Bunny Fonts -->
<link rel="preconnect" href="https://fonts.bunny.net">
<link href="https://fonts.bunny.net/css?family=alegreya-sans:400,400i,800,800i|pixelify-sans:400,700" rel="stylesheet" />
```

**Problem**

* Every file repeats the same `<link>` tags → hard to maintain, slows the first render (the browser re-parses duplicates).

**Better**

1. **Single source of truth** – use a build tool / server-side include (`partials/head.html`).  
2. **Preload not repeat** – boost font loading:

```html
<!-- head.html -->
<link rel="preload" href="https://fonts.bunny.net/alegreya-sans.woff2" as="font" type="font/woff2" crossorigin>
<link rel="stylesheet" href="/css/main.css">
```

> ***Humor beat*** – Think of `<head>` like the backstage crew. You only need one calm stage manager, not four clones sprinting in circles yelling “Places, everybody!”
---

### A-2 Semantic Grouping & Landmarks
Each page replicates the same `<nav>` markup. That’s workable today; tomorrow it’s technical debt.

```22:34:about.html
<nav> … four identical <li> … </nav>
```

**Reflective question**  What happens when you add one new page? *Four* separate edits.  

**Solution path**

* Use a templating layer (Nunjucks, Handlebars, PHP includes, React components—pick your poison).  
* Extract a shared `nav.html` partial.

```html
<!-- nav.html -->
<nav>
    <ul class="nav-menu">
        <li><a href="/">Home</a></li>
        …
    </ul>
</nav>
```

---

### A-3 `<section>` vs `<article>` — Recap & Application
You already asked this in chat, so let’s solidify.

* **`<article>`** = self-contained. If I copy-paste it to another site, it still makes sense.  
* **`<section>`** = thematic group inside something larger.

**Your code**

```60:75:projects.html
<a class="project-card" …>
    <img …>
    <h2>Assignment 1</h2>
    <p>Short description.</p>
</a>
```

A project card is standalone content. Wrapping each `project-card` anchor in an `<article>` would be semantically perfect:

```html
<article class="project-card">
  <a href="https://github.com/DanIsaksson/assignment-1">
     …
  </a>
</article>
```

---

### A-4 Link & Image Paths (Back-slash Bug)
Windows uses backslashes; URLs **never** should.

```65:66:projects.html
<img src="images\freeplay-checkpoint-plugin.jpg">
```

On UNIX hosting this image = *404 party*.

```html
<img src="images/freeplay-checkpoint-plugin.jpg">
```

> ***Humor beat*** – Backslashes in URLs are like Swedish road signs written in Klingon. People get very lost, very fast.
---

### A-5 Lists, Anchors & Contact Details
Structure found in `cv.html`:

```23:29:cv.html
<ul class="contact-details">
  <li><a href="mailto:danisacsson@gmail.com">danisacsson@gmail.com</a></li>
```

Good! `<li>` outside `<a>` is the correct order (earlier you had the inverse in drafts). Keep verifying *semantics-first*.

---

### A-6 Accessibility Touches
**Checklist**

* Each page needs **exactly one `<h1>`** (some pages skip it).  
* The nav menu is visually fixed left; give keyboard users a *skip link*.  
* Ensure color contrast ≥ 4.5:1 (the lavender on white may not cut it).  

---

## 3 B. The CSS Paint & Polish — Variables, Layout, Units
Time to upgrade that paintbrush.

### B-1 Custom Properties Basics (and a small bug)
You smartly declared variables:

```1:14:style.css
:root {
  --hue-main: 220;
  --clr-body: hsl(var(--hue-main), 10%, 95%);
}
```

But then:

```16:20:style.css
body {
    background-color: --clr-body;   /* ❌  var() missing */
}
```

**Fix**

```css
body { background-color: var(--clr-body); }
```

Why `var()`? Think of it as a **bartender**; the CSS property says “gimme *var--clr-body*, the usual.”

---

### B-2 Typography Scale & `clamp()`
You nailed `--nav-font-size: clamp(16px, 3vw, 22px)` – responsive without media queries.

Now tame the wild pixel beasts:

```37:41:style.css
font-size: 100px;   /* inside .general-container h2 */
```

**Refactor path**

```css
:root {
  --fs-hero: clamp(2.5rem, 6vw + 1rem, 6rem);
}
.general-container h2 { font-size: var(--fs-hero); }
```

---

### B-3 Consistent Units
Example of mixed pixels & percentages:

```20:27:style.css
.nav-menu {
  width: 8%;        /* percent of viewport width */
  height: 30%;      /* percent of viewport height? no, parent height */
}
```

Percent **of what**? Keep mental models simple:

* Use **rem** for text/inset spacing.  
* Use **%** or **fr** for grid tracks.  
* Use **clamp()** for responsive extremes.

**Exercise** Convert that `height:30%` into a max-height responsive rule:

```css
.nav-menu {
  height: clamp(200px, 30vh, 400px);
}
```

---

### B-4 Layout with CSS Grid — Centering & Duplication
You fixed centering with `margin-left:auto; margin-right:auto;`.

**Why the duplicate `width`?**

```73:83:style.css
.general-container {
  width: 50%;
  …
  width: 90%;   /* second declaration overrides first */
}
```

Remove the first. DRY code prevents 3 a.m. bugs.

---

### B-5 DRY & Grouped Selectors
`.project-card`, `.profile-photo`, `.profile-photo-cv` all repeat identical border radii & colors. Extract a utility:

```css
.rounded-pixel {
  border-radius: 15px;
  border: 2px solid hsl(var(--hue-main),100%,10%);
}
.project-card,
.profile-photo img,
.profile-photo-cv img {
    /* apply the utility */
    border-radius: var(--rounded-radius,15px);
    border: 2px solid hsl(var(--hue-main),100%,10%);
}
```

---

### B-6 Visual Polish & Micro-Interactions
Your `contact-details li:hover` swap color is a strong start.

Upgrade project cards:

```css
.project-card {
  transition: transform .25s ease, box-shadow .25s ease;
}
.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 6px 15px rgba(0,0,0,.15);
}
```

> ***Dark-satire aside*** – Lull users into clicking: “Come, dear visitor, hover over my card… nothing bad will happen…” (ominous thunder).
---

## 4 C. The Grand Synthesis — Making HTML & CSS Dance Together
### 1 Project Architecture
Currently each HTML page imports `style.css`. That’s fine, but:

* Consider a **component folder** approach:  
  ```
  /components
      nav.css & .html
      card.css
  main.css (imports them)
  ```
* Future frameworks (React/Vue/Svelte) encourage single-source components — you’re already half-way there.

### 2 Scalability Checklist
* **Global reset** or **normalize.css** to zero out inconsistent defaults.  
* **Naming convention** – BEM (`project-card__title`) or utility (Tailwind).  

### 3 Responsive Workflow
Mobile-first means:

```css
.project-grid {
    grid-template-columns: repeat(auto-fill,minmax(150px,1fr));
}
@media (min-width:768px) {
    .project-grid { grid-template-columns: repeat(auto-fill,minmax(200px,1fr)); }
}
```

### 4 Maintainability — Kill Inline Styles
```66:69:index.html
<span style="color:#4CAF50;">.NET</span>
```

Move to CSS:

```css
.skill-dotnet { color: var(--clr-dotnet); }
```

And define `--clr-dotnet` inside `:root`.

### 5 Performance Sprinkles
You already use `preconnect`; add:

```html
<link rel="preload" href="/images/hero.jpg" as="image">
```

and compress images to WebP for a 40-70 % savings.

---

## 5 D. Final Review & Next Steps
### Key Takeaways
* Semantics first (`<article>` vs `<section>`, one `<h1>`).  
* Variable-driven design (`var()`, `clamp()`).  
* DRY components (shared nav, utility classes).  
* Accessibility & responsive concerns early, not bolted on.

### Action Plan
| Timeframe | Task |
|-----------|------|
| **Today** | Fix `var(--clr-body)` bug, remove duplicate widths, correct image paths |
| **Tomorrow** | Extract nav into partial, create `:root` typography scale |
| **This week** | Convert fixed pixel dimensions to `rem`/`clamp`, add hover polish, audit contrast |
| **Stretch** | Implement the JavaScript splash screen, run Lighthouse & axe accessibility scans |

### Resources
* MDN: CSS Grid guide.  
* Kevin Powell YouTube on `clamp()`.  
* WebAIM Contrast Checker.

### Quiz Ideas
1. Rewrite `.project-card` with variables in `< 8` lines.  
2. Identify three spots where `<article>` beats `<section>`.

> ***Humor outro*** – Remember that *legendary 200-year-old developer* quote? The secret to such longevity is simple: keep your CSS DRY, your semantics sharp, and your coffee supply infinite. Refactor early, refactor often—because debugging at 3 a.m. without variables is the real horror story.  
Happy coding!
