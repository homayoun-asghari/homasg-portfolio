# homasg — my first personal website (2019, abandoned)

An abandoned personal portfolio site, hand-written in HTML and CSS over six days in **September 2019**. Three separate layout attempts, none finished, no site ever deployed.

It ships here exactly as it was found. Nothing has been cleaned up, renamed, or fixed. The broken parts are the reason it is published.

---

## Provenance

> This repository was reconstructed in 2026 from a filesystem archive. The code was never under version control at the time.
>
> **Commit dates are the real modification times of the original files**, recovered with `stat`, accurate to the second. The work happened between **2019-09-19 16:44** and **2019-09-24 09:01** local time (UTC+03:30). One commits are dated 2026: the README, the rendered previews, and any corrections. Each is labelled as such in its commit message.

## What is here

```
index.html      language picker: ENGLISH / فارسی
pages/          layout attempt 3 — plain divs, absolute pixels   (Sep 24)
pages2/         layout attempt 2 — Bootstrap grid                (Sep 22)
sakhla/         layout attempt 1½ — a fourth standalone page     (Sep 24)
style/          CSS for pages/ and, wrongly, for pages2/
style2/         CSS for pages2/ that pages2/ never loads
images/         10 images, 9 of them unused
```

`sakhla` is a mangled transliteration of *sākhtār* / سقاله — the folder is scaffolding, a single self-contained page with no links out.

There is **no build step, no framework, and not one line of JavaScript I wrote.** Every `<script>` tag in the project points at a CDN.

## What is wrong with it

I am publishing this as a dated artifact — the "before" picture — not as a portfolio piece. Everything below was verified against the files in this repository.

**It has no content.**
- `pages/home.html` and `pages2/home.html` contain one paragraph of **Lorem Ipsum**, pasted twice into itself so the tail reads `...remainingLorem Ipsum is simply...` and ends `remaining essential. essential.`
- The other six English pages contain **no body content at all**. Header, nav, closing script tags. Nothing between.
- The four Persian pages — `خانه.html`, `درباره من.html`, `نمونه کارها.html`, `تماس یا من.html` — are **0 bytes**, in both `pages/` and `pages2/`. Eight empty files. They are kept at 0 bytes in this repository because they are the evidence. The last of those filenames is itself a typo: تماس **یا** من instead of تماس **با** من.
- The homepage language switcher offers two choices. `ENGLISH` reaches a real page. `فارسی` links to `pages/خانه.html`, which is one of the empty files. Half the site's front door opens onto nothing.

**The layout is pixel-pushed against one monitor.**
```css
.topbar     { position: absolute; width: 1366px; padding: 20px; position: fixed; }
.explanation{ margin-top: 225px; margin-left: 635px; width: 500px; height: 400px; }
```
`1366px` is the width of the laptop screen it was written on. `position` is declared twice in the same rule. `.background` is positioned by hard-coded `margin-left` — `273px`, `546px`, `820px`, `1093px` on the four pages — arbitrary numbers that mean nothing on any other display. `style2/home.css` hard-codes `height: 1080px`, so the two attempts are tuned to two *different* screens.

**Bootstrap is loaded and then fought.**
`pages2/` uses `.container-fluid > .row > .col-2 / .col-10`, then immediately overrides the grid with `position: fixed`, `float: right`, `margin-top: -55px`, `margin-top: -60px`, and fixed pixel heights. The grid does no work; it is scaffolding holding up hand-placed boxes.

**The header is split mid-word to fake kerning.**
```html
<div class="col-2">  <h1> HOMAY</h1>       <h3> WEB DEVE</h3>  </div>
<div class="col-10"> <h1> OON ASGHARI</h1> <h3> LOPER</h3>     </div>
```
Two column halves, one dark and one light, with the name cut across the boundary so it reads as a single word with a colour change through it. It renders correctly at exactly one viewport width. `pages2/about me.html` cuts the same name at a *different* letter — `HOMAYOON ASGH` / `ARI` across `col-4` / `col-8` — so the two pages do not even break the word in the same place.

**Attempt 2 is wired to the wrong stylesheet.**
Every page in `pages2/` links `../style/home.css`, `../style/about me.css`, and so on. But `style/` styles `.topbar`, `.namelogo` and `.background` — the markup of `pages/`. The rules that actually position the split header, `.col-2 { height: 1080px }` and `.col-10 { background-color: black }`, live in `style2/`, which **no page in the repository ever loads**. The kerning trick above cannot have rendered as intended. The entire `style2/` directory is dead on arrival.

**Three vendored libraries, all unused.**
`style/bootstrap.min.css` and `style2/bootstrap.min.css` are two byte-identical 156 KB copies that no page references — every page pulls Bootstrap 4.3.1 from `stackpath.bootstrapcdn.com` instead. Same for `js/`: local copies of jQuery, Popper and Bootstrap that nothing loads.

**Smaller things.**
- `class="btn btn-defult"` — a misspelling of `btn-default`. It is styled anyway, by a matching `.btn.btn-defult` rule in `style/style.css`. And Bootstrap 4 removed `.btn-default` entirely, so the correctly-spelled class would not have worked either. The bug and its accidental workaround both shipped.
- **Unclosed `<div>`s.** `pages/about me.html`, `pages/contact me.html` and `pages/portfolio.html` each open four `<div>` elements and close three. `<div class="topbar">` is never closed; the browser silently swallows the rest of the document into it.
- **Filenames contain spaces** — `about me.html`, `contact me.css` — and are referenced as raw unescaped spaces in `href` attributes.
- **9 of the 10 images are unused.** Only `main.jpg` is referenced, by `style/style.css`. The seven social-media icons, `main2.jpg` and `homeback.png` were downloaded for a footer that was never built.
- No `alt` text, because there are no `<img>` tags — every image that renders does so through a CSS `background-image`.

## The one thing that is not wrong

`style/style.css` — the landing page only — carries five real media-query breakpoints at Bootstrap's 575.98 / 767.98 / 991.98 / 1199.98 boundaries, adjusting background size, heading margin and button geometry at each. The front door is responsive. Nothing behind it is. Whoever wrote that stylesheet knew what a breakpoint was and then did not use one again.

## Timeline

| When | What |
|---|---|
| Sep 19 16:44 | Eight empty Persian page files created |
| Sep 19 17:02–18:07 | Social icons collected, landing page written |
| Sep 20 19:03 | `style.css` with the responsive breakpoints |
| Sep 22 19:08–19:46 | Attempt 2: Bootstrap grid, split header, `style2/` |
| Sep 24 08:27 | *(design mockup made in Adobe XD — see `design-mockups-xd`)* |
| Sep 24 08:34 | `sakhla/` — a fourth, standalone page |
| Sep 24 08:43–09:01 | Attempt 3: back to plain divs and absolute pixels |
| — | Nothing after. |

Five days, three layouts, zero content, and then it stopped.

## Attribution

The HTML and CSS in this repository are mine. The following were in the original directory and are **excluded** from this repository because they are third-party:

- `js/` — Bootstrap 4 (`bootstrap.min.js`), jQuery 3.3.1, Popper.js. Never referenced by any page.
- `style/bootstrap.min.css` and `style2/bootstrap.min.css` — Bootstrap 4 CSS, 156 KB each, byte-identical, never referenced by any page.
- `fonts/` — the Persian webfonts **B Badr, B Koodak, B Lotus** and **B Titr** in `.eot`, `.ttf` and `.woff`. These are commercial Iranian typefaces I did not license, and no stylesheet in the project declares an `@font-face` for any of them.

The images in `images/` are unattributed downloads from 2019 and are not my work either; they are kept because their absence would misrepresent the state of the directory.

## Running it

Open `index.html` in a browser. Click `ENGLISH`. Set your window to exactly 1366 pixels wide first, or the header will not line up. Click `فارسی` and you will get a blank page, which is the honest result.
