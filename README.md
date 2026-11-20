# Open-Meteo API guide (documentation sample)

An unofficial, task-focused guide to the [Open-Meteo](https://open-meteo.com) weather forecast and geocoding APIs, written as a public API documentation sample.

📖 **[Read the guide](https://elliottwhite252.github.io/api-docs-sample/)**

## What's inside

| Content | Location |
| --- | --- |
| Tutorial, how-to guides, concept, and reference pages | [`docs/`](docs/) |
| OpenAPI 3.1 spec for both endpoints | [`docs/openapi.yaml`](docs/openapi.yaml) |
| Plain-text map for AI tools | [`docs/llms.txt`](docs/llms.txt) |
| CI: Vale, Spectral, MkDocs build, Pages deploy | [`.github/workflows/docs.yml`](.github/workflows/docs.yml) |

## Run it locally

```bash
pip install mkdocs-material
mkdocs serve
```

Then open `http://127.0.0.1:8000`.

To run the checks:

```bash
vale sync && vale docs
npx @stoplight/spectral-cli lint docs/openapi.yaml
```

## Credits

Weather data and API by [Open-Meteo](https://open-meteo.com), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This guide isn't affiliated with Open-Meteo.

Written by [Elliott White](https://elliottwhite252.github.io/portfolio/).
