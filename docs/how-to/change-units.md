# Change units

By default, Open-Meteo returns metric units. Use this guide to return values in the units your users expect, such as Fahrenheit, miles per hour, and inches.

## Add the unit parameters

```bash
curl "https://api.open-meteo.com/v1/forecast?latitude=40.7128&longitude=-74.006&current=temperature_2m,wind_speed_10m,precipitation&temperature_unit=fahrenheit&wind_speed_unit=mph&precipitation_unit=inch&timezone=auto"
```

| Parameter | Default | Options |
| --- | --- | --- |
| `temperature_unit` | `celsius` | `celsius`, `fahrenheit` |
| `wind_speed_unit` | `kmh` | `kmh`, `ms` (meters per second), `mph`, `kn` (knots) |
| `precipitation_unit` | `mm` | `mm`, `inch` |

Each parameter changes every variable of that type in the response, across `current`, `hourly`, and `daily`.

!!! note
    Snowfall and snow depth have their own units. By default, they're centimeters and meters. Check the `*_units` object rather than assuming.

## Read the unit from the response

Don't hard-code unit labels in your app. Read them from the matching `*_units` object so they always match the data:

```javascript
const { current, current_units } = await res.json();
const label = `${current.temperature_2m}${current_units.temperature_2m}`;
// "48.2°F"
```

## Choose units by locale

A common pattern is to pick units from the user's region. For example, the United States uses Fahrenheit, mph, and inches, while most other countries use Celsius, km/h, and millimeters. Let users change it in settings, because preferences vary.

## Related

- [API reference](../reference/api.md)
