# CineTon

> Some of the films I've watched. The rest of the drama? I'm living it.

CineTon is a personal cinema diary for browsing watched films and keeping a watchlist. It pairs a clean, responsive interface with personal ratings, film details, and lightweight visitor interaction.

**Live site:** https://toxinhub.github.io/cineton/

## Features

- Browse watched titles and the watchlist.
- Switch between poster-grid and compact list views.
- Search and filter the library by relevant title details.
- Sort titles by rating, release year, title, and recency.
- Explore film and TV details, including posters, synopsis, cast, director or creator, and ratings when available.
- Add personal ratings, notes, and watched dates to library entries.
- Use random-title discovery to find something to watch.
- Submit public ratings and comments where enabled.
- Responsive layout for desktop and mobile.
- Warm, understated cream, cocoa, and muted-gold styling with Mina and Cormorant Garamond typography.

## Technology

- HTML, CSS, and vanilla JavaScript
- GitHub Pages for hosting
- JSON-based library data
- TMDB and optional OMDb metadata integrations
- Supabase-powered visitor interaction features

CineTon does not require a frontend framework or a build step.

## Project files

| File | Purpose |
| --- | --- |
| `index.html` | Public cinema diary |
| `admin.html` | Library-management interface |
| `data.json` | Movie and TV library data |
| `README.md` | Project documentation |

## Privacy and security

- Never commit access tokens, API keys, passwords, or other credentials to the repository.
- Do not place private or sensitive information in public files. If the repository is public, its committed library data is public too.
- Use the admin interface only with credentials you are authorized to use. Keep tokens private and grant only the permissions needed.
- Browser-side configuration is not a secure place to publish secrets. Treat anything committed to the repository or delivered to visitors as public.
- Visitor-submitted content may be visible to other visitors.

## Third-party services

CineTon may use TMDB and OMDb for title metadata and Supabase for visitor interaction features. Their services are subject to their own terms and policies.

This project is a personal cinema diary, not a streaming service. Film metadata, artwork, and ratings may be provided by third-party sources.

## Maintenance

Keep documentation aligned with the current public experience. Avoid publishing private configuration, credentials, internal operational details, or implementation notes that visitors do not need.
