# How responses are structured

Most APIs return a list of objects, one per time step. Open-Meteo does the opposite. It returns one list per variable, and you match them up by position. Once you understand this, every hourly and daily response reads the same way.

## Parallel arrays

Here's an hourly response for three hours, with some fields left out:

```json
{
  "hourly_units": { "time": "iso8601", "temperature_2m": "°C", "precipitation_probability": "%" },
  "hourly": {
    "time": ["2026-11-20T00:00", "2026-11-20T01:00", "2026-11-20T02:00"],
    "temperature_2m": [9.1, 8.7, 8.4],
    "precipitation_probability": [0, 5, 10]
  }
}
```

Read it as a table, where each position is a row:

| Position | `time` | `temperature_2m` | `precipitation_probability` |
| --- | --- | --- | --- |
| 0 | 2026-11-20T00:00 | 9.1 °C | 0% |
| 1 | 2026-11-20T01:00 | 8.7 °C | 5% |
| 2 | 2026-11-20T02:00 | 8.4 °C | 10% |

Every list in `hourly` has the same length. The value at position *n* in any list belongs to the time at position *n* in `time`. `daily` works the same way, with one position per day.

## Why it's designed this way

Repeating field names for every hour adds up fast. A seven-day hourly forecast has 168 time steps, so listing each variable name once instead of 168 times keeps responses much smaller. This format is also easy to load straight into charts and data tools, which expect one column per variable.

The cost is a small step in your code to turn the lists into rows, if your app needs rows. See [Get a daily forecast](../how-to/daily-forecast.md#turn-the-response-into-rows) for an example.

## The blocks in a response

A forecast response contains only the blocks you asked for:

| Block | Present when you request | Shape |
| --- | --- | --- |
| `current` | `current=…` | One value per variable, plus `time` and `interval` |
| `hourly` | `hourly=…` | Parallel arrays, one position per hour |
| `daily` | `daily=…` | Parallel arrays, one position per day |

Each block has a matching `*_units` object, such as `hourly_units`, that gives the unit of every variable in it.

## Times and time zones

All times in the response use the `timezone` you requested, or GMT if you didn't set one. Times have no offset attached, such as `2026-11-20T13:00`. To convert them to another zone, use `utc_offset_seconds` from the response.

If you'd rather work with timestamps, set `timeformat=unixtime`. Times then come back as seconds since January 1, 1970, UTC.

## Coordinates in the response

The `latitude` and `longitude` in the response are the center of the forecast grid cell the API used. They can be slightly different from the ones you sent. Use your original coordinates, not the returned ones, if you need to identify the location later.

## Related

- [API reference](../reference/api.md)
