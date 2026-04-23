# Firecrawl Toolkit

> **Unmaintained.** Use [`firecrawl-py`](https://github.com/mendableai/firecrawl/tree/main/apps/python-sdk), Firecrawl's official Python SDK.

I was writing scripts that needed to pull clean content from the web: markdown from product pages, sitemaps for crawl budgeting, full-page screenshots for comparisons. Firecrawl had the right primitives. I wanted a thin Python layer with defaults I liked, built-in retries, param validation, and one import covering crawl / scrape / batch / map. So I built this for myself.

Python wrapper around the Firecrawl REST API.

## Install

```bash
git clone https://github.com/ramonclaudio/firecrawl-toolkit.git
cd firecrawl-toolkit
pip install -r requirements.txt
```

## Configuration

Get a Firecrawl API key at https://www.firecrawl.dev/app/api-keys. Set it via env var or `.env`:

```bash
export FIRECRAWL_API_KEY=your_api_key
```

Or pass `api_key="..."` directly.

## Usage

```python
import firecrawl

# Single URL
firecrawl.scrape(url="https://example.com", formats=["markdown", "html"], onlyMainContent=True)

# Crawl
firecrawl.crawl(url="https://example.com", formats=["markdown", "html"])

# Batch
firecrawl.batch_scrape(urls=["https://example.com", "https://sitemaps.org"], formats=["markdown", "html"])

# Site map
firecrawl.map(url="https://example.com", includeSubdomains=True, limit=1000)
```

## Parameters

| Parameter | Type | Example |
| --- | --- | --- |
| `formats` | list | `["markdown", "html", "rawHtml", "links", "screenshot"]` |
| `onlyMainContent` | bool | `True` |
| `includeTags` | list | `["article", "main"]` |
| `excludeTags` | list | `["nav", "footer"]` |
| `headers` | dict | `{"User-Agent": "Custom"}` |
| `waitFor` | int | `1000` |
| `mobile` | bool | `False` |
| `actions` | list | `[{"type": "click", "selector": "#btn"}]` |
| `location` | dict | `{"country": "US", "languages": ["en-US"]}` |

## Formats

`markdown`, `html`, `rawHtml`, `links`, `extract`, `screenshot`, `screenshot@fullPage`

## Actions

| Action | Parameters |
| --- | --- |
| `wait` | `milliseconds`, `selector` |
| `click` | `selector` |
| `write` | `selector`, `text` |
| `press` | `key` |
| `scroll` | `direction`, `amount` |
| `screenshot` | `fullPage` |
| `scrape` | none |

## Errors

| Error | When |
| --- | --- |
| `ConfigurationError` | Missing or invalid config |
| `ValidationError` | Invalid request params |
| `APIError` | API returned an error |
| `NetworkError` | Connection problems |
| `ResponseError` | Unexpected API response shape |

## License

MIT
