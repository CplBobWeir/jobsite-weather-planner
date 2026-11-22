
# Jobsite Weather Planner

## Purpose
Create a responsive web dashboard that helps construction managers compare crane lifts, concrete pours, and roofing work across the next seven days at a selected jobsite. The app will display simple weather-based GO, CAUTION, and NO-GO ratings with short explanations, supporting preliminary scheduling decisions rather than guaranteeing that conditions are safe.

## Inputs
- Jobsite location: selected by clicking an interactive map. The selected latitude and longitude are displayed, and a new selection automatically downloads a new forecast.
- Crane wind limit: labeled number input in miles per hour (mph), default 30 mph, valid range 10-60 mph.
- Concrete minimum temperature: labeled number input in degrees Fahrenheit (°F), default 40 °F, valid range 20-60 °F.
- Roofing precipitation threshold: labeled number input in percent (%), default 30%, valid range 0-100%.
- Working hours: fixed at 7:00 AM-5:00 PM in the jobsite's local timezone for the initial version. Editable start and end time inputs are added later as the Custom Working Hours feature.
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
