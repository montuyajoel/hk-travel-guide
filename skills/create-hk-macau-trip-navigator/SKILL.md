---
name: create-hk-macau-trip-navigator
description: Build, extend, maintain, and deploy the Hong Kong & Macau Trip Navigator website: a mobile-first static travel companion with itinerary, maps, food, coffee, attraction guides, currency, weather, shopping, poses, and Instagram Reel inspiration.
---

# Create and maintain the Hong Kong & Macau Trip Navigator

## Purpose

Use this skill when asked to create, extend, redesign, debug, or maintain the Hong Kong & Macau Trip Navigator website. The goal is to make real changes in the existing repository, not merely provide instructions or mockups.

## Project identity

- **Website:** Hong Kong & Macau Trip Navigator
- **GitHub repository:** `montuyajoel/hk-travel-guide`
- **Production URL:** `https://hk-macau-trip-navigator.vercel.app`
- **Vercel project:** `hk-macau-trip-navigator`
- **Production alias:** `https://hk-macau-trip-navigator.vercel.app`
- **Primary branch:** `main`
- **Trip dates:** 13–18 December 2026
- **Technology:** Static HTML pages, CSS, vanilla JavaScript; deployed on Vercel
- **No application backend or account sync is documented.** Browser-local state must not be described as cross-device synced.

## Non-negotiable deployment rule

**Do not deploy automatically.**

- Implement the requested change and commit it to GitHub `main`.
- Tell the user it is saved to GitHub and not deployed.
- Wait for an explicit instruction such as “deploy”, “deploy now”, or “proceed and deploy”.
- Only then deploy the latest `main` commit to Vercel production and wait until the deployment reports `READY`.
- Never say a change is live until production deployment is verified READY.
- If the user asks only for a preview or code change, do not deploy.

## User experience and design principles

- Mobile-first and responsive; many users will use the site on a phone while travelling.
- Editorial travel-guide aesthetic: generous white space, large destination photography, clean typography, blue rounded action links, and restrained red destination accents.
- Keep navigation clear and compact, controls touch-friendly, and card layouts consistent.
- **Always include relevant photos when creating or materially updating visual guide content.**
- Prefer genuine, location-accurate photos of the actual Hong Kong/Macau place, attraction, dish, café or product. Avoid generic imagery that could misrepresent the subject.
- Check image relevance, crop, alignment, aspect ratio, and mobile rendering. Avoid stretching; use `object-fit:cover` for fixed image frames.
- If an image URL cannot be verified, be transparent and prefer a reliable alternative rather than claiming it was checked.
- Preserve existing working features, user data keys, navigation and styling unless the user asks to change them.
- Do not introduce duplicate calls-to-action or redundant page sections.
- Respect reduced-motion preferences for animations and transitions.
- Dark/light mode is a shared feature. Its localStorage key is `hkMacauTheme2026`; avoid breaking its header icon control or theme persistence.

## Repository structure and page responsibilities

The main pages currently include:

| File | Purpose |
|---|---|
| `index.html` | Welcome / landing page, guide navigation, Hong Kong live weather panel, and link to the separate itinerary |
| `itinerary.html` | Six-day trip planner, day navigation, route directions, progress, notes, food, coffee and optional stops |
| `food.html` | Hong Kong and Macau food guide with 16-item must-try checklist |
| `michelin.html` | Michelin and restaurant guide with estimated prices and directions |
| `disney.html` | Hong Kong Disneyland playbook: park maps, eight themed lands, rides, dining and relaxed plan |
| `currency.html` | HKD ⇄ PHP currency converter using Frankfurter API |
| `weather.html` | Weather and crowd-planning reference page; official HKO and Macau weather links plus third-party resources |
| `shopping.html` | Shopping districts and personal wishlist |
| `poses.html` | Instagram pose/photo inspiration gallery |
| `reel-inspo.html` | Instagram Reel Inspiration gallery, original full-size vertical embeds |
| `FEATURES_AND_CHANGELOG.md` | User-facing feature and maintenance documentation |

The welcome page and itinerary are separate. Keep the welcome page focused on introducing the trip and guide pages; the itinerary belongs on `itinerary.html`.

## Trip baseline

Use these as the established trip facts unless the user explicitly changes them:

- Dates: 13–18 December 2026.
- Hotel: iclub Mong Kok Hotel, 2 Anchor Street, Mong Kok, Hong Kong.
- Day 1, Dec 13: Airport A21 arrival stop at Bank Centre, Nathan Road; hotel; Avenue of Stars.
- Day 2, Dec 14: Man Mo Temple, PMQ, optional Hopewell Centre scenic glass elevators, Peak Tram, Peak Tower, Star Ferry.
- Day 3, Dec 15: Hong Kong Disneyland via Olympic → Sunny Bay → Disneyland Resort Line.
- Day 4, Dec 16: ferry from Sheung Wan / Shun Tak Centre to Macau Outer Harbour; historic centre including Senado Square and Ruins of St Paul's; optional Cotai / Venetian. Ferry times are planning targets, not bookings.
- Day 5, Dec 17: Nan Lian Garden, Chi Lin Nunnery, Mong Kok markets, Temple Street.
- Day 6, Dec 18: return via the airport-bound A21 stop on Argyle Street near Yau Tsim Mong District Health Centre. This is not the same stop as the arrival stop.
- Keep a relaxed pace, generally three to five main activities per day, with optional stops clearly labelled as optional.

## Important existing features and implementation details

### Itinerary page
- Day selector with Previous/Next buttons and swipe navigation (swipe left advances; swipe right goes back).
- Directional day-change animation, respecting reduced motion.
- Google Maps / Apple Maps provider toggle.
- Directions for route legs and destination-only links.
- Full-day route link.
- Stop completion tracking and progress bar.
- Personal notes per stop.
- Food, optional nearby stopovers, and day-specific coffee suggestions.
- Browser state key: `hkMacauNavigatorV3`.
- Coffee and place photos are configured in `COFFEE_BY_DAY` and `PLACE_PHOTOS` arrays/maps in `itinerary.html`.

### Homepage weather
- Live Hong Kong conditions from Open-Meteo.
- Displays current temperature, feels-like temperature, next-hour precipitation probability and last update in Hong Kong time.
- Refreshes every 30 minutes.
- Hong Kong only; Macau was deliberately removed from the live homepage widget to simplify the display.
- Do not present this as a marine forecast or ferry-operation status.

### Food guide
- Must-try checklist has 16 items.
- Checklist uses localStorage key `hkMacauMustTryChecklist2026`.
- Keep food photography aligned and cards consistent.
- Checklist state is local to the browser/device.

### Currency
- HKD ⇄ PHP.
- Frankfurter API rates are indicative and generally update on business days, not continuously.

### Shopping
- Wishlist supports item name, category, HKD budget, suggested trip day, product URL and notes.
- Items can be marked bought, have their planned day changed, be deleted, and exported as JSON.
- localStorage key: `hkMacauShoppingWishlist2026`.
- Wishlist does not sync across devices.

### Reel Inspiration
- Keep the original full-size Instagram embeds stacked vertically.
- New user-supplied Reels are added at the top with sequential numbering.
- Instagram owns embed playback and availability; do not promise playback is guaranteed.
- Follow the dedicated `add-instagram-reel` skill when adding a single Reel URL.

### Poses
- Instagram embed gallery; preserve existing references and layout when extending.

## Working workflow

### 1. Understand the request

- Identify the page or feature involved.
- If the request is clear, proceed without asking unnecessary questions.
- If a crucial design/content choice is missing, ask one concise clarification.
- Determine whether the change affects one page, shared styles/scripts, navigation, or documentation.
- For current prices, opening hours, addresses, schedules, official policies, or other changing travel details, verify current information before adding it. Clearly mark estimates and optional detours.

### 2. Inspect current source before editing

Always fetch the latest version of the relevant file(s) from GitHub `main` before editing. Do not rely on an old local copy, an earlier chat snippet, or a remembered version.

GitHub fetch action pattern:

```js
const r = await tools.mcp__GitHub__fetch_file({
  repository_full_name: "montuyajoel/hk-travel-guide",
  path: "index.html",
  ref: "main",
  encoding: "utf-8"
});
const content = r.result.content;
const blobSha = r.result.sha;
```

Fetch every file that needs to change. If a page links to another page, inspect the relevant navigation and shared conventions before altering it.

### 3. Implement carefully

- Make the smallest coherent change that fully satisfies the request.
- Preserve existing HTML structure, CSS conventions, JavaScript behavior and localStorage keys.
- Do not overwrite newer GitHub content with a stale copy.
- For new pages, follow the site's existing responsive and editorial design system and add links from the appropriate navigation / homepage guide grid.
- For interactive controls, implement working behavior; do not add decorative controls that do nothing.
- For local persistence, use a clear, stable key and explain if data is browser-local.
- Add meaningful alt text to images.
- Use semantic headings, accessible labels, keyboard focus states, and touch-friendly targets.
- Avoid adding dependencies or build tooling unless required; the project is intentionally a lightweight static site.

### 4. Validate

Before committing:
- Check for malformed HTML, broken JavaScript syntax, mismatched tags, duplicate IDs, and incorrect relative links.
- Check mobile and desktop layout implications.
- Confirm new images correspond to their labels and crop well.
- Confirm navigation links and external map / Instagram links are correct.
- Check that localStorage keys and existing saved data are not unintentionally changed.
- For data-driven lists, ensure ordering and labels remain accurate.
- If a page uses external APIs, provide graceful fallback/error text and do not imply the service is guaranteed.
- If practical, inspect the rendered page or run a local syntax/HTML check before committing.

### 5. Commit to GitHub

For an existing file, update using the freshly fetched blob SHA:

```js
const u = await tools.mcp__GitHub__update_file({
  repository_full_name: "montuyajoel/hk-travel-guide",
  path: "index.html",
  content: updatedContent,
  sha: blobSha,
  message: "Describe the change",
  branch: "main"
});
```

For a new file, use the GitHub create-file action with a descriptive commit message.

After the write:
- Capture the commit SHA.
- When practical, fetch the file again to verify the saved content.
- If multiple files need changes, update them sequentially and use the latest blob SHA for each path.
- Update `FEATURES_AND_CHANGELOG.md` when a material feature is added or removed.

### 6. Report clearly

Summarize:
- What changed and which page(s) were affected.
- The GitHub commit link.
- The relevant page link, but label it as the live page only if deployed.
- State explicitly: **“Saved to GitHub, not deployed.”**
- If there is a known limitation (unverified image, external API dependency, local-only storage), state it briefly.

## Deploy only when asked

Vercel project details:

- Team ID: `team_cfrMtPfuGNRkKYQsyjphs8LL`
- Team slug: `home-care-ie`
- Project ID: `prj_3JkX39cmIjhTYyGuX4CkwO8Ry8T8`
- Project name: `hk-macau-trip-navigator`
- GitHub repo ID: `1466440176`
- Production alias: `https://hk-macau-trip-navigator.vercel.app`

When and only when the user explicitly requests deployment:
1. Identify the latest `main` commit SHA containing the requested changes.
2. Create a Vercel production deployment from GitHub `main` at that SHA, using the project/team identifiers above.
3. Poll deployment status until it reaches `READY` or a terminal failure state.
4. If READY, report the production URL and deployment status.
5. If it fails, report the failure accurately; do not claim the site is updated.

Do not deploy automatically after commits, after adding Reels, or after editing content.

## Content accuracy and trust

- Distinguish itinerary suggestions from confirmed bookings.
- Do not invent ferry times, opening hours, prices, or live availability.
- Label restaurant and coffee budgets as estimates.
- Recheck business addresses and opening hours before recommending a new stop.
- A map link is a navigation shortcut, not a guarantee of route or service status.
- Official transport, attraction, weather and business sources are preferred for changing details.
- Preserve the user's established itinerary choices and relaxed pacing unless asked to revise them.

## Related workflow

For adding one Instagram Reel URL to `reel-inspo.html`, use the separate `add-instagram-reel` skill. This website skill governs the broader app architecture, design, implementation, maintenance, GitHub workflow and deployment policy.
