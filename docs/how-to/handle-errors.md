# Handle errors

Use this guide to handle the three problems you're most likely to hit: an invalid request, a place search with no matches, and a rate limit.

## Invalid requests

If a parameter is missing or invalid, the API returns HTTP status `400` and a JSON body like this:

```json
{
  "error": true,
  "reason": "Cannot initialize WeatherVariable from invalid String value temperature for key hourly"
}
```

`reason` says what went wrong. Common causes:

- **A misspelled variable name**, such as `temperature` instead of `temperature_2m`.
- **A value out of range**, such as `forecast_days=20`. The maximum is 16.
- **Missing coordinates.** `latitude` and `longitude` are required.

Check the status before you read the data:

```javascript
const res = await fetch(url);
const body = await res.json();

if (!res.ok || body.error) {
  throw new Error(`Forecast request failed: ${body.reason ?? res.status}`);
}
```

`reason` is written for developers. Log it, but show users a simpler message, such as "Couldn't load the forecast. Try again."

## Place searches with no matches

A search that finds nothing isn't an error. The status is still `200`, but the response may not include a `results` list at all. Check for it before reading the first result:

```javascript
const { results } = await res.json();

if (!results || results.length === 0) {
  showMessage("No places found. Check the spelling, or try a nearby city.");
  return;
}
```

Searches of fewer than two characters always return nothing, so don't send a request until the user has typed at least two.

## Rate limits

The free tier allows fewer than 10,000 calls per day, 5,000 per hour, and 600 per minute. To stay well under them:

- **Cache forecasts.** Forecasts change slowly, so reusing a response for 15 to 60 minutes rarely changes what users see.
- **Debounce search.** Wait until the user stops typing for about 300 milliseconds before you call the geocoding endpoint.
- **Combine variables.** Request everything you need in one call instead of one call per variable.

## Related

- [API reference](../reference/api.md)
