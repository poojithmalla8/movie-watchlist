# movie-watchlist

Personal movie/series watchlist database, built from an Instagram "Movie Recommendations" saved collection.

## The database

The catalog is sharded across `movies-01.json` … `movies-04.json` (about 1,300 titles total).
Each file is a JSON array; each entry looks like:

```json
{
  "id": "tt0111161",
  "title": "The Shawshank Redemption",
  "type": "movie",
  "year": 1994,
  "genres": ["Drama", "Crime"],
  "language": "English",
  "rating": 9.3,
  "poster": "https://...",
  "saves": 12
}
```

- `type` is `movie` or `series`
- `rating` is the IMDb average rating (may be null)
- `language` is the original language (may be null)
- `poster` is a thumbnail URL (may be null)
- `saves` counts how many saved Instagram posts recommended the title
- Plot descriptions are intentionally omitted.

To load the whole database, concatenate the four arrays.

## Refresh

The database is refreshed automatically once a day from the latest saved posts.
New recommendations are extracted, matched against IMDb metadata, and merged in
(deduplicated by IMDb id).
