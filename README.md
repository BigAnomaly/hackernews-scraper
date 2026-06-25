[Hackernews Scraper](https://apify.com/fresh_cliff/hackernews-scraper?fpr=data)

# Hacker News Scraper for Apify

A production-ready Apify actor that scrapes stories from Hacker News front page using Playwright.

## 🚀 Features

- Scrapes Hacker News front page stories
- Extracts comprehensive story data:

- Title and URL
- Points (upvotes)
- Author username
- Number of comments
- Time posted
- Story rank
- Hacker News discussion URL
- Configurable number of stories to scrape
- Option to include/exclude job posts
- Built with Playwright for reliable scraping
- Production-ready for Apify platform

## 📁 Project Structure

```
hackernews-scraper/
├── .actor/
│   ├── actor.json              # Actor metadata and configuration
│   └── dataset_schema.json     # Output data schema
├── apify_actor.py              # Main actor entry point
├── hackernews_scraper.py       # Core scraper implementation
├── Dockerfile                  # Docker configuration for Apify
├── requirements.txt            # Python dependencies
├── INPUT_SCHEMA.json           # Input configuration schema
└── README.md                   # This file
```

## 🔧 Local Testing

### Prerequisites

- Python 3.11+
- pip

### Installation

1. Install dependencies:

```
$pip install -r requirements.txt
```

1. Install Playwright browsers:

```
$playwright install chromium
```

1. Test the scraper locally:

```
$python hackernews_scraper.py
```

## 🌐 Deploy to Apify

### Prerequisites

1. [Create an Apify account](https://console.apify.com/sign-up)
2. Install Apify CLI: `npm install -g apify-cli`
3. Login: `apify login`

### Deployment Steps

1. **Navigate to project directory:**

```
$cd hackernews-scraper
```

1. **Deploy to Apify:**

```
$apify push
```

1. **Access your actor** at [Apify Console](https://console.apify.com/actors)

### Running on Apify

1. Navigate to your actor in the Apify Console
2. Click "Run"
3. Configure input options (optional)
4. Click "Start" to run the actor
5. View results in the "Dataset" tab

## ⚙️ Input Configuration

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `maxStories` | integer | 30 | Maximum number of stories to scrape (1-100) |
| `includeJobPosts` | boolean | false | Include "Who is hiring?" job posts |

### Example Input

```
{
  "maxStories": 30,
  "includeJobPosts": false
}
```

## 📊 Output Format

Each story is returned as a JSON object with the following structure:

```
{
  "rank": 1,
  "title": "Show HN: I built a tool for...",
  "url": "https://example.com/article",
  "points": 342,
  "author": "username",
  "comments": 127,
  "timeAgo": "2024-01-15T10:30:00.000Z",
  "hackerNewsUrl": "https://news.ycombinator.com/item?id=12345678"
}
```

### Output Fields

| Field | Type | Description |
| --- | --- | --- |
| `rank` | number | Story position on front page |
| `title` | string | Story title |
| `url` | string | Link to the story/article |
| `points` | number | Number of upvotes |
| `author` | string | Username who posted the story |
| `comments` | number | Number of comments |
| `timeAgo` | string | Timestamp when story was posted |
| `hackerNewsUrl` | string | URL to Hacker News discussion |

## 🛠️ Built With

- **Python 3.11** - Programming language
- **Playwright** - Browser automation
- **Apify SDK** - Actor framework
- Following Apify best practices and patterns

## 📝 Use Cases

- Monitor trending tech stories
- Track specific topics on HN
- Build custom HN readers/aggregators
- Research what content performs well
- Create HN analytics dashboards

## 🔒 Rate Limiting

The scraper is designed to be respectful of Hacker News:

- Single page load per run
- No aggressive pagination
- Configurable limits on stories scraped

## 📄 License

This actor is provided as-is for use on the Apify platform.

## 🤝 Support

For issues or questions:

- Check the [Apify documentation](https://docs.apify.com)
- Open an issue in the repository
- Contact via Apify platform

---

**Ready to deploy in under 10 minutes! 🎉**