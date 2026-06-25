[Hackernews Scraper](https://apify.com/andok/hackernews-scraper?fpr=data)

# Hacker News Scraper & Tracker

Track Hacker News discussions for competitive intelligence, developer sentiment, and trending topics in tech. Instead of scraping HTML, this actor queries the official HN Firebase API to pull stories by category — top, new, best, ask, show, or job — with scores, comment counts, and author data. Schedule it daily to build a signal feed for product launches, technology trends, and community buzz.

## Features

- **Six categories** — fetch top, new, best, ask, show, or job stories in a single run
- **Official API** — uses the Hacker News Firebase API for reliable, structured data
- **Rich metadata** — includes score, comment count, author, timestamp, and source domain
- **Domain extraction** — automatically parses the hostname from each story URL
- **Bulk fetching** — retrieve up to 500 stories per run with batched API calls
- **No browser required** — pure API access means fast execution and low resource usage
- **Pay-per-result pricing** — only pay for stories extracted, with built-in charge limits

## Input

| Field | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `category` | `string` | No | `top` | Story category to fetch: `top`, `new`, `best`, `ask`, `show`, or `job` |
| `maxItems` | `integer` | No | `100` | Maximum number of stories to fetch (1-500) |
| `timeoutSeconds` | `integer` | No | `15` | Per-request API timeout in seconds (1-120) |

### Input Example

```
{
  "category": "top",
  "maxItems": 50,
  "timeoutSeconds": 15
}
```

## Output

Each dataset item represents one Hacker News story. Key fields:

- `id` (`number`) — HN story ID
- `title` (`string`) — story headline
- `url` (`string`) — link to the external content (or HN discussion if self-post)
- `domain` (`string`) — hostname of the linked URL (e.g. `github.com`)
- `score` (`number`) — upvote count
- `by` (`string`) — author username
- `time` (`number`) — Unix timestamp of submission
- `descendants` (`number`) — total comment count
- `type` (`string`) — item type (`story`, `job`, etc.)

### Output Example

```
{
  "id": 38945678,
  "title": "Show HN: I built an open-source alternative to Datadog",
  "url": "https://github.com/example/monitoring-tool",
  "domain": "github.com",
  "score": 342,
  "by": "techfounder",
  "time": 1705334400,
  "descendants": 187,
  "type": "story"
}
```

## Pricing

| Event | Cost |
| --- | --- |
| Post Extracted | Pay-per-event (see actor pricing page) |

## Use Cases

- **Competitive intelligence** — monitor when competitors or their products get discussed on HN
- **Developer sentiment** — track how the community reacts to new tools, frameworks, and launches
- **Trend detection** — identify rising technologies by analyzing top and best story patterns over time
- **Content research** — find high-engagement topics for technical blog posts or developer marketing
- **Job market analysis** — scrape the monthly "Who is Hiring?" threads for hiring trends
- **AI agent feeds** — supply structured HN data to LLM pipelines for tech news summarization

## Related Actors

| Actor | What it adds |
| --- | --- |
| [Google News Scraper](https://apify.com/andok/google-news-scraper) | Broaden coverage beyond HN to mainstream news outlets |
| [RSS & Atom Feed Parser](https://apify.com/andok/rss-parser) | Parse the HN RSS feed or any other RSS source for simpler use cases |
| [Reddit Scraper](https://apify.com/andok/reddit-json-scraper) | Track discussions on Reddit for a complementary community signal |