# mikatomorrow.github.io — Claude context

## Site flow
index.html → boot.html → plaza.html → room pages

## Room pages & color themes
| Page | Accent (border) | Title color |
|------|----------------|-------------|
| work.html | #7a9900 | #aabb44 |
| music.html | #2266aa | #4488cc |
| papers.html | #996622 | #cc9944 |
| about.html | #994433 | #cc6655 |
| food.html | #cc7722 | #ee9933 |
| gaming.html | #22aa77 | #33cc99 |
| random.html | #cc3366 | #ee4488 |
| mystery.html | #663399 | #9966cc |
| weather.html | #1188cc | #33aaee |
| notes.html | plain white, no theme |

## Standard dark-room page structure
- DOCTYPE: XHTML 1.0 Transitional
- Background: `background-color: #7070aa; background-image: url('bg.png'); background-repeat: repeat;` (except gaming=#000000, random=star.gif tiled, mystery/weather=black)
- Custom cursor: `html, body, * { cursor: none !important }` + `html, body { min-height: 100vh }` + fixed `<div id="fake-cursor">` tracking mousemove
- Body needs `position: relative` for absolute-positioned gifs
- Gifs: `position: absolute` on body, placed before `<div id="outer">` in HTML — NOT fixed
- Content panel: `<div id="outer">` (760px centered) → `<div id="header">` → `<div id="content">`
- Header has breadcrumb, h1, .sub tagline; border-left color matches room accent
- Clippy: fixed bottom-right canvas renderer, 124×93px frames from clippy.png, magenta (R>200 G<60 B>200) removed

## CRITICAL RULES
- **NEVER modify Clippy seq[] arrays or canvas code** unless explicitly asked. User fine-tunes these manually.
- weather.html has NO custom cursor — cross-origin iframe swallows mousemove events
- mystery.html is a full-screen flying toasters screensaver — no content panel, no Clippy
- notes.html is plain white (Times New Roman, black on white) — no cursor, no Clippy, no gifs

## notes.html structure
- `<details class="subject">` accordion blocks, one per subject
- `<summary>` shows title + one-line teaser
- `.question` class (yellow left border) for questions/check-understandings to follow up on
- `.note-callout` class (grey left border) for personal observations
- MathJax not yet added — LaTeX formulas are written but not rendered

## plaza.html portal conventions
- Each room is `<a href="X.html" class="portal pt-X">` with image slot + info + arrow
- mystery and weather portals are centered/no-image-slot style (see CSS overrides)
- Portal order: work, music, papers, about, food, gaming, random, weather, notes (class notes), mystery

## Gif placement pattern (all dark rooms)
CSS on body: `position: relative`
CSS on gif: `position: absolute; top: Xpx; left/right: 10px; pointer-events: none; z-index: 60; image-rendering: pixelated; image-rendering: crisp-edges;`
HTML: `<img id="gif-name" src="name.gif" alt="" />` placed before `<div id="outer">`

## Flying toasters (mystery.html only)
- Sprite sheet background-image approach (not img tags)
- `flap` keyframe steps background-position 0 → -256px (4-frame sprite at 64px each)
- `fly` keyframe translates across screen
- Toast uses fly only (no flap)

## Known gif issues
- Some gifs have white backgrounds — check before adding. Confirmed clean: headphone.gif, mic2-4.gif, bear.gif, headphone_spin.gif, cutepika.gif, pikasleep.gif, tomato_plop.gif, food1.gif, xwings1.gif, astronaut_flip.gif, train.gif
- Removed due to white bg: gangster.gif, horse1.gif, mic1.gif

## Work/projects page (planned redesign)
- work.html: dark-themed index with featured cards + compact list, each entry links to own page
- Individual project pages: plain white style (like notes.html)
- See conversation for structure confirmation before building
