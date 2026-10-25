# Sand Blocks Levels

Open data archive of level data for **Sand Blocks: Drop Puzzle** — the physics drop puzzle by Rollic Games where you pull colorful sand blocks into matching Tetris-shaped pits before the timer runs out.

This repository tracks the level metadata behind the fan-made walkthrough site:

> 🌐 **[sand-blocks.org](https://sand-blocks.org/)** — video walkthroughs & pull-order guides for all 600 levels

## What's in here

| Path | Contents |
| --- | --- |
| [`data/levels.json`](data/levels.json) | **Primary dataset.** Every level (1–600) with its solution video, board thumbnail, difficulty band and publish date. Same file the website renders. |
| [`data/games.json`](data/games.json) | Game metadata: developer, genre, installs, version, release date, store listing description. |
| [`data/video-meta.json`](data/video-meta.json) | Per-video YouTube metadata (upload date, duration, max-res availability) collected with yt-dlp. |
| [`data/level-data-normalized.json`](data/level-data-normalized.json) | Normalized crawl output: level → video id / watch URL / thumbnail URL. |
| [`data/level-data-raw.json`](data/level-data-raw.json) | Raw crawl output, kept for provenance. |
| [`data/video-links.json`](data/video-links.json) | Video links extracted from the walkthrough playlist. |
| [`data/crawl-summary.json`](data/crawl-summary.json) | Latest crawl run stats (videos found, images downloaded, gaps). |
| [`data/released-levels.json`](data/released-levels.json) | Level release log — which new levels were published on which date. |
| [`archives/`](archives/) | Release-note posts for newly added level batches (551–600). |

## Level schema

Each entry in `data/levels.json`:

```json
{
  "id": 46,
  "name": "Level 46",
  "image": "https://img.mobilecasualgames.com/sandblocks/level-46.webp",
  "videoId": "-RuDJCNHfvY",
  "embedUrl": "https://www.youtube.com/embed/-RuDJCNHfvY",
  "watchUrl": "https://www.youtube.com/watch?v=-RuDJCNHfvY",
  "sourceUrl": "https://www.youtube.com/watch?v=-RuDJCNHfvY",
  "difficulty": "Beginner",
  "title": "Sand Blocks Level 46 Solution Walkthrough",
  "publishDate": "2026-08-27"
}
```

| Field | Description |
| --- | --- |
| `id` / `name` | Level number, 1–600 |
| `image` | Board thumbnail (webp) |
| `videoId` | YouTube video id of the solution |
| `embedUrl` / `watchUrl` / `sourceUrl` | Embed and watch URLs for the solution video |
| `difficulty` | One of the four bands below |
| `title` | Walkthrough video title |
| `publishDate` | Date the walkthrough was added to the guide |

## Difficulty bands

| Band | Levels |
| --- | --- |
| Beginner | 1 – 99 |
| Intermediate | 100 – 199 |
| Advanced | 200 – 249 |
| Expert | 250 – 600 |

## Data pipeline

1. A crawler watches the Sand Blocks walkthrough playlist on YouTube and the game's store listing.
2. Board thumbnails are downloaded, converted to webp and served from the site's image CDN.
3. Everything is stored in Postgres, then exported into the flat JSON files you see in `data/`.
4. The static site at [sand-blocks.org](https://sand-blocks.org/) builds directly from these files.

New levels are usually released five at a time; `data/released-levels.json` and `archives/` record each batch shortly after it goes live.

## Contributing

Spotted a wrong video, a missing thumbnail, or a level that moved? Please open an issue or pull request.

## Disclaimer

This is an unofficial, fan-made data archive. *Sand Blocks: Drop Puzzle* is a trademark of Rollic Games. Solution videos belong to their respective YouTube channels. Not affiliated with, endorsed by, or sponsored by Rollic Games.
