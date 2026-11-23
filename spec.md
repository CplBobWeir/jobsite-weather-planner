
# Jobsite Weather Planner

## Overview
Build a responsive, single-file `index.html` dashboard for construction managers to select a jobsite on an interactive map, retrieve a seven-day Open-Meteo forecast, and review weather-based GO, CAUTION, or NO-GO ratings for crane lifts, concrete pours, and roofing. The initial version uses fixed 7:00 AM-5:00 PM jobsite-local hours. It shows weather values, risk explanations, missing-data warnings, and a visible planning-guidance disclaimer. The required app will be completed and validated before implementing the two extra features.

## Purpose
Create a responsive web dashboard that helps construction managers compare crane lifts, concrete pours, and roofing work across the next seven days at a selected jobsite. The app will display simple weather-based GO, CAUTION, and NO-GO ratings with short explanations, supporting preliminary scheduling decisions rather than guaranteeing that conditions are safe.

## Inputs
- Jobsite location: selected by clicking an interactive map. The selected latitude and longitude are displayed, and a new selection automatically downloads a new forecast.
- Crane wind limit: labeled number input in miles per hour (mph), default 30 mph, valid range 10-60 mph.
- Concrete minimum temperature: labeled number input in degrees Fahrenheit (°F), default 40 °F, valid range 20-60 °F.
- Roofing precipitation threshold: labeled number input in percent (%), default 30%, valid range 0-100%.
- Working hours: fixed at 7:00 AM-5:00 PM in the jobsite's local timezone for the initial version. Custom Working Hours adds whole-hour start and end inputs in the jobsite's local timezone, matching the hourly forecast resolution. Require the start to be earlier than the end; overnight periods are not supported.
- Forecast period: fixed at the next 7 days. The forecast is downloaded automatically from Open-Meteo and limited to working hours for daily ratings.

## Calculations
- For the initial version, evaluate hourly weather only from 7:00 AM through 4:59 PM in the jobsite's local timezone. After Custom Working Hours is implemented, use the user's selected start time through 1 minute before the selected end time.
- Assign each hourly result a GO, CAUTION, or NO-GO rating, then use the worst hourly rating for that day's activity rating. NO-GO overrides CAUTION, and CAUTION overrides GO.

### Crane lifts
- These thresholds are simplified planning assumptions, not universal safety requirements or a replacement for the crane manufacturer's wind limits.
- GO: sustained wind speed and gust speed are both below 90% of the configured crane wind limit.
- CAUTION: sustained wind speed or gust speed reaches 90% of the limit but remains below the limit.
- NO-GO: sustained wind speed or gust speed reaches or exceeds the configured crane wind limit.
- For example, with the default limit of 30 mph, GO is below 27 mph, CAUTION is from 27 mph through below 30 mph, and NO-GO is 30 mph or above.

### Concrete pours
- These thresholds are simplified planning assumptions, not universal safety requirements or a replacement for project specifications, concrete mix requirements, or a qualified concrete plan.
- Let M equal the user's configured concrete minimum temperature in degrees Fahrenheit (°F).
- GO: temperature is above M + 5°F.
- CAUTION: temperature is from M°F through M + 5°F, inclusive.
- NO-GO: temperature is below M°F.
- With the default minimum of 40°F, GO is above 45°F, CAUTION is 40-45°F inclusive, and NO-GO is below 40°F.

### Roofing
- These thresholds are simplified planning assumptions, not universal safety requirements or a replacement for manufacturer instructions, project specifications, or applicable roofing procedures.
- Let P equal the user's configured roofing precipitation threshold in percent (%).
- GO: precipitation probability is below 50% of P.
- CAUTION: precipitation probability is from 50% of P through P, inclusive.
- NO-GO: precipitation probability is above P.
- With the default threshold of 30%, GO is below 15%, CAUTION is 15-30% inclusive, and NO-GO is above 30%.

### Missing weather data
- Missing required hourly data for an activity initially makes that activity's hourly result CAUTION.
- A known hourly NO-GO result for the same activity overrides missing-data CAUTION.
- Missing location or forecast data prevents meaningful activity ratings and must be shown as unavailable rather than GO.
- Display a warning whenever missing hourly data causes a CAUTION or prevents a rating.

### References
- OSHA crane and derrick standard, 29 CFR 1926.1431: [OSHA - 1926.1431](https://www.osha.gov/laws-regs/regulations/standardnumber/1926/1926.1431)
- ACI cold-weather concreting guidance: [ACI-306R, Guide to Cold Weather Concreting](https://www.concrete.org/publications/internationalconcreteabstractsportal.aspx)
- NRCA roofing weather and installation guidance: [NRCA Roofing Guidelines](https://nrca.net/roofing-guidelines) and [NRCA Technical Library](https://nrca.net/roofingguidelines/library)

## Outputs
- Interactive map showing the selected jobsite marker, latitude and longitude, local timezone, and a loading status while the forecast is retrieved.
- A professional, mobile-friendly seven-day calendar showing the date and a GO, CAUTION, or NO-GO rating for crane lifts, concrete pours, and roofing.
- Rating cards or cells that use both color and text labels: green for GO, yellow for CAUTION, and red for NO-GO.
- Working hours displayed for each day in the jobsite's local time; show the fixed 7:00 AM-5:00 PM in the initial version and the selected hours after Custom Working Hours is implemented.
- Selecting a day expands a detail panel below the calendar for that day.
- Expanded details show weather values with units, the highest-risk hour for each activity, and a short explanation of why that rating was assigned.
- Crane details show sustained wind and gusts in mph; concrete details show temperature in °F; roofing details show precipitation probability in %.
- Missing required hourly data is clearly identified with a CAUTION warning unless a known hourly result establishes NO-GO. Missing location or forecast data is shown as unavailable rather than GO.
- Loading, map, forecast-download, invalid-location, and invalid-setting states use clear, readable error messages and do not imply that a rating is safe or valid.
- A visible disclaimer states that the ratings are simplified planning guidance, not safety guarantees or substitutes for manufacturer limits, project specifications, or professional judgment.

## Look and Feel
- Use a clean, professional dashboard with a header and a collapsible settings panel for the weather thresholds. Add working-hour controls to the panel when Custom Working Hours is implemented.
- On the initial screen, show the default settings and a clear prompt to select a jobsite on the interactive map. Show the seven-day calendar after a jobsite is selected and its forecast is available.
- Place the interactive map above the seven-day calendar.
- Use a light neutral background, dark slate text, and subtle construction-orange accents.
- Show GO, CAUTION, and NO-GO with green, yellow, and red styling, text labels, and icons so status is not communicated by color alone.
- Let users select a calendar day to expand its weather details inline below the calendar.
- On phones, stack the header, settings, map, calendar, and expanded details vertically. Use touch-friendly controls and keep text and ratings readable at narrow widths.
- Keep the design and interactions simple enough for a single-file student web app.

## Features
The following two extra features are implemented separately, only after the required app features have been built and validated. Implement Custom Working Hours first, followed by the Printable Jobsite Weather Report.

### Custom Working Hours
- This feature comes from the assignment's suggested ideas.
- Allow users to change the workday start and end times from the fixed initial hours of 7:00 AM-5:00 PM in the jobsite's local timezone.
- Accept same-day whole-hour values only, require the start to be earlier than the end, include the start hour, and exclude the end hour.
- Automatically recalculate daily weather ratings using the selected hours.

### Printable Jobsite Weather Report
- This is an original feature.
- Add a Print Report button that generates a printer-friendly seven-day summary.
- Include the jobsite coordinates, forecast dates, activity ratings, weather explanations, and safety disclaimer.
- Use the browser's built-in print functionality.

## Validation
### Illustrative crane calculation
- This example demonstrates the rule only; these are not actual forecast readings or app results.
- Configured crane wind limit = 30 mph; sustained wind = 22 mph; gust = 28 mph.
- 90% of the 30 mph limit is 27 mph (30 x 0.90 = 27).
- The sustained wind is below 27 mph, but the gust is at least 27 mph and below 30 mph. Expected hourly rating: CAUTION.
- The gust is 28 / 30 x 100 = 93.3% of the limit. The expected daily rating is CAUTION if no other working hour is NO-GO or missing required data.

### Real-data validation after the app is built
- Select the Denver, Colorado test location at latitude 39.7392 and longitude -104.9903.
- Use the latest day in the seven-day forecast with complete hourly data. Record the forecast retrieval date and time, selected date, location, jobsite timezone, and units.
- Record the raw Open-Meteo hourly temperature (°F), sustained wind speed (mph), wind gust (mph), and precipitation probability (%) for each hour from 7:00 AM through 4:00 PM in Denver local time.
- By hand, assign each hour's activity rating using the rules in Calculations: crane wind and gust thresholds, the configured concrete minimum temperature and its 5°F caution band, and the configured roofing precipitation threshold and its 50% caution boundary. Missing required hourly data is CAUTION unless a known hour establishes NO-GO.
- Determine each daily activity rating by taking the worst hourly rating, then compare the hand-calculated crane, concrete, and roofing ratings with the app's daily results. Record any mismatch and the hourly values that explain it.
- Retrieve the National Weather Service hourly forecast for the same location and date. Compare matching hourly temperature, wind speed, and precipitation probability values with the Open-Meteo values, using consistent local timestamps and units.
- Record the forecast values and differences for the matching hours. Forecasts from the two services are not required to agree exactly; this comparison documents differences and is not a pass/fail test of either provider.

#### Denver validation run: 2026-11-28
- Requested location: Denver, Colorado (39.7392, -104.9903); timezone: America/Denver. The Open-Meteo request was retrieved on 2026-11-22 at 4:55:19.027 PM (UTC-07:00). The response reported coordinates 39.746895, -104.987076.
- The latest complete date in the seven-day forecast was Saturday, November 28, 2026. All ten working-hour timestamps and all four requested weather values were present.
- The exact captured hourly data used for hand calculations and the app check:

| Local time | Temperature (°F) | Sustained wind (mph) | Wind gust (mph) | Precipitation probability (%) |
|---|---:|---:|---:|---:|
| 7:00 AM | 45.3 | 1.7 | 13.4 | 7 |
| 8:00 AM | 44.9 | 4.3 | 12.3 | 7 |
| 9:00 AM | 43.6 | 6.2 | 10.7 | 7 |
| 10:00 AM | 41.9 | 8.0 | 8.7 | 7 |
| 11:00 AM | 40.8 | 8.7 | 7.2 | 7 |
| 12:00 PM | 40.5 | 7.9 | 5.8 | 5 |
| 1:00 PM | 40.7 | 6.0 | 4.5 | 5 |
| 2:00 PM | 40.9 | 5.4 | 4.3 | 5 |
| 3:00 PM | 41.4 | 5.7 | 5.4 | 5 |
| 4:00 PM | 42.0 | 6.1 | 7.4 | 5 |

- Default thresholds used: crane wind limit 30 mph (90% caution boundary: 27 mph); concrete minimum 40°F (caution band: 40-45°F inclusive); roofing precipitation threshold 30% (caution band: 15-30% inclusive).
- Hand calculations:
  - **Crane lifts:** Maximum sustained wind was 8.7 mph and maximum gust was 13.4 mph. Both are below the 27 mph caution boundary, so the expected daily rating is **GO**.
  - **Concrete pours:** Minimum temperature was 40.5°F. This is within the 40-45°F caution band, so the expected daily rating is **CAUTION**.
  - **Roofing:** Maximum precipitation probability was 7%. This is below the 15% caution boundary, so the expected daily rating is **GO**.
- App check: Loaded these exact ten saved records as the forecast response fixture for the November 28 test date; no new forecast was downloaded for the calculation check. The app displayed Crane **GO** (highest-risk hour 7:00 AM), Concrete **CAUTION** (highest-risk hour 12:00 PM), and Roofing **GO** (highest-risk hour 7:00 AM). The app's hourly weather values matched the table above.
- Hand-calculated and app results match for all three activities: **Yes**.

##### NWS forecast comparison
- NWS hourly forecast retrieved on 2026-11-22 at 4:59:02.519 PM (UTC-07:00) from `https://api.weather.gov/gridpoints/BOU/63,62/forecast/hourly`. The NWS point lookup for 39.7392, -104.9903 resolves to grid BOU/63,62 and timezone America/Denver.
- All ten matching November 28 hourly periods from 7:00 AM through 4:00 PM were available, with local timestamps carrying the -07:00 offset. NWS temperature values are in °F, wind speeds in mph, and precipitation probabilities in percent.
- Absolute differences are calculated as `|Open-Meteo value - NWS value|`. Precipitation differences are percentage points.

| Local time | Open-Meteo temp (°F) | NWS temp (°F) | Abs. diff (°F) | Open-Meteo wind (mph) | NWS wind (mph) | Abs. diff (mph) | Open-Meteo precip (%) | NWS precip (%) | Abs. diff (percentage points) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 7:00 AM | 45.3 | 39 | 6.3 | 1.7 | 5 | 3.3 | 7 | 3 | 4 |
| 8:00 AM | 44.9 | 41 | 3.9 | 4.3 | 5 | 0.7 | 7 | 3 | 4 |
| 9:00 AM | 43.6 | 46 | 2.4 | 6.2 | 5 | 1.2 | 7 | 3 | 4 |
| 10:00 AM | 41.9 | 51 | 9.1 | 8.0 | 5 | 3.0 | 7 | 3 | 4 |
| 11:00 AM | 40.8 | 56 | 15.2 | 8.7 | 5 | 3.7 | 7 | 3 | 4 |
| 12:00 PM | 40.5 | 59 | 18.5 | 7.9 | 5 | 2.9 | 5 | 3 | 2 |
| 1:00 PM | 40.7 | 61 | 20.3 | 6.0 | 5 | 1.0 | 5 | 3 | 2 |
| 2:00 PM | 40.9 | 62 | 21.1 | 5.4 | 5 | 0.4 | 5 | 3 | 2 |
| 3:00 PM | 41.4 | 61 | 19.6 | 5.7 | 5 | 0.7 | 5 | 3 | 2 |
| 4:00 PM | 42.0 | 59 | 17.0 | 6.1 | 3 | 3.1 | 5 | 3 | 2 |

- The forecasts differ because the providers can use different models, grid resolutions and terrain representations, data assimilation, update cycles, and forecaster adjustments. This comparison records the differences; exact agreement is not expected.

## Out of Scope
- The planned Custom Working Hours and Printable Jobsite Weather Report features remain in scope and are not excluded below.
- No user accounts or login.
- No multiple saved jobsites or persistent user profiles.
- No paid weather services.
- No equipment scheduling or employee management.
- No weather alerts, notifications, or historical forecasts.
- No National Weather Service integration within the app; NWS is used only for validation.
- No address search or geocoding; jobsite selection is by clicking the map.
- No native mobile apps or offline operation.
- Weather ratings are planning guidance, not safety guarantees.

## Build stages
Build and validate the stages in order. Complete and validate all required app features before starting either extra feature. Keep the app in one `index.html` file suitable for GitHub Pages, test each stage before proceeding, and commit each completed stage.

### Stage 1: Creating the visual mockup
- **Build:** Create the page structure and responsive styling in `index.html`, with a header, collapsible threshold settings, map area, seven-day calendar, selected-day detail panel, loading/error states, and disclaimer. Use representative static content and a map placeholder; do not build forecast calculations yet.
- **Check:** Verify the initial jobsite-selection prompt, desktop hierarchy, mobile vertical layout, readable labels, status colors/icons, and touch-friendly controls.
- **Builds on:** Establishes the layout and interaction pattern for all later stages.
- Commit the completed stage.

### Stage 2: Connecting jobsite selection and forecast data
- **Build:** Add interactive map selection, coordinate display, jobsite timezone, threshold controls, and Open-Meteo hourly forecast retrieval. Keep working hours fixed at 7:00 AM-5:00 PM local time.
- **Check:** Verify that selecting or changing a map point refreshes the forecast; check units and local timestamps; inspect loading, failed-request, invalid-location, and incomplete-response states.
- **Builds on:** Replaces the mockup's map and sample weather with real location and forecast data.
- Commit the completed stage.

### Stage 3: Calculating ratings and displaying the forecast
- **Build:** Apply the documented hourly rules, missing-data handling, and worst-hour daily aggregation. Populate the seven-day activity calendar and expandable detail panel with weather values and explanations.
- **Check:** Hand-check boundary cases for each activity, including thresholds, working-hour inclusion, worst-hour precedence, missing data, and unavailable forecasts. Verify displayed values have units and labels.
- **Builds on:** Adds the primary planning workflow to the map and forecast connection.
- Commit the completed stage.

### Stage 4: Validating and publishing the required app
- **Build:** Complete required-feature testing and perform the documented real-data validation for Denver: capture Open-Meteo hourly values for 7:00 AM-4:00 PM local time, calculate ratings by hand, compare with app results, and compare matching hourly temperature, wind, and precipitation forecasts with NWS.
- **Check:** Record forecast differences without requiring exact agreement. Test the responsive layout and errors, publish the required single-file app to GitHub Pages, and confirm the deployed page loads, map/forecast work, and ratings match the hand calculations.
- **Builds on:** Verifies the complete required app before extras; do not start either extra feature until this stage passes.
- Commit the completed stage.

### Stage 5: Adding Custom Working Hours
- **Build:** As the first extra feature, add whole-hour start/end controls defaulting to 7:00 AM-5:00 PM in the jobsite's local timezone. Require valid same-day periods with the start before the end, and recalculate daily ratings when they change.
- **Check:** Verify valid and invalid time ranges, inclusion of the selected start hour and exclusion of the end hour, recalculated day ratings/details, and that restoring the defaults reproduces the required app's ratings.
- **Builds on:** Extends the validated fixed-hours calculation without changing the earlier required workflow.
- Commit the completed stage.

### Stage 6: Adding the Printable Jobsite Weather Report
- **Build:** As a separate original extra feature, add a Print Report button and a printer-friendly seven-day report using the browser's built-in print functionality. Include coordinates, forecast dates, ratings, explanations, and safety disclaimer.
- **Check:** Inspect print preview and printed output for completeness, legibility, page breaks, and absence of interactive-only controls. Verify the app still works on GitHub Pages as a single `index.html`.
- **Builds on:** Adds the report after the required app and Custom Working Hours are complete.
- Commit the completed stage.

### Implementation notes
- Avoid a build system or server-side dependencies.
- Keep NWS as a validation comparison only, not an in-app forecast integration.
- Thresholds remain simplified planning assumptions and must not be presented as safety guarantees.
