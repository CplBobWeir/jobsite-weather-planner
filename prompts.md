
# AI Prompt Log

This file records the requests made to the AI coding agent, what was changed, and whether the changes worked.

## 2026-11-22
- Asked to update only the Purpose section of spec.md using the improved paragraph proposed in the prior review.
- Changed the Purpose paragraph to describe the responsive seven-day planning dashboard, the three activities, GO/CAUTION/NO-GO ratings with explanations, and the non-safety-guarantee limitation.
- Worked: successfully; no other spec sections or application code were changed.

## 2026-11-22
- Asked to update only the Inputs section of spec.md with default values, valid ranges, units, and input controls for every input.
- Changed the Inputs section to include map selection, crane wind limit, concrete minimum temperature, roofing precipitation threshold, working hours in the jobsite's local timezone, and the fixed seven-day Open-Meteo forecast period.
- Set working hours to default to 7:00 AM-5:00 PM and clearly defined the controls and ranges.
- Worked: successfully; no application code or other spec sections were changed, and no Git commit was created.

## 2026-11-22
- Asked to update only the Calculations section with GO, CAUTION, and NO-GO rules, missing-data handling, the worst-hourly-day rule, and OSHA, ACI, and NRCA references.
- Changed the Calculations section to define crane, concrete, roofing, working-hour, missing-data, and reference rules. Concrete thresholds now follow the configured minimum temperature, and all thresholds are labeled as planning assumptions.
- Worked: successfully; no other spec sections or application code were changed, and no Git commit was created.

## 2026-11-22
- Asked to update only the Outputs section using the recommendations from the Outputs Review.
- Changed the Outputs section to describe the interactive map, selected coordinates and timezone, loading status, seven-day calendar, color-coded text ratings, expandable daily details, units, working hours, missing-data warnings, error states, and the visible planning-guidance disclaimer.
- Worked: successfully; no other spec sections or application code were changed, and no Git commit was created.

## 2026-11-22
- Asked to update only the Look and Feel section using the recommendations from the review.
- Changed the section to specify a header with collapsible settings, an initial jobsite-selection prompt, map above calendar, neutral construction-oriented styling, labeled and icon-supported ratings, expandable daily details, and a vertically stacked, touch-friendly mobile layout.
- Worked: successfully; no other spec sections or application code were changed, and no Git commit was created.

## 2026-11-22
- Asked to update only the Validation section with the Denver test location, real-data validation procedure, hand calculations, app comparison, and NWS comparison.
- Updated the illustrative crane example with 22 mph sustained wind and 28 mph gust, showing the 27 mph caution threshold and expected CAUTION result. Added a distinct post-build validation procedure using real hourly data without inventing readings or app results.
- Worked: successfully; no other spec sections or application code were changed, and no Git commit was created.

## 2026-11-22
- Asked to update only Out of Scope, keep existing exclusions, add limits for saved jobsites/profiles, alerts/history, NWS integration, address search/geocoding, native apps/offline operation, and preserve the two planned in-scope features and safety disclaimer.
- Updated Out of Scope with the requested exclusions and explicitly stated that Custom Working Hours and Printable Jobsite Weather Report remain in scope.
- Worked: successfully; no other spec sections or application code were changed, and no Git commit was created.

## 2026-11-22
- Asked to add a Features section documenting Custom Working Hours and Printable Jobsite Weather Report as separate extras after required features are built and validated.
- Added both feature descriptions, their origin, behavior, print content, browser print approach, and implementation order. Clarified that the initial version uses fixed 7:00 AM-5:00 PM hours and aligned related Inputs, Calculations, Outputs, and Look and Feel references.
- Worked: successfully; no application code was written and no Git commit was created.

## 2026-11-22
- Asked to add the approved app overview and complete six-stage build plan to spec.md while preserving its sections and Features, and not to begin implementation.
- Added the overview near the top and the six sequential build stages at the end, including build goals, checks, dependencies, required validation before extras, and single-file GitHub Pages constraints. Recorded this request.
- Worked: successfully; documentation only; no application code or index.html was created, and no Git commit was made.

## 2026-11-22
- Asked to build only Stage 1 as a responsive visual mockup in a single index.html file, with demonstration weather values and no APIs or real calculations.
- Created the static dashboard mockup with collapsible threshold settings, jobsite map placeholder, seven-day sample rating cards, expandable sample details, loading/error previews, and a visible planning disclaimer.
- Worked: successfully; the Stage 1 mockup was created without weather API connections or rating calculations. No later stage was built and no Git commit was created.

## 2026-11-22
- Asked to build only Stage 2: replace the map placeholder with an interactive Leaflet map, connect Open-Meteo for seven days of local hourly weather, keep working hours fixed at 7:00 AM-5:00 PM, allow threshold adjustments, and show loading, error, and missing-data states without calculating activity ratings.
- Added map-based jobsite selection with coordinates and timezone, OpenStreetMap tiles, seven-day Open-Meteo forecasts for temperature (°F), sustained wind (mph), wind gusts (mph), and precipitation probability (%), validated threshold inputs, and local-time hourly details from 7:00 AM through 4:00 PM. Missing hourly timestamps and values are called out without substituting data; working hours remain fixed and no GO/CAUTION/NO-GO calculations were added.
- Tested in the browser: Leaflet and a real Open-Meteo forecast loaded; selecting a different point refreshed the coordinates and forecast; the selected day showed 10 local work-hour records with labeled units; a 390 px mobile viewport had no page-level horizontal overflow; invalid threshold input showed validation feedback; simulated missing values, a missing hour, and an entirely missing forecast day produced clear warnings; and a simulated HTTP 503 displayed an error and recovered on retry.
- Worked: successfully; Stage 2 is ready for user testing. No later stage was built and no Git commit was created.

## 2026-11-22
- Asked to build only Stage 3 using the exact documented activity thresholds, hourly work window, worst-hour aggregation, missing-data behavior, and daily details, while preserving Stage 2 and deferring later features and the commit.
- Implemented crane, concrete, and roofing hourly ratings and daily worst-hour results. The seven-day calendar now shows labeled/icon ratings; selected-day details show hourly values and ratings, the highest-risk hour, explanations, and missing-data warnings. Missing timestamps are represented as missing working-hour readings. Valid threshold edits immediately recalculate without another forecast request; invalid thresholds mark ratings unavailable.
- Browser-tested boundary fixtures: crane 28 mph gust and 27 mph wind = CAUTION, 30 mph = NO-GO; concrete 40°F and 45°F = CAUTION and 39°F = NO-GO; roofing 15% and 30% = CAUTION and 31% = NO-GO. Verified worst-hour precedence, missing values/timestamps, known NO-GO overriding missing-data CAUTION, and inclusion of 7:00 AM through 4:00 PM while excluding 5:00 PM.
- Also verified threshold changes caused no second API request, invalid thresholds withheld ratings, a simulated HTTP 503 cleared stale results and recovered, and the live Open-Meteo forecast still loaded. Desktop (1280 px) and mobile (375 px) layouts had no page-level horizontal overflow; the hourly table scrolls within its container on mobile. `git diff --check` passed.
- Worked: successfully; Stage 3 only is ready for user testing. Custom Working Hours, the printable report, later stages, and a Git commit were not added.

## 2026-11-22
- Asked to collect Denver Open-Meteo hourly weather data for Stage 4 validation, record its retrieval time and forecast date, list the spec's default thresholds, identify the NWS hourly forecast endpoint, and defer calculations, app changes, publishing, and commits.
- Retrieved the actual Open-Meteo forecast for 39.7392, -104.9903 with America/Denver local time. At 2026-11-22 16:55:19.027 -07:00, confirmed 2026-11-28 was the latest forecast date with all ten 7:00 AM-4:00 PM timestamps and all requested values present. Identified the Denver NWS point and hourly forecast endpoints.
- Worked: successfully; the raw weather table and threshold defaults were provided in the response. No hand ratings or forecast comparisons were calculated, no application file was changed, and no Git commit was created.

## 2026-11-22
- Asked to hand-check the November 28 Denver data against the app using the exact saved forecast, document inputs/calculations/app results in the Validation section, and avoid a fresh forecast, publishing, rule changes, or a commit.
- Browser-tested the app with a fixture containing the exact ten captured Open-Meteo records for November 28. The app returned Crane GO, Concrete CAUTION, and Roofing GO, matching the hand calculations; no new API forecast was requested. Added the saved input table, default thresholds, hand calculations, app results, and match outcome to spec.md's Validation section.
- Worked: successfully; all three ratings match. No calculation rules or application code were changed, nothing was published, and no Git commit was created.

## 2026-11-22
- Asked to compare the saved November 28 Denver Open-Meteo forecast with the NWS hourly forecast, calculate absolute differences for matching hourly temperature, wind, and precipitation values, document the comparison in spec.md, record NWS retrieval time, and avoid app changes, publishing, or a commit.
- Retrieved all ten NWS hourly periods for November 28 from 7:00 AM through 4:00 PM at 2026-11-22 16:59:02.519 -07:00. Calculated hourly absolute differences against the saved Open-Meteo values and added the values, difference table, retrieval details, and a brief explanation of forecast variation to spec.md's Validation section.
- Worked: successfully; matching NWS data was available for all ten hours. No application code was changed, nothing was published, and no Git commit was created.

## 2026-11-22
- Asked to build only Stage 5, Custom Working Hours, using the validated Stage 4 app and forecast; add jobsite-local start/end inputs defaulting to 7:00 AM-5:00 PM, recalculate ratings and hourly details without another download, validate same-day ranges, test missing data and mobile layout, and defer Stage 6 and the Git commit.
- Added whole-hour jobsite-local time controls, same-day start-before-end validation, and selected-hour filtering with the start included and end excluded. Forecast records are retained for the full local day so valid custom periods can extend beyond the default hours. The calendar, details, risk explanations, missing-data counts, and forecast status now reflect the selected period. Clarified the hour-resolution and time-range rules in spec.md.
- Browser-tested with a fixture containing the exact saved November 28, 2026 Open-Meteo readings for 7:00 AM-4:00 PM, plus controlled supplemental/missing hours for testing custom periods. Default ratings matched the Stage 4 results: Crane GO, Concrete CAUTION, Roofing GO. A 5:00-7:00 AM selection displayed only the 5:00 and 6:00 AM records and showed missing-data CAUTION warnings. Equal start/end and a non-hour-aligned time were rejected; restoring 7:00 AM-5:00 PM restored the same ratings and ten detail rows. Confirmed one forecast request for the test, no page errors, and no horizontal overflow or clipped time controls at the mobile viewport.
- Worked: successfully; Stage 5 only is ready for user testing. Stage 6, publishing, and a Git commit were not performed.
