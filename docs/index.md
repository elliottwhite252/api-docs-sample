# Open-Meteo API guide

Open-Meteo is a free weather API. You send it a location and the weather data you want, and it returns a forecast as JSON. There's no API key and no sign-up for non-commercial use.

This guide covers the two endpoints most apps need:

- **Forecast** (`/v1/forecast`): current conditions, hourly forecasts, and daily forecasts for a latitude and longitude.
- **Geocoding** (`/v1/search`): find the latitude and longitude of a place by name.

!!! info "Unofficial guide"
    This is an independent documentation sample. It isn't affiliated with Open-Meteo. For the complete list of parameters and variables, see the [official documentation](https://open-meteo.com/en/docs).

## Where to start

| If you want to… | Read |
| --- | --- |
| Make your first request | [Get your first forecast](tutorial.md) |
| Show a week of weather in local time | [Get a daily forecast](how-to/daily-forecast.md) |
| Use Fahrenheit, mph, or inches | [Change units](how-to/change-units.md) |
| Handle bad input and failed searches | [Handle errors](how-to/handle-errors.md) |
| Understand the response format | [How responses are structured](concepts/response-structure.md) |
| Look up every parameter and field | [API reference](reference/api.md) |
| Turn a weather code into words | [Weather codes](reference/weather-codes.md) |

## Before you build

- **Usage limits.** The free tier allows fewer than 10,000 calls per day, 5,000 per hour, and 600 per minute, for non-commercial use only. Commercial use needs a paid plan.
- **Attribution.** Open-Meteo data is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). If your app shows the data, credit Open-Meteo.
- **No uptime guarantee** on the free tier. Cache responses where you can.
