
# Jobsite Weather Planner

## Purpose
Create a web app that helps construction managers plan work based on the weather. The app will show which days are good for crane lifts, concrete pours, and roofing.

## Inputs
- Jobsite location: selected by clicking a map.
- Crane wind limit (mph): number input, default 30 mph, range 10-60 mph.
- Weather forecast: downloaded automatically from Open-Meteo.
- Forecast period: next 7 days.

## Calculations
- Compare hourly wind speed and gusts to the crane wind limit.
- Compare temperatures to cold-weather concrete limits.
- Compare precipitation probability to roofing limits.
- Rate each activity as GO, CAUTION, or NO-GO.
- The thresholds will need to be verified with sources before building.

## Outputs
- Interactive map showing the jobsite location.
- Seven-day weather forecast.
- Calendar showing GO, CAUTION, or NO-GO for each activity.
- Explanation of why each rating was given.

## Look and Feel
- Clean, professional construction management dashboard.
- Map near the top.
- Seven-day calendar below the map.
- Green, yellow, and red activity ratings.
- Easy to use on a phone or computer.

## Validation
Example crane check using a proposed rule:
- Wind limit = 30 mph.
- Forecast gust = 28 mph.
- CAUTION begins at 90% of the limit.
- 28 / 30 x 100 = 93.3%.
- Expected result: CAUTION.

This is an initial hand calculation. The full validation will use actual downloaded forecast data and verified thresholds.

## Out of Scope
- No user accounts or login.
- No paid weather services.
- No equipment scheduling or employee management.
- No guarantee that weather conditions will be safe.
