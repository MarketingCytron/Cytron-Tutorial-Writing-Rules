---
name: "cytron-tutorial-rules"
description: "Apply Cytron's Tutorial Writing Rules when drafting, revamping or reviewing any tutorial for my.cytron.io/tutorial: credentials, structure, formatting, product links, SEO, safety, pre-publish checklist."
---

# Cytron Tutorial Writing Rules

Single source of truth: the "Cytron Tutorial Writing Rules" doc (https://claude.ai/code/artifact/93882066-b198-4390-963a-2f6b205969e2).
Writers (Cytron staff and interns) use the live **Cytron Tutorial Guide** page, https://marketingcytron.github.io/Cytron-Tutorial-Writing-Rules/
(published from the claude.ai artifact "Cytron Tutorial Guide"), or the doc itself. Point writers to the guide page, never to
the old WI or template. If this skill and the doc disagree, the doc wins; tell the user about the mismatch.
The doc also holds the WebAdmin setup steps and the editor how-tos (links, images, code, YouTube, Telegram banner), with
short videos for uploading a picture through Browse Server, inserting the Telegram banner, and what a pasted outside picture does.

MUST = compulsory for every tutorial; a miss sends the draft back. SHOULD = follow where it applies; skip if it doesn't fit.

Purpose: a tutorial page shows how a product works before a customer orders, and is where customers and customer support
staff come back to when something goes wrong. Write every step for a complete beginner who knows nothing about digital making.

Boards: tutorials cover any main board (Maker ESP32, Raspberry Pi, micro:bit, Arduino-compatible boards and more). Rules
that name Maker ESP32 use it only as an example; apply them to the tutorial's own main board, tool (Arduino IDE, Thonny,
MakeCode, etc.), Getting Started guide and Telegram community.

## Modes

- **Draft / revamp**: produce body HTML for the WebAdmin Description field (Source view), starting at `<h2>`, never repeating
  the title. Placeholders: `<!-- IMAGE: ... -->` (system diagram, hardware assembly photo, a screen capture per setup step,
  demo), `<!-- GIST EMBED -->`, `<!-- TELEGRAM BANNER -->`; mark optional sections with `<!-- optional -->`. Use the tutorial's
  own main board, tool and Getting Started guide, never a hard-coded Maker ESP32. Every credential is a placeholder (§0).
  Body paragraphs carry `style="text-align: justify;"`, no font styles, every `<a>` has `target="_blank"`,
  and the banner is a centred `<p>` with the linked `<img>` at `width: 900px` (§1b). After the HTML, output every WebAdmin
  field (§5) as a table, with character counts for Post Name, Pitch and Meta Tag Title.
- **Review**: check §0 first, then the checklist (§8). Report failures as a table (Rule · MUST/SHOULD · What's wrong · Fix),
  credentials first, then other MUST items. Quote the exact offending text or URL, **except a credential**: name its type,
  where it sits (page body, Gist file and line, screenshot) and show it masked (first 3 characters + ••••). Don't rewrite the
  whole tutorial unless asked. Don't be strict about wording or optional sections: flag real misses, not close equivalents.

## 0. Credentials and secrets: zero tolerance (all MUST)

Never publish a real password, token or key anywhere on a tutorial page. The Q4 2026 quick scan found real Blynk tokens,
Telegram bot tokens and Wi-Fi passwords in 11 published tutorials (Gists, code in the page body, a public GitHub repo).
A real credential is the most serious finding in any review.

| Type | Examples | Placeholder |
|---|---|---|
| Wi-Fi | SSID and password | `YOUR_WIFI_SSID`, `YOUR_WIFI_PASSWORD` |
| IoT platform | Blynk auth token, template ID and name; ThingSpeak write key; Adafruit IO key | `YOUR_BLYNK_AUTH_TOKEN`, `YOUR_TEMPLATE_ID`, `YOUR_API_KEY` |
| Bots | Telegram bot token and chat ID | `YOUR_TELEGRAM_BOT_TOKEN`, `YOUR_CHAT_ID` |
| Cloud and AI services | Firebase API key and database secret; OpenAI, Gemini, Google API keys | `YOUR_API_KEY` |
| Logins | MQTT user and password, email/SMTP password, any account password | `YOUR_MQTT_USER`, `YOUR_MQTT_PASSWORD` |
| Device keys | LoRaWAN AppKey, device certificates, private keys | `YOUR_APP_KEY` |
| Personal details | Phone number, personal email, home address | Leave out, or blur in images |

Where they leak: Gists (every old revision stays public), code in the page body, screenshots (Serial Monitor, Blynk Console,
BotFather chat, browser address bar: a Telegram API URL contains the bot token), videos, ZIP/Drive downloads, GitHub repos.

Rules:
1. Test with real values locally, then swap in placeholders before the code goes anywhere. No real value in WebAdmin, a Gist or a repo, not even in a draft.
2. A comment beside each placeholder (`// Replace with your own Wi-Fi name`); the reader replaces it in a Testing & Validation step.
3. Use a bot, Blynk device or account made only for the tutorial, never a personal or Cytron office one.
4. Crop or blur every credential before saving a screenshot or recording a video.
5. Before submitting, search body, Gists and downloads for password, ssid, token, auth, key, secret, api, bot; check any long random string.
6. Revoke or regenerate the tokens used for screenshots and video when done.
7. A real value ever saved in a Gist or repo: deleting it is not enough (revision history). Revoke it and create a new Gist.

If one is already published: (1) revoke/regenerate it the same day (BotFather /revoke, Blynk Console, provider console, change
the Wi-Fi password); (2) replace it with a placeholder everywhere (WebAdmin body, a new Gist, repo, Drive, screenshots, video);
(3) tell the supervisor the same day, naming the page and location but never pasting the value. Removing without revoking does
not fix the leak.

Patterns to look for in reviews: Telegram bot token `\d{8,10}:[A-Za-z0-9_-]{35}`; Google/Firebase key `AIza[0-9A-Za-z_-]{35}`;
OpenAI-style `sk-…`; GitHub `ghp_…` / `github_pat_…`; AWS `AKIA…`; a quoted 32-character string assigned to an auth/token
variable (Blynk); any non-placeholder string assigned to ssid, pass, password, token, auth, key, secret, chat_id, user;
literal strings passed to `WiFi.begin()` or `.connect()`. Check rendered Gists and inline code. Never repeat a found value.

## 1. Structure (this order; close equivalent names and extra H2s are fine)

| # | Heading | Level | Required | Must contain |
|---|---|---|---|---|
| 1 | Introduction | H2 | MUST | 2–4 sentences: what the reader builds and why it matters (Education/Industry). Open with the reader's problem. Right after the paragraph: the video tutorial if there is one, or an optional hero image. |
| 2 | Disclaimer / Safety Notes | H2 | Optional (§6) | Recommended when a safety trigger applies: electrical, battery or heat cautions, warranty notes, classroom supervision. |
| 3 | Prerequisites | H2 | MUST | Link Getting Started guides/basics; name software, accounts, firmware or SDKs to install. |
| 4 | Objectives (or Overview) | H2 | MUST | What the reader will learn or build. No length limit. |
| 5 | List of Components (or Hardware Components / Hardware Required) | H2 | MUST | Numbered list, product name linked, new window; quantity only when more than one unit (e.g. x2); name and link only, no product pictures (§3). |
| 6 | System Diagram & Wiring | H2 | MUST | Labelled block/circuit diagram (Canva, Fritzing) at native aspect ratio + pin-to-pin wiring table ([Main board] · [Module] · Function). **Note:** for mounting tips or other ways to connect. A hardware assembly photo with every connection visible where it helps. |
| 7 | Software Setup | H2 | MUST | IDE/toolchain version, library names + install steps, board and port selection; link the official download/docs page of every software; screenshots encouraged. If Prerequisites already links a board setup guide, don't repeat the board setup unless the tutorial needs a new setup. |
| 7a | Install [Library name] Library | H3 | When a library is installed | Numbered install steps in the board's own tool, with a screen capture per step. Arduino IDE: Library Manager incl. the "Install All" dependency prompt; others: Thonny's package manager, MakeCode Extensions, pip/apt on Raspberry Pi OS. |
| 8 | Sample Code | H2 | MUST | A line such as "Upload the following code to your [board]:" + public GitHub Gist embed. |
| 8a | Key Code Explanation | H3 | MUST | One bullet per key line/block: `code`: what it does. |
| 9 | Testing & Validation | H2 | MUST | Numbered steps to run and verify; inline troubleshooting note where a step often fails. |
| 9a | Expected Results | H3 | MUST | Expected outputs: Serial Monitor or terminal lines, LEDs, sounds, browser view. |
| 10 | Demo / Results | H2 | MUST | Photos or a YouTube embed of the working project; screen captures of dashboards, the Serial Monitor or the terminal. |
| 11 | Troubleshooting & Extra Tips | H2 | Optional | If included: H3s, each a symptom as the reader sees it, bullet fixes (power, baud rate, library conflicts, sensor orientation, calibration). |
| 12 | Conclusion | H2 | MUST | 2–3 sentences: what the reader built and learned, the final result, what to try next (link a related tutorial). |
| 13 | Downloads & Assets | H2 | Optional | ZIP of diagrams/configs, repos, datasets, example flows, STL/3D files. |
| 14 | Telegram community banner | no heading | MUST | One banner at the end, centred, 900 px wide, image linked (new window) to the matching community. |

The Hardware Components block and Related Posts below the body come from the Links tab, not the body. No empty headings.
Older pages use "List of Components / BOM"; new tutorials use "List of Components".

Telegram banners: download the named file from the Community Banner folder
(https://drive.google.com/drive/folders/186p2woTflBfHwUBpQwDWdBDOdYqAaUaE); all channels: https://my.cytron.io/cytrons-telegram-channel.
Pick by the main board, not the sensor. Maker Gathering only when no product community fits. In drafts, name the banner file
and link in the `<!-- TELEGRAM BANNER: … -->` placeholder.

| Use for | Community | Link | Banner file |
|---|---|---|---|
| Maker ESP32, ESP32 projects | ESP Makers Malaysia (Official) | https://t.me/ESPmakersMY | Maker ESP32 Telegram Banner.png |
| Maker UNO, Maker Drive, other Cytron Maker boards | Cytron Maker Board MY | http://qr.codes/0P3Lai (same as Arduino) | Cytron Maker Board Telegram.png |
| Arduino boards | Arduino | http://qr.codes/0P3Lai | Arduino Telegram.png |
| Raspberry Pi | Raspberry Pi | http://qr.link/aX8uQ7 | Raspberry Pi Telegram.png |
| Raspberry Pi in industry/professional use | Raspberry Pi Professional | http://qr.link/BXAybc | Raspberry Pi for Professional-footer.png |
| NVIDIA Jetson | NVIDIA Jetson | http://qr.codes/b2TBX5 | NVIDIA Jetson Telegram.png |
| RDK boards (RDK X5 etc.) | RDK Series Community | http://qr.codes/0H84mK | RDK-telegram-footer.png |
| micro:bit | micro:bit | https://qr.link/owmYeg | microbit Telegram.png |
| EDU:BIT | EDU:BIT Support Group | https://t.me/edubit_trainers | none yet |
| ZOOM:BIT | ZOOM:BIT Support Group | https://t.me/zoombit_support | Zoombit Support.png |
| SUMO:BIT | SUMO:BIT Support Group | https://t.me/sumobit_support | Sumobit Banner.png |
| SUMO Drone, school robotics, STEM | STEM Robotik | http://qr.codes/YO63x0 | SUMO_Drone_STEM Robotik.png |
| CircuitPython projects | CircuitPython Malaysia | https://t.me/CircuitPythonMY | none yet |
| 3D printing | 3D Printing | http://qr.io/r/pgVcQB | 3D Printing Telegram.png |
| Robomania competition tutorials | Robomania 2025 | https://t.me/robomania_my | Robomania_Telegram_Banner.png |
| Only tutorials related to RAC (a Cytron event) | RAC Helpdesk | https://t.me/RAC_helpdesk | none yet |
| Cytron Learning Hub content | Cytron Learning Hub | http://qr.link/G7fcUA | Cytron Learning Hub.png |
| General maker projects, none of the above | Maker Gathering | http://qr.io/r/n7EwBk | none yet |

"none yet" = no banner in the folder; flag it so the writer asks for one. Never invent a Telegram link.

## 1b. Formatting and layout (all MUST; the most common review comments)

| Area | Rule |
|---|---|
| Alignment | Justify every paragraph, the Introduction included (`style="text-align: justify;"`). |
| Font | Editor default font and size only; never other fonts or sizes such as 16 or 20. Text copied from Word, Google Docs, ChatGPT or a website is pasted with Paste as plain text. |
| Headings | Section titles Heading 2, sub-titles Heading 3. No bold text used as a heading, no bold on headings (Troubleshooting H3s included). Title case, not capitals ("Introduction", not "INTRODUCTION"). |
| Start of the body | Straight into the Introduction heading: no title, horizontal line or picture before it. Prerequisites is its own H2. |
| Spacing | One empty line between paragraphs, text and pictures, two pictures, code and pictures. Nothing touches or overlaps. |
| Pictures | Through Browse Server only (PNG or JPEG, uploaded into the SEO URL folder); never hotlinked or pasted from Google Docs, Word or a website (they keep an outside link such as googleusercontent.com and break into a red X; a common cause of missing pictures). Steps: Image button > Browse Server > S3 Image Manager opens on tutorial/<seo-url> > blue Upload > click the file to insert. 800 px wide at most: wider ones resized with the ratio lock on, narrower ones never enlarged. No stretched or blurred pictures; no picture of code already shown as text. |
| Links | Every link New Window (_blank). |
| Banner | Centred, 900 px wide, ratio locked, inserted via Browse Server, Link tab = the community's Telegram link, Target New Window (_blank). Check it opens the right group. |
| Length | Too long → split into a series (Parent + Sort Order 1, 2, 3…). |

In reviews of a live or saved page, check: `text-align: justify` on body paragraphs; `<h2>` for sections (not `<p><strong>`); `<strong>`/`<b>` inside headings; inline `font-family`/`font-size` styles; `<hr>` or content before the first `<h2>`; consecutive blocks with no spacing; `<img>` with `src` outside the tutorial's image folder (e.g. googleusercontent.com); image widths over 800 px or enlarged/stretched; banner width ≠ 900 px or not centred; `<a>` without `target="_blank"`.

## 2. Title, intro, writing quality

- Post Name (MUST): short, clear tutorial title, ≤60 characters; avoid numbers (e.g. version numbers) unless required; not repeated in the body.
- Intro (MUST): 2–4 sentences, what and why; name the main board (e.g. Maker ESP32, Raspberry Pi 5, micro:bit) and the main part, and link the board (first mention); link anything readers may want to learn more about (e.g. MediaPipe, ROS 2) to its official page. SHOULD open with the reader's problem, not "In this tutorial…".
- Video tutorial (if any): directly after the Introduction paragraph.
- Cover image / thumbnail (MUST): minimalist; clear pictures of the products used only, on a plain background (no photo of the real build needed); landscape 16:9; file named after the SEO URL.
- Writing (MUST): complete-beginner language, active voice, short sentences; full product names ("Raspberry Pi 5", not "Pi 5"); grammar and spelling checked across the whole tutorial (e.g. Grammarly). Read it back as a beginner: hard to read → simplify; too long → split into a series.

## 3. Hardware list and product links

- MUST: numbered list, product name linked; add the quantity only when more than one unit is used (e.g. "Jumper wires x10"). The name must clearly mean the same product as its product page (exact page title not required; a name pointing to a different product is a miss).
- MUST: cytron.io links use the SEO URL only, no domain: protocol `<other>`, path such as `/p-maker-esp32`, so readers stay in their own store.
- MUST: every link's target = New Window (_blank).
- MUST: main board linked at its first mention in the Introduction; later links allowed.
- SHOULD: a product family with versions may link to a store search (e.g. SPG30-XX*).
- MUST: note regional alternatives when products differ between the stores ticked in Store Name.
- MUST: no prices, discounts or stock levels in body text.
- MUST: every listed item attached in Related Product (fills the Hardware Components block).
- MUST: non-Cytron parts get a generic name, no link to another store.
- MUST: no new tutorials on discontinued products; revamps name the replacement.
- MUST: every product link opened on each ticked store before submitting.
- MUST: 3D, PCB files and downloads on Cytron-owned storage, linked under Downloads & Assets.
- MUST: name and link only in the list, no product pictures (the Hardware Components block shows them).
- MUST: a training-kit tutorial lists the kit, not each part; Related Product and thumbnail show the kit.
- MUST: list every item the build uses (cameras, cables included) and nothing else; List of Components and Related Product match exactly.
- MUST: link a product even if the Malaysia store doesn't sell it (other stores, e.g. SG, do); link products wherever they are named, Introduction included.
- Tracking parameters: team decision pending. Don't add or strip them unless asked; flag `&tracking=…&utm_campaign=…` with no `?`.

## 4. Code, versions, setup references

- MUST: long code as a public GitHub Gist, pasted via the editor's Source view. **Staff use their own GitHub account; interns
  use the intern GitHub account** (access from their supervisor; authentication code from Mat Liven). Never the account of someone outside Cytron. Accounts of
  ex-staff: suggest copying the Gist to a current Cytron account in a revamp.
- MUST: short command lines in the editor's Computer Code style, Shift+Enter for new lines.
- MUST: state the IDE/toolchain version and board package (e.g. "esp32 by Espressif Systems 3.3.12"); SHOULD: library versions.
- SHOULD: header comment (Project, Board e.g. Cytron Maker ESP32, main module).
- MUST: credentials as placeholders per §0, replaced by the reader in a Testing & Validation step.
- MUST: code as text, never a screenshot; terminal/Serial Monitor output may be a screen capture under Demo / Results.
- SHOULD: name built-in libraries (WiFi.h, WebServer.h) in Software Setup.
- MUST: quote error messages literally as the Troubleshooting H3.
- MUST: writer proofreads and tests by following the published steps on a clean setup. Peer review recommended.

## 5. WebAdmin fields (all compulsory; fill before writing; Save after every change)

Getting started: the supervisor sets up a short WebAdmin username (not the full IC name); log in at cytron.io/admin (first time:
Forgot Password); Tutorial > Tutorials > +; set the SEO URL first.

| Tab | Field | Rule |
|---|---|---|
| General | Post Name | §2, ≤60 chars. |
| General | Pitch (Meta Tag Description) | Not shown on the page: one complete sentence, "Build a/an [project] using [main board] and [main part] to [outcome].", ≤160 chars, unique. Count with code. |
| General | Description | The body (§1). |
| General | Post Tags | Board family and main board first (e.g. ESP32, Maker ESP32), then main modules, protocols, topic. |
| General | Meta Tag Keywords | 3–8 keywords, comma-separated; never the Pitch. |
| General | Meta Tag Title | Search results and browser tab: Post Name, optionally + key technology, ≤60 chars. |
| Data | Context Menu | Choose one: Education or Industry. |
| Data | SEO URL | Title in lowercase, hyphens, no special characters. Set it first. Never change after publishing; if forced, redirect keeping `/tutorial/`. |
| Data | Image Folder Name | Filled by WebAdmin and locked; images upload here; does not follow later SEO URL changes. |
| Data | Publish Date | The actual publish date, not the date the tutorial was written. |
| Data | Post Type | Tutorial, Project, Protip, News, Uncategorised. |
| Data | Project Level | Beginner: microcontroller with 1–2 sensors, or basic RPi. Intermediate: 2+ sensors, or RPi software projects. Advanced: AI or Industry projects. Only these three levels (no Expert). |
| Data | Status | Enabled (public), Disabled (hidden), Enabled but hide in catalog (unlisted, reachable by SEO URL). |
| Data | Sort Order | 1. In a series, parts in order: 1, 2, 3… Another number only on the supervisor's request. |
| Links | Author | Writer's name from the dropdown. |
| Links | Categories | Matching categories, e.g. Wireless & IoT > Maker ESP32. |
| Links | Store Name | Tick every store first; untick only a store where a Related Product isn't sold. |
| Links | Parent | Series only: the main post (e.g. series hub). Empty for standalone tutorials. |
| Links | Related Post | Existing posts on the same topic (e.g. Getting Started with Maker ESP32). |
| Links | Related Product | Exactly the items in List of Components (the kit for a kit tutorial); use the variation product code (parent product with options) where one exists. |
| Image | Image (thumbnail) | 16:9, preferably 1280×720, ~300 KB (max 1 MB), title in the image. Minimalist: clear pictures of the products used only (no photo of the real build needed), plain background, few colours, Cytron logo; nothing cut off by background removal; kit tutorials show the kit. Every series part has its own thumbnail. |

Other SEO and media rules (MUST):
- Series hub Pitch describes the whole series. Hub lists every part; prev/next works both ways.
- Headings: H2 sections, H3 inside, no empty headings, no H1 in the body.
- Internal links: SEO URL only; never `index.php?route=eblog/epost…`. Always link the Getting Started prerequisite.
- External links: official docs, new window; datasheets as `static.cytron.io` PDF or Google Docs `/preview`, never `/edit`.
- A graphic (screen capture, schematic, assembly photo) wherever a step needs one.
- Inline images: 800 px wide at most (wider → 800 px, ratio locked; narrower → original size, never enlarged), ~300 KB (max 1 MB), not stretched or blurred; every connection visible and labelled where needed. Only via Browse Server into the SEO URL folder, PNG or JPEG. Edit in the team Canva.
- Image files lowercase, hyphenated, starting with the project name; every image has 5–15 word alt text.
- YouTube: Share > Embed (Start at if needed), paste via the Embedded YouTube Video button.

## 6. Safety notes (optional; right after Introduction, recommended when a trigger applies)

Open with "This project is an educational prototype designed for learning…", then the concrete risk and precaution:

| Trigger | Note must say |
|---|---|
| Mains AC | Qualified people only; enclosed, rated relay module; unplug before touching. |
| LiPo / Li-ion | Correct polarity, no shorts, never charge unattended. |
| Motors, servos, robots | Fingers clear of moving parts; stop-on-disconnect failsafe in code. |
| Soldering / heat | Ventilation, eye protection. |
| Food, pets or people | Food-grade materials for food contact; someone checks in person if it fails. |
| Alarms, gas, fire, temperature, medical sensing | "Educational prototype, not a certified safety device." |
| 5 V sensors on 3.3 V pins | ESP32, Raspberry Pi and many other boards work at 3.3 V: level shifter or divider; state the pin voltage. |
| Wi-Fi passwords, bot tokens, API keys | Keep private; never publish real credentials (§0). |

Also: warranty notes where a build could void one; adult supervision for classroom use.

## 7. Review flow

Writer drafts → self-check and test → peer review (recommended) → SEO and link check → publish → writer's live-page check
within 7 days. Any miss returns the draft to the writer. A real credential stops publishing outright.

## 8. Pre-publish checklist

Credentials (any miss stops publishing)
- [ ] Every credential in body, Gists, downloads and repos is a §0 placeholder
- [ ] Body, Gists and downloads searched for password, ssid, token, auth, key, secret, api, bot: no real value
- [ ] No credential visible in any screenshot, GIF or video
- [ ] No Gist or repo revision ever held a real value, or that value has been revoked
- [ ] Tokens used for screenshots and video revoked or regenerated

Structure
- [ ] Every MUST section present in §1 order (close equivalent names and extra H2s are fine)
- [ ] Disclaimer / Safety Notes, Troubleshooting & Extra Tips and Downloads & Assets where useful
- [ ] Labelled system diagram at native ratio + pin-to-pin wiring table
- [ ] A graphic wherever a step needs one
- [ ] Demo / Results has photos, a YouTube embed or screen captures
- [ ] One Telegram banner at the end, linked to the matching community
- [ ] No empty headings or leftover placeholders

Formatting and layout
- [ ] Every paragraph justified; default font and size; copied text pasted as plain text
- [ ] Section titles H2, sub-titles H3; no bold on headings; no headings in capitals
- [ ] Body starts with the Introduction heading: no title, line or picture before it
- [ ] One empty line between paragraphs, pictures and code; nothing overlaps
- [ ] Every picture via Browse Server (PNG/JPEG), ≤800 px wide, not enlarged, stretched or blurred
- [ ] No picture of code already shown as text
- [ ] Telegram banner centred, 900 px, linked to the right group, New Window (_blank)
- [ ] Conclusion at the end; video tutorial (if any) right after the Introduction
- [ ] Read back as a beginner; split into parts if too long

Title and intro
- [ ] Post Name short and clear, ≤60 chars, no numbers unless required, not repeated in the body
- [ ] Introduction 2–4 sentences: what and why
- [ ] Thumbnail 16:9, ~300 KB (max 1 MB), title in image, minimalist, product pictures only
- [ ] Proofread (Grammarly)

Products
- [ ] Every item linked by its product name (quantity only when more than one), clearly the right product, no product pictures
- [ ] cytron.io links use the SEO URL only, protocol `<other>`
- [ ] Every link opens in New Window (_blank)
- [ ] Product links work on every ticked store; regional alternatives noted
- [ ] Main board linked at first mention in the Introduction
- [ ] No prices/discounts in body
- [ ] Related Product holds exactly the items in List of Components (the kit for a kit tutorial)
- [ ] No discontinued products

Admin, SEO and media
- [ ] Every WebAdmin field filled (General, Data, Links, Image)
- [ ] Project Level matches the §5 definitions
- [ ] Pitch one complete "Build a…" sentence, ≤160 chars, unique
- [ ] Meta Tag Keywords 3–8 keywords only
- [ ] No `index.php` URLs; every link opened and working, incl. hub and prev/next
- [ ] Inline images ≤800 px wide (wider resized, ratio locked; narrower not enlarged), ~300 KB, in the SEO URL folder, alt text, hyphenated names
- [ ] Gist and YouTube embeds render correctly

Code and safety
- [ ] Long code in a public Gist (staff: own GitHub account; interns: the intern account); short commands in Computer Code style
- [ ] IDE/toolchain version stated
- [ ] Safety notes, if included, name the concrete risk and precaution
- [ ] Writer proofread and tested by following the published steps
- [ ] Peer review completed (recommended)

After publishing
- [ ] Live-page check within 7 days (links, embeds, browser-tab title), fixes applied

## Notes for Claude

- Keep this skill in step with the live guide page. Its hub copy is `projects/tutorial-writing-guide/cytron-tutorial-rules-SKILL.md`
  in the private Cytron-Build-Tutorial repo; the guide page source is `index.html` in the same folder.
- my.cytron.io pages usually return 403 to fetching. Say so and work from what the user pastes or uploads (saved .html pages work well); never guess what a live page says.
- Don't invent product slugs. If unknown, leave `/p-[slug]` as a visible placeholder and list it for the writer.
- Count characters for Post Name, Meta Tag Title and Pitch with code, don't estimate.
- Never repeat a credential value found in a tutorial, Gist, file or the old WI PDF (it holds shared-account passwords) in drafts, docs, reports or chat. Mask it.
- Reference tutorials (for the team, not for writers to copy): ESP32 Smart Home Dashboard with Real-Time Sensor Data, ESP32 High Temperature Alert System, ESP32 Water Tank Monitoring with Web Dashboard, ESP32 Digital Clock (older layout). Several still break a rule or two.