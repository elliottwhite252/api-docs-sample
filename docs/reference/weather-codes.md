# Weather codes

The `weather_code` variable describes conditions as a number, using codes from the World Meteorological Organization (WMO). Use this table to turn a code into a description for your users.

| Code | Conditions |
| --- | --- |
| 0 | Clear sky |
| 1 | Mainly clear |
| 2 | Partly cloudy |
| 3 | Overcast |
| 45 | Fog |
| 48 | Depositing rime fog |
| 51 | Light drizzle |
| 53 | Moderate drizzle |
| 55 | Dense drizzle |
| 56 | Light freezing drizzle |
| 57 | Dense freezing drizzle |
| 61 | Light rain |
| 63 | Moderate rain |
| 65 | Heavy rain |
| 66 | Light freezing rain |
| 67 | Heavy freezing rain |
| 71 | Light snow |
| 73 | Moderate snow |
| 75 | Heavy snow |
| 77 | Snow grains |
| 80 | Light rain showers |
| 81 | Moderate rain showers |
| 82 | Violent rain showers |
| 85 | Light snow showers |
| 86 | Heavy snow showers |
| 95 | Thunderstorm |
| 96 | Thunderstorm with light hail |
| 97 | Heavy thunderstorm |
| 99 | Thunderstorm with heavy hail |

Codes 96 and 99 appear only from weather models that forecast hail. Other models report 95 or 97 instead.

## Handle unknown codes

Always include a fallback description for codes that aren't in your table. That keeps your app working if a new code ever appears.

```javascript
const WEATHER = { 0: "Clear sky", 1: "Mainly clear", 2: "Partly cloudy", 3: "Overcast" /* … */ };

function describe(code) {
  return WEATHER[code] ?? "Unknown conditions";
}
```
