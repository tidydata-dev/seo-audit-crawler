# SEO Audit Tool — Website Audit & SEO Checker — Python, Node.js & cURL examples

Crawl any website and get a **0-100 SEO score for every page**, the **issues ordered by priority with how to fix them**, **broken links**, duplicate titles and descriptions, schema types and a **site summary**. **$4 per 1,000 pages**; pages that don't load are not charged.

Hosted on Apify: **[SEO Audit Tool — Website Audit & SEO Checker](https://apify.com/tidydata/seo-audit-crawler?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/seo-audit-crawler").call(run_input={
    "startUrls": [
        {
            "url": "https://www.python.org"
        }
    ],
    "maxPages": 50,
    "maxDepth": 3,
    "checkBrokenLinks": True,
    "addSummary": True
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['url', 'score', 'issueCount', 'title']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/seo-audit-crawler').call({"startUrls": [{"url": "https://example.com"}], "maxPages": 10});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~seo-audit-crawler/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"startUrls": [{"url": "https://example.com"}], "maxPages": 10}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
