# Frontend TypeScript — NASA Videos

Next.js + TypeScript frontend component for the NASA Video Library feature, built for a headless Drupal 11 + Next.js architecture. The Drupal backend module that registers this as a paragraph type lives at: https://github.com/franciscojavierguardado101/Drupal-Custom-Module-Nasa-Videos

## What it does

- Search bar that queries the NASA Images and Video Library API in real time
- Topic filter pills: Space, ISS, Mars, Moon, Webb, Earth, Launches, Hubble
- Responsive auto-fill grid of video cards with thumbnail, title, date, and description
- Clicking a card opens an inline HTML5 video modal — fetches the `.mp4` asset URL on open and plays it natively in the browser
- ESC key and backdrop click close the modal
- Load More button appends the next page of results without a page reload
- Results count displayed above the grid

## APIs used (no key required)

| Data | Source |
|------|--------|
| Video search + metadata | `https://images-api.nasa.gov/search` |
| Video asset (.mp4) URL | `https://images-api.nasa.gov/asset/{nasa_id}` |

## File structure

```
src/
  app/
    api/
      nasa-videos/
        route.ts              # Next.js API proxy: search + asset URL fetcher
  components/
    paragraphs/
      nasa-videos/
        NasaVideos.tsx        # Main component: search, topic pills, grid, modal
        types.ts              # TypeScript interface for NasaVideoItem
        index.ts              # Barrel export
```

## How the API route works

`route.ts` handles two actions via query params:

| Param | Behavior |
|-------|----------|
| `?q=space&page=1` | Searches NASA Images API, returns 12 results per page |
| `?action=asset&id={nasa_id}` | Fetches the asset manifest and returns the best available `.mp4` URL |

## Stack

- Next.js 16 App Router
- TypeScript
- Drupal 11 headless backend (Pantheon)
- Deployed on Vercel
