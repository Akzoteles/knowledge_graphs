# Personal knowledge graphs — a directory

A single-page, hand-curated directory of dependency-graph-style personal
knowledge sites — yours and others you find — regardless of where each
one is hosted. Cards can be filtered by host (GitHub Pages / Vercel /
other web) and sorted by name, curatorial order, or recent activity.

There's no database and no build step: every entry lives in one
JavaScript array near the top of `index.html`. Adding a site means
adding a few lines to that array.

## How to host it on GitHub Pages

1. Create a new repository on GitHub (e.g. `knowledge-graphs`).
2. Upload `index.html` and `.nojekyll` — drag them into the GitHub web
   UI ("Add file" → "Upload files"), or push them with git.
3. In the repository, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to "Deploy from a
   branch", pick the `main` branch and the `/ (root)` folder, then save.
5. GitHub gives you a URL a minute or two later, usually
   `https://<username>.github.io/<repo-name>/`.

## Adding an entry

Open `index.html`, find the `SITES` array near the top of the
`<script>` block, and add a block like this — anywhere in the array,
in whatever order you want them to appear by default:

```js
{
  name: 'Site name',
  url: 'https://example.com/',
  host: 'github-pages',   // must be exactly: 'github-pages', 'vercel', or 'web'
  author: 'Their name',   // optional — omit or leave '' to hide the byline
  description: 'A short description of what this graph covers.',
  tags: ['philosophy', 'systems'],   // optional
  repoUrl: 'https://github.com/owner/repo',  // optional — see below
  dateAdded: '2026-08-19',  // 'YYYY-MM-DD', the day you added it
},
```

The four **example entries** already in the file (`Example — GitHub
Pages site`, `Example — Vercel site`, `Example — other web`) are just
placeholders showing the three host types. Delete them once you've got
real entries in, or leave one of each as a quick reference for the
format.

### About `repoUrl` and live dates

If a site's source is public on GitHub, add `repoUrl` and its card will
automatically show a **live** "repo updated X days ago," pulled from
that repo's last commit every time someone visits the page — no
manual updating needed. This works regardless of whether the site
itself is hosted on GitHub Pages, Vercel, or anywhere else, as long as
the *code* lives in a public GitHub repo.

If there's no `repoUrl` (or the source isn't on GitHub), the card falls
back to showing "added {dateAdded}" — the date you typed in by hand.
That date is also what "Sort: most recently active" uses for entries
without a live repo, so it's worth keeping accurate as a rough signal
even when it's not a true "last updated."

## Notes and limitations

- **Rate limits**: each visitor's browser calls the GitHub API once per
  entry that has a `repoUrl`. GitHub allows 60 unauthenticated requests
  per hour per visitor IP — fine unless the list grows past several
  dozen GitHub-linked entries.
- This is intentionally *not* auto-discovering sites — you're
  curating it by hand, which also means you control what gets listed.
