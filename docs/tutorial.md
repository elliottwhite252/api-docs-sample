# Get your first forecast

In this tutorial, you'll find a city's coordinates and then get its current temperature and a three-day forecast. You'll make two requests, read the responses, and see how the two endpoints work together.

**Time:** about 10 minutes
**You'll need:** a terminal with `curl`. No account or API key.

## Step 1: Find the city's coordinates

The forecast endpoint needs a latitude and longitude, not a city name. Use the geocoding endpoint to look them up:

```bash
curl "https://geocoding-api.open-meteo.com/v1/search?name=Tokyo&count=1"
```

`count=1` asks for only the best match. The response looks like this:

```json
{
  "results": [
    {
      "id": 1850147,
      "name": "Tokyo",
      "latitude": 35.6895,
      "longitude": 139.69171,
      "elevation": 44.0,
      "feature_code": "PPLC",
      "country_code": "JP",
      "admin1_id": 1850144,
      "timezone": "Asia/Tokyo",
      "population": 9733276,
      "country_id": 1861060,
      "country": "Japan",
      "admin1": "Tokyo"
    }
  ],
  "generationtime_ms": 0.71
}
```

You need three values from this result:

- `latitude`: `35.6895`
- `longitude`: `139.69171`
- `timezone`: `Asia/Tokyo`

## Step 2: Request the forecast

Pass those values to the forecast endpoint. Ask for the current temperature and a daily high and low:

```bash
curl "https://api.open-meteo.com/v1/forecast?latitude=35.6895&longitude=139.69171&current=temperature_2m&daily=temperature_2m_max,temperature_2m_min&timezone=Asia/Tokyo&forecast_days=3"
```

Here's what each parameter does:

| Parameter | Value | Why |
| --- | --- | --- |
| `latitude`, `longitude` | From step 1 | Where to forecast. |
| `current` | `temperature_2m` | The temperature right now, measured at a height of 2 meters. |
| `daily` | `temperature_2m_max,temperature_2m_min` | Each day's high and low. |
| `timezone` | `Asia/Tokyo` | Makes each day run from midnight to midnight in Tokyo, not GMT. |
| `forecast_days` | `3` | Today plus two more days. The default is 7. |

## Step 3: Read the response

The response looks like this. The values in yours depend on the current weather.

```json
{
  "latitude": 35.7,
  "longitude": 139.6875,
  "timezone": "Asia/Tokyo",
  "current_units": { "time": "iso8601", "interval": "seconds", "temperature_2m": "°C" },
  "current": { "time": "2026-11-20T13:00", "interval": 900, "temperature_2m": 14.2 },
  "daily_units": { "time": "iso8601", "temperature_2m_max": "°C", "temperature_2m_min": "°C" },
  "daily": {
    "time": ["2026-11-20", "2026-11-21", "2026-11-22"],
    "temperature_2m_max": [15.8, 17.1, 16.4],
    "temperature_2m_min": [8.4, 9.0, 10.2]
  }
}
```

Some fields are left out here to keep it short. Three things to notice:

1. **The coordinates moved slightly.** The API uses the nearest point on its forecast grid, so `latitude` and `longitude` can differ a little from what you sent. That's expected.
2. **Units come separately.** `current_units` and `daily_units` tell you each value's unit. Temperatures are in °C unless you ask for Fahrenheit.
3. **Daily data is a set of matching lists.** The first item in each list belongs to the first date. On 20 November, the high is 15.8 °C and the low is 8.4 °C.

That third point is the key to reading every hourly and daily response. [How responses are structured](concepts/response-structure.md) explains it in more detail.

## What you've done

You turned a city name into coordinates, requested a forecast, and read the current temperature and daily highs and lows.

## Next steps

- [Get a daily forecast](how-to/daily-forecast.md) with rain chance and conditions
- [Change units](how-to/change-units.md) to Fahrenheit, mph, or inches
- [Handle errors](how-to/handle-errors.md) before you ship
