
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
