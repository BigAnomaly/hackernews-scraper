[Hackernews Scraper](https://apify.com/legend006/hackernews-scraper?fpr=data)

# 🟠 Hacker News Scraper

Scrape **Hacker News** stories, comments, polls, jobs, and Ask/Show HN posts. Search by keyword + date range, pull full HN lists (front page, new, best, ask, show, jobs), or fetch any user's complete activity.

> ⚡ Uses HN's official Algolia + Firebase APIs. No login, no rate-limit nightmares, no scraping HTML.

---

## ✨ What you can do

- 🔎 **Keyword search** with date range, tag filter, min-points threshold, and sort by relevance/date/points
- 📋 **Pull any HN list** — top, new, best, Ask HN, Show HN, jobs
- 👤 **Get any user's full activity** — stories AND comments, by username
- 💬 **Optionally fetch full comment trees** — flattened with parent IDs (great for AI training)

---

## 🚀 Quick start

1. Click **Try for free**
2. Pick mode: `search`, `list`, or `user`
3. Enter targets
4. Click **Start**

---

## 📥 Input examples

### Search for "claude" stories from the last month with 50+ points

```
{
    "mode": "search",
    "searchQueries": ["claude"],
    "tags": "story",
    "sortBy": "points",
    "since": "2026-04-01",
    "minPoints": 50,
    "maxItems": 500,
    "includeComments": true
}
```

### Pull current front page

```
{
    "mode": "list",
    "listType": "topstories",
    "maxItems": 30,
    "includeComments": true,
    "maxCommentsPerStory": 50
}
```

### Get pg's recent activity

```
{
    "mode": "user",
    "users": ["pg", "dang"],
    "maxItems": 100
}
```

---

## 📤 Output (per item)

```
{
    "type": "story",
    "id": 12345678,
    "title": "Show HN: A new way to scrape data",
    "text": null,
    "author": "username",
    "points": 234,
    "numComments": 87,
    "createdAt": "2026-04-15T12:34:56.000Z",
    "url": "https://example.com/article",
    "hnUrl": "https://news.ycombinator.com/item?id=12345678",
    "tags": ["story", "front_page"],
    "comments": [
        {
            "type": "comment",
            "id": 12345679,
            "text": "Great post!",
            "author": "commenter",
            "points": 12,
            "createdAt": "2026-04-15T13:00:00.000Z",
            "parentId": 12345678
        }
    ]
}
```

---

## 🎯 Use cases

| Who | Why |
| --- | --- |
| 🤖 AI / LLM teams | High-signal tech-discussion training data, filterable by topic and quality (points threshold) |
| 📰 Tech journalists | Track what's trending in dev/startup community |
| 🧑‍💻 Engineers | Dataset of "Show HN" launches, open-source releases, new tools |
| 📊 VCs / scouts | Monitor early-stage signals across founders posting on HN |
| 📈 SEO researchers | Track tech keywords surfacing in HN search trends |

---

## ⚙️ Tech notes

- Search uses HN's [Algolia API](https://hn.algolia.com/api) — fast, fielded, supports complex queries
- Lists & item details use HN's [Firebase API](https://github.com/HackerNews/API) — official, real-time
- No auth required, no API key needed, no rate-limit (within reason)
- Comments are fetched recursively from Firebase for accuracy and full trees

---

## ❓ FAQ

**Will I get rate-limited?**
HN is generous — the Algolia API is unmetered for reasonable use. Comment-tree scraping at large scale is slower because each item is a separate Firebase call.

**Are deleted/dead items included?**
No — they're filtered automatically.

**Can I scrape historical data?**
Yes. Use `since` and `until` in search mode to pull any historical date range. HN's archive goes back to 2007.

**Schedule it?**
Yes — set up an Apify Schedule for daily/hourly trend tracking.