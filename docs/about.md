# About this guide

I wrote this guide as a public API documentation sample. Most of my professional documentation is under NDA, so this shows how I approach API docs using a real, public API.

It isn't affiliated with or endorsed by Open-Meteo. All facts come from Open-Meteo's [official documentation](https://open-meteo.com/en/docs) and [terms](https://open-meteo.com/en/terms). The writing is my own.

## Approach

**Organized by what the reader needs.** The guide follows the [Diátaxis](https://diataxis.fr) framework:

| Type | Page |
| --- | --- |
| Tutorial | [Get your first forecast](tutorial.md) |
| How-to guides | [Get a daily forecast](how-to/daily-forecast.md), [Change units](how-to/change-units.md), [Handle errors](how-to/handle-errors.md) |
| Concept | [How responses are structured](concepts/response-structure.md) |
| Reference | [API reference](reference/api.md), [Weather codes](reference/weather-codes.md) |

**Focused on what trips people up.** Open-Meteo's response format, parallel arrays instead of a list of objects, is the most common source of confusion for new users. It gets its own concept page, and every guide that returns arrays shows how to read them.

**Scoped to what most apps need.** The spec covers two endpoints and their common parameters, not every option. Each page links to the official docs for the full list.

## Tooling

- **OpenAPI 3.1** describes both endpoints. [Spectral](https://github.com/stoplightio/spectral) lints the spec, and [Redoc](https://github.com/Redocly/redoc) renders the reference.
- **[MkDocs](https://www.mkdocs.org) with the Material theme** builds the site.
- **[Vale](https://vale.sh)** checks the prose against the Google developer documentation style guide.
- **GitHub Actions** runs every check on each pull request and publishes the site when changes merge.
- **[llms.txt](llms.txt)** gives AI tools a plain-text map of the guide.

---

*Elliott White · [Portfolio](https://elliottwhite252.github.io/portfolio/) · [GitHub](https://github.com/elliottwhite252)*
