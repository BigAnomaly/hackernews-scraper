[Hackernews Scraper](https://apify.com/makework36/hackernews-scraper?fpr=data)

# Hacker News Scraper

Scrapes stories, jobs, and comments from Hacker News using the official Firebase API. Supports all story categories with optional comment fetching and score filtering.

## What data does it extract?

| Field | Description |
| --- | --- |
| `id` | Hacker News item ID |
| `title` | Story title |
| `url` | External link (null for text-only posts like Ask HN) |
| `score` | Number of upvotes |
| `author` | Username of the submitter |
| `time` | Unix timestamp |
| `timeISO` | ISO 8601 formatted date |
| `commentCount` | Total number of comments on the story |
| `type` | Item type: `story`, `job`, or `poll` |
| `text` | Body HTML for Ask HN, Show HN, and job posts |
| `domain` | Domain extracted from the URL (e.g. `github.com`) |
| `hnUrl` | Direct link to the HN discussion page |
| `comments` | Array of top-level comments (when `includeComments` is enabled) |

## Use cases

- **Tech trend tracking** -- Monitor which topics, tools, and companies are trending among developers.
- **Content curation** -- Pull top stories for newsletters or aggregator sites.
- **Sentiment analysis** -- Collect comments on specific topics to gauge developer opinion.
- **Job board aggregation** -- Scrape HN job postings for a tech job feed.
- **Competitive intelligence** -- Track when your company or product gets discussed on HN.

## How to use

Get the current top 30 stories:

```
{
    "storyType": "top",
    "maxResults": 30
}
```

Ask HN posts with at least 100 points, including comments:

```
{
    "storyType": "ask",
    "maxResults": 20,
    "minScore": 100,
    "includeComments": true
}
```

Latest job postings:

```
{
    "storyType": "job",
    "maxResults": 50
}
```

## Input parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `storyType` | string | `top` | Category to scrape: `top`, `new`, `best`, `ask`, `show`, `job` |
| `maxResults` | integer | `50` | Number of stories to return (1-500) |
| `includeComments` | boolean | `false` | Fetch top-level comments for each story. Increases run time. |
| `minScore` | integer | — | Only return stories with at least this many points |

## Output example

```
{
    "id": 39521347,
    "title": "Show HN: I built a SQL playground that runs in the browser",
    "url": "https://github.com/nicholasgasior/sql-playground",
    "score": 287,
    "author": "ngasior",
    "time": 1711324800,
    "timeISO": "2026-03-25T04:00:00.000Z",
    "commentCount": 94,
    "type": "story",
    "text": null,
    "domain": "github.com",
    "hnUrl": "https://news.ycombinator.com/item?id=39521347"
}
```

## Performance & cost

- Fetches items in parallel (10 concurrent requests) for fast execution.
- 50 stories without comments: ~5 seconds. With comments: 30-60 seconds depending on discussion size.
- Costs under $0.01 per run on the Apify platform for most configurations.

## FAQ

**Why does enabling comments make it so much slower?**
Each story's comments require individual API calls. A story with 200 comments means 200 extra HTTP requests. The actor only fetches top-level comments to keep it manageable.

**What's the difference between "top" and "best"?**
"Top" shows the current front page ranking. "Best" shows the highest-voted stories across a longer timeframe -- it's HN's all-time best, roughly.

**Can I search for specific keywords?**
Not directly. HN's Firebase API doesn't support full-text search. Use `storyType: "top"` or `"new"` and filter the results downstream.

**Is there a rate limit?**
The HN Firebase API is public with no strict rate limit, but the actor uses 10 concurrent requests with retries to be respectful.