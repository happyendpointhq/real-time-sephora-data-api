# Sephora API

Real-time access to Sephora product data: 8,500+ products with pricing, reviews
and ratings, brand and category directories, store locations, and per-store
availability. Clean JSON over a normal REST API, so there is no scraping, no
proxy rotation, and no HTML parsing to maintain.

Coverage spans the US, Canada, and France.

Built and maintained by [Happy Endpoint](https://happyendpoint.com).

- Subscribe on RapidAPI: https://rapidapi.com/happyendpoint/api/real-time-sephora-api
- Product page: https://happyendpoint.com/library/sephora-api
- Hosted docs: https://happyendpointhq.github.io/sephora-api/

---

## What you get

- Product search by keyword, category, or brand
- Full product records with specifications and real-time pricing
- Customer reviews and ratings
- Brand and category directories
- Store locations
- Per-store product availability
- Autocomplete for product name suggestions

---

## Getting started

### 1. Get an API key

Subscribe on RapidAPI. There is a free tier:
https://rapidapi.com/happyendpoint/api/real-time-sephora-api

### 2. Make a request

```bash
curl "https://real-time-sephora-api.p.rapidapi.com/search-by-keyword?query=moisturizer" \
  -H "x-rapidapi-host: real-time-sephora-api.p.rapidapi.com" \
  -H "x-rapidapi-key: YOUR_RAPIDAPI_KEY"
```

### Python

```python
import os

import requests

HOST = "real-time-sephora-api.p.rapidapi.com"
HEADERS = {
    "x-rapidapi-host": HOST,
    "x-rapidapi-key": os.environ["RAPIDAPI_KEY"],
}


def get(path, **params):
    r = requests.get(
        f"https://{HOST}{path}",
        params={k: v for k, v in params.items() if v is not None},
        headers=HEADERS,
        timeout=30,
    )
    r.raise_for_status()
    return r.json()


results = get("/search-by-keyword", query="moisturizer")
brands = get("/brands-list")
```

### JavaScript

```javascript
const HOST = 'real-time-sephora-api.p.rapidapi.com';

async function get(path, params = {}) {
  const url = new URL(`https://${HOST}${path}`);
  for (const [k, v] of Object.entries(params)) {
    if (v != null) url.searchParams.set(k, v);
  }

  const res = await fetch(url, {
    headers: {
      'x-rapidapi-host': HOST,
      'x-rapidapi-key': process.env.RAPIDAPI_KEY,
    },
  });
  if (!res.ok) throw new Error(`Sephora API ${res.status}`);
  return res.json();
}

const results = await get('/search-by-keyword', { query: 'moisturizer' });
```

---

## Endpoints

Base URL: `https://real-time-sephora-api.p.rapidapi.com`

### Search and discovery

| Endpoint | Returns |
|---|---|
| `GET /auto-complete` | Product name suggestions for a partial query |
| `GET /search-by-keyword` | Products matching a search term |
| `GET /search-by-category` | Products within a category |
| `GET /search-by-brand` | Products from a brand |

### Product data

| Endpoint | Returns |
|---|---|
| `GET /product-details` | Full record for a single product |
| `GET /product-reviews` | Customer reviews and ratings |
| `GET /product-availability` | Stock availability, including per store |

### Reference data

| Endpoint | Returns |
|---|---|
| `GET /brands-list` | All brands |
| `GET /categories-list` | Root product categories |
| `GET /category-data` | Detail for a single category |
| `GET /store-list` | Store locations |
| `GET /status` | Service health |

---

## Using this API from Claude, Cursor, or another MCP client

RapidAPI hosts an MCP server, so you can query this API from an AI assistant
without writing any code:

```json
{
  "mcpServers": {
    "Sephora": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.rapidapi.com",
        "--header",
        "x-api-host: real-time-sephora-api.p.rapidapi.com",
        "--header",
        "x-api-key: YOUR_RAPIDAPI_KEY"
      ]
    }
  }
}
```

| Client | Config path |
|---|---|
| Claude Desktop (macOS) | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Claude Desktop (Windows) | `%APPDATA%\Claude\claude_desktop_config.json` |
| Cursor | `~/.cursor/mcp.json` |
| Claude Code | `.mcp.json` in your project root |

---

## What people build with this

- Price tracking and competitor monitoring for beauty retail
- Product comparison and review aggregation sites
- Affiliate and shopping assistant tools
- Assortment and catalogue analysis
- Availability monitoring across stores
- Sentiment analysis on review text
- Recommendation engines and beauty tech products

---

## FAQ

### Does Sephora have an official public API?

No. Sephora does not publish a public product API. This API is built and
maintained by Happy Endpoint to provide that access.

### Is there a free tier?

Yes. RapidAPI hosts a free plan with a monthly request quota, enough to prototype
against.

### How is this different from scraping?

Scraping a retailer means maintaining selectors that break on every redesign,
rotating proxies, handling bot challenges, and accepting that it may breach the
site's terms. This is a REST API returning JSON with a stable contract.

### Which countries are covered?

The US, Canada, and France.

### Can I check whether a product is in stock at a specific store?

Yes. `/store-list` returns store locations and `/product-availability` reports
availability, including per store.

### Can I get the full catalogue as a file rather than calling the API?

Yes. Happy Endpoint sells a Sephora US products dataset of 8,000+ products as a
one-off file. See [happyendpoint.com/datasets](https://happyendpoint.com/datasets)
or email happyendpointhq@gmail.com.

### Do you cover other retailers?

Yes. IKEA, Tesco, Kohl's, and H&M, among others. See
[happyendpoint.com/library](https://happyendpoint.com/library).

---

## Related repos

- [ikea-api](https://github.com/happyendpointhq/ikea-api) - IKEA product, category, and store data
- [priceline-api](https://github.com/happyendpointhq/priceline-api) - hotel, flight, and car rental data
- [bayut-api-python-examples](https://github.com/happyendpointhq/bayut-api-python-examples) - runnable Python patterns that transfer to this API
- [bayut-api-postman-collection](https://github.com/happyendpointhq/bayut-api-postman-collection) - our Postman collection format

---

## Disclaimer

Happy Endpoint is an independent provider. This project is **not affiliated
with, endorsed by, sponsored by, or connected to** any of the websites,
platforms, retailers, or marketplaces referenced here or reachable through the
underlying APIs.

All product names, brands, trademarks, and registered trademarks are the
property of their respective owners. Any reference to them is descriptive only,
to identify the subject matter of the data, and does not imply any association
or endorsement.

Users are responsible for ensuring their use of any data complies with
applicable laws and the terms of service of the relevant source.

---

## About Happy Endpoint

[Happy Endpoint](https://happyendpoint.com) builds and maintains real-time data
APIs for property portals, retailers, and marketplaces. All APIs are available on
RapidAPI with a free tier.

- Catalogue: [happyendpoint.com/library](https://happyendpoint.com/library)
- Datasets: [happyendpoint.com/datasets](https://happyendpoint.com/datasets)
- Documentation: [docs.happyendpoint.com](https://docs.happyendpoint.com)
- Contact: happyendpointhq@gmail.com

## Licence

MIT. See [LICENSE](LICENSE).
