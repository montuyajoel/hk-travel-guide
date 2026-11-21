# Hong Kong & Macau Trip Navigator — Features & Change Log

**Project:** Hong Kong & Macau Trip Navigator  
**Repository:** [montuyajoel/hk-travel-guide](https://github.com/montuyajoel/hk-travel-guide)  
**Production site:** https://hk-macau-trip-navigator.vercel.app  
**Trip dates:** 13–18 December 2026  
**Last documented update:** 21 November 2026

This document records the app's user-facing features, trip content, implementation notes, and the major changes made during development. Operational details such as live availability, prices, schedules, and external image hosting can change.

---

## 1. Product overview

A mobile-friendly trip companion for a six-day Hong Kong and Macau itinerary. It combines a day-by-day plan, map directions, progress tracking, food recommendations, coffee stops, optional attractions, and dedicated planning pages.

The design uses a clean, editorial travel-guide style: white space, large destination imagery, blue rounded action links, and a red destination accent. Layouts are responsive for mobile and desktop.

## 2. Main itinerary and trip planning

The itinerary covers **13–18 December 2026**, with a relaxed pace of roughly three to five main activities per day.

| Date | Day theme | Main plan |
|---|---|---|
| Dec 13 | Arrival & harbour | Airport A21 arrival stop at Bank Centre, hotel check-in, Avenue of Stars |
| Dec 14 | Central & Peak | Man Mo Temple, PMQ, Peak Tram, Peak Tower, Star Ferry |
| Dec 15 | Disneyland | Travel to Hong Kong Disneyland via Olympic, Sunny Bay and the Disneyland Resort Line |
| Dec 16 | Macau | Ferry to Macau Outer Harbour, historic centre, Senado Square, Ruins of St Paul's, optional Cotai/Venetian |
| Dec 17 | Gardens & markets | Nan Lian Garden, Chi Lin Nunnery, Mong Kok markets, Temple Street |
| Dec 18 | Airport departure | Airport-bound A21 stop on Argyle Street and return to the airport |

### Itinerary interactions

- Day selector to switch between the six daily plans.
- Individual stop cards with transport mode and practical route notes.
- Directions links for each leg and destination-only links.
- Google Maps / Apple Maps provider toggle.
- Full-day route link.
- Stop completion checkboxes and a progress indicator.
- Personal notes attached to itinerary stops; progress and notes are stored in browser local storage.
- Optional nearby stopovers and coffee suggestions for each day.

### Important transport notes

- Arrival and departure use different A21 stops. The arrival stop is Bank Centre; the airport-bound departure stop is near Yau Tsim Mong District Health Centre on Argyle Street.
- Disneyland routing uses Olympic → Sunny Bay → Disneyland Resort Line.
- Macau ferry departure is planned from Hong Kong Macau Ferry Terminal at Shun Tak Centre to Macau Outer Harbour. Ferry times in the guide are planning context, not a booking or confirmation.
- The app creates map directions; it does not book tickets or guarantee live transit schedules.

## 3. Homepage weather

The homepage includes a live Hong Kong weather panel powered by the Open-Meteo forecast API.

Displayed information:
- Current temperature.
- Feels-like temperature.
- Next-hour precipitation probability.
- Last-updated time in Hong Kong time.

Implementation notes:
- Hong Kong coordinates: 22.3193, 114.1694.
- Refresh interval: every 30 minutes.
- No API key is required for the current integration.
- Open-Meteo is credited in the interface.

**Latest weather design decision:** The homepage shows Hong Kong only. Macau is geographically close and usually has broadly similar conditions, so a second city card was considered unnecessary clutter. The interface notes that Macau weather is generally similar and recommends checking local wind conditions before the ferry, where marine conditions matter.

The dedicated Weather & Crowd page remains a separate navigation destination. Do not interpret the homepage panel as a marine forecast or ferry-operation status.

## 4. Food guide — `food.html`

A dedicated food guide presents Hong Kong and Macau dishes and restaurant suggestions.

Features:
- Photo-led food cards with aligned image sizing.
- Must-try checklist with 16 items.
- Completion count showing how many of the 16 items have been checked.
- Checklist state saved in browser local storage using the key `hkMacauMustTryChecklist2026`.
- Responsive card layout: one column on small screens and two columns on larger screens.

Image note: food imagery is sourced from external image hosts and may be illustrative. Availability and image URLs can change; images should be checked periodically for broken links or mismatched dishes.

## 5. MICHELIN and restaurant guide — `michelin.html`

The Michelin page includes a curated selection of restaurants in Hong Kong and Macau.

Features:
- Restaurant listings.
- Estimated per-person price ranges.
- Map/directions links.
- Restaurant options across both destinations.

Prices are planning estimates, not live menu quotations. Menus, prices, opening hours, and Michelin status can change and should be rechecked before visiting.

The wider itinerary also includes day-specific restaurant recommendations with approximate spend in the local currency.

## 6. Disneyland playbook — `disney.html`

A dedicated Hong Kong Disneyland planning page.

Features include:
- Park map links.
- Overview of eight themed lands.
- Must-try attractions and rides.
- Restaurant suggestions.
- A relaxed suggested ride plan.
- Practical park-day tips.

The page is designed as a planning aid; attraction operations, park hours, showtimes, and queue conditions are subject to change.

## 7. Currency converter — `currency.html`

A simple HKD ⇄ PHP currency conversion page.

- Converts between Hong Kong dollars and Philippine pesos.
- Uses the Frankfurter exchange-rate API.
- Shows an indicative rate rather than a guaranteed bank/card transaction rate.
- Exchange-rate data generally updates on business days and is not a tick-by-tick quote.

## 8. Weather and crowd page — `weather.html`

A separate page linked from the homepage for weather and crowd-related planning. Treat third-party information and links as external references; the app does not claim continuous crowd, queue, or location tracking unless a specific live data integration is visibly provided.

## 9. Food, coffee and optional stop recommendations

The itinerary contains day-specific restaurant and coffee recommendations, plus optional nearby stopovers.

Examples of coffee stops retained in the plan:
- Little Cove Espresso · Central Yards.
- % Arabica · The Henderson.
- Macchina · Wan Chai.
- % Arabica · Victoria Dockside / K11 MUSEA.
- Starbucks · Avenue of Stars.
- Urban Coffee Roaster · Tsim Sha Tsui.

ICHIRAN Mong Kok was added to the Dec 13 food recommendations:
- Shop B, G/F, The Beacon, 88 Sai Yee Street, Mong Kok.
- Japanese tonkotsu ramen.
- Estimated spend: HK$101–200 per person.
- The listing notes individual counter seating and approximate walking distance from Mong Kok MTR Exit E2. Check current hours before visiting.

Optional stopover examples include Yau Ma Tei, Tsim Sha Tsui Clock Tower, Tai Kwun, Central Market and Hong Kong Observation Wheel. Destination photos are included where configured.

## 10. Visual design and responsive improvements

- Shared editorial visual direction across the homepage and subpages.
- Large destination and attraction imagery.
- Responsive layouts for narrow mobile screens.
- Food-card photo alignment improvements and consistent image sizing.
- Disneyland header sizing adjusted to prevent mobile overflow.
- Navigation links between itinerary, food, Disneyland, currency, weather and Michelin pages.
- Map-provider selector for Google Maps and Apple Maps.

## 11. Notable change history

This is a feature-level history assembled from the development record, not a complete commit-by-commit Git log.

| Change | Summary |
|---|---|
| Itinerary foundation | Added six-day Hong Kong and Macau plan with transport legs, route links and day selection |
| Map controls | Added Google Maps / Apple Maps selection and route-opening links |
| Trip progress | Added stop completion tracking and personal notes |
| Optional stops | Added nearby attraction/stopover suggestions and destination photos |
| Coffee recommendations | Added day-specific coffee stops near planned routes |
| Food guide | Added food cards, photo layout refinements and a 16-item persistent must-try checklist |
| Restaurant pricing | Added estimated per-person price ranges to food recommendations |
| Michelin guide | Added restaurant price estimates and map directions |
| Disneyland playbook | Added park map, eight-land overview, must-try rides, dining suggestions and a relaxed ride plan |
| Currency page | Added HKD ⇄ PHP conversion using Frankfurter |
| Weather page | Added a separate weather/crowd planning destination |
| Homepage weather | Added live Hong Kong conditions using Open-Meteo, with a 30-minute refresh |
| Weather simplification | Removed the separate Macau homepage weather card; retained Hong Kong weather and a Macau/ferry wind note |
| ICHIRAN recommendation | Added ICHIRAN Mong Kok to Dec 13 food suggestions with address, description and estimated spend |
| Disneyland preparation reminder | Added a Dec 14 reminder to buy snacks/food and a bottle of water for the Dec 15 park day |
| Design refinement | Applied a cleaner editorial travel-guide style and improved mobile presentation |
| Image maintenance | Replaced or corrected a number of food and landmark image references after visual mismatch/broken-image feedback |

### Recent repository commits recorded in the project notes

- `99cf2838c55d44c19fe351307cccaea688c9cce7` — homepage live weather widget.
- `f15f85f21de5034c2861cc0747d0b1907f7fdc8b` — ICHIRAN Mong Kok recommendation and restaurant-card photo rendering.
- `5c62b92259498e5d1e2fb72224fda5f7aee02796` — Dec 14 Disneyland preparation reminder.
- `4d4c33b7e09e7b44568bf53a87a498f25a5fda64` — homepage weather simplified to Hong Kong only.

## 12. Technical notes

- Front end is a set of static HTML pages with CSS and JavaScript.
- Main pages: `index.html`, `food.html`, `michelin.html`, `disney.html`, `currency.html`, and `weather.html`.
- Deployed on Vercel and source-controlled in GitHub.
- External integrations currently documented: Open-Meteo for homepage weather and Frankfurter for currency rates.
- Maps open through Google Maps or Apple Maps links.
- Checklist, completion state and personal notes use browser local storage where implemented.
- No user account or backend sync is described by the current feature set; local browser data should not be assumed to sync across devices.

## 13. Limitations and maintenance checklist

Before travel, recheck:
- Ferry schedules, terminal and ticket details.
- A21 stop locations and service information.
- Attraction opening hours, park hours and ride operations.
- Restaurant hours, prices, reservations and addresses.
- Exchange rates and card/bank fees.
- Weather, rain, wind and ferry/marine conditions.
- External photo URLs and image-to-dish/landmark accuracy.
- Third-party map links and API availability.

The app is a personal trip-planning companion, not a booking platform, live transit authority, or guarantee of business/attraction operating status.

---

*End of documentation.*
