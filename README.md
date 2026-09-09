# Emily's Birthday Quest

A little retro-arcade birthday website: a passcode gate, three riddles, a
catch-the-gems game, and a final map reveal that ends with a trip to Wilsons
Prom.

Everything lives in **one file**, `index.html` — no build step, no
dependencies. The other files (`_redirects`, `vercel.json`, `404.html`) just
help whichever host you pick understand the page routing (see below).

## The passcode

`100997`. It's set near the top of the `<script>` block in `index.html` as
`PASSCODE`, if you ever want to change it.

## Pages / URLs

| URL | Page |
|---|---|
| `/1` (or just `/`) | Passcode gate |
| `/2` | Welcome message |
| `/3` | Riddle: Noi Pizzeria |
| `/4` | Riddle: "bestie" |
| `/5` | Riddle: jewellery / gardening |
| `/6` | Catch-the-gems game |
| `/7` | Final map — click to find Wilsons Prom |

## Easiest way to publish it (2 minutes, no account tricks)

**Netlify Drop** — no git, no login required:

1. Go to **https://app.netlify.com/drop**
2. Drag this whole folder onto the page
3. You'll get a live link instantly (you can rename it in the site settings
   to something like `emily-birthday.netlify.app`)

The included `_redirects` file makes sure `/2`, `/3` etc. all work when
typed directly or refreshed, not just when clicked through from the app.

### Alternative: Vercel

If you'd rather use Vercel, drag the folder into a new project the same way,
or connect it as a git repo. The included `vercel.json` handles the same
routing fix as Netlify's `_redirects`.

### Alternative: GitHub Pages

Push this folder to a repo and enable Pages in the repo settings. The
included `404.html` handles the routing fix for GitHub Pages specifically
(it has no server config, so it needs a small redirect trick instead). It
works for both a root domain and a `username.github.io/reponame/` style URL.

## Testing it locally before you send it

From inside this folder, run:

```
python3 -m http.server 8000
```

then open `http://localhost:8000/` and click through normally — all the
in-app navigation (buttons, the passcode auto-advance, etc.) works fine on a
plain local server. Directly typing a sub-path like `http://localhost:8000/3`
into the address bar won't work locally (that needs the redirect rules
above, which only matter once it's actually deployed).

## Editing the content later

Everything is in `index.html`:

- `PASSCODE` — the 6-digit code
- `RIDDLES` — the array with each riddle's prompt, accepted answers, and hint
- The welcome message text is in `renderWelcome()`
- The final reveal text ("We're going to Wilsons Prom!") is in `renderMap()`,
  inside the `handleClick` function, in the `reveal.innerHTML` line
- The gem-catching game's target score (15) and timer (30s) are the
  `TARGET` and `timeLeft` variables in `renderGame()`

No build tools needed — just edit the HTML file directly and re-deploy
(drag the folder into Netlify Drop again, or `git push` if using Pages).
