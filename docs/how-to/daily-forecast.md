# Get a daily forecast

Use this guide to build a seven-day forecast like the ones in weather apps: a high, a low, a chance of rain, and a short description for each day.

## Request

```bash
curl "https://api.open-meteo.com/v1/forecast?latitude=35.6895&longitude=139.69171&daily=weather_code,temperature_2m_max,temperature_2m_min,precipitation_probability_max&timezone=auto"
```

| Daily variable | What it gives you | Unit |
| --- | --- | --- |
| `weather_code` | The day's overall conditions, as a number | WMO code |
| `temperature_2m_max` | The day's high | °C |
| `temperature_2m_min` | The day's low | °C |
| `precipitation_probability_max` | The highest chance of rain or snow during the day | % |

You don't need `forecast_days`, because seven days is the default.

## Always set the time zone

Without `timezone`, days run midnight to midnight in GMT. For a city far from GMT, that shifts every high, low, and rain chance into the wrong day.

Set it in one of two ways:

- **`timezone=auto`** uses the time zone of the coordinates. This is the simplest option.
- **A time zone name**, such as `timezone=Asia/Tokyo`. Use this if you already have it, for example from a [geocoding result](../tutorial.md#step-1-find-the-citys-coordinates).

## Turn the response into rows

Each daily variable is a list in the same order as `daily.time`. Read them together by position:

```javascript
const res = await fetch(url);
const { daily } = await res.json();

const days = daily.time.map((date, i) => ({
  date,
  high: daily.temperature_2m_max[i],
  low: daily.temperature_2m_min[i],
  rainChance: daily.precipitation_probability_max[i],
  code: daily.weather_code[i],
}));
```

`days` is now one object per day, ready to display.

## Show conditions as words

`weather_code` is a number. Convert it to a description, and an icon if you have one, using [Weather codes](../reference/weather-codes.md). For example, `3` means overcast and `61` means light rain.

## Related

- [How responses are structured](../concepts/response-structure.md)
- [Change units](change-units.md)
