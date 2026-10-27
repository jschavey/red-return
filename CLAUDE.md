# Red Return — notes for agents

A satirical landing page for a fake luxury startup that composts the ultra-rich and ships them to Mars "to terraform it." The founder is a parody visionary-billionaire. It's a goof for sharing with friends, not a product.

Live: https://jschavey.github.io/red-return/ · Repo: https://github.com/jschavey/red-return

## Ground rules for the satire

- **Fictional people and brands only.** The founder is **Dax Valtor** ("Founder, CEO, Chief Engineer, Chief Visionary & Future Topsoil"). Never name or quote a real person (no Elon), and never use real company names, logos or wordmarks (Tesla, SpaceX, etc.). The archetype carries the joke.
- **The look is borrowed; the brand isn't.** Sleek, minimal, black-and-white futurist showroom styling with a Mars-red accent. No car metaphors: Fory found "0–soil in 60" style jokes dumb. Keep jokes about death, wealth, Mars, terraforming, and startup hype.
- **Never collect anything.** No real forms, email capture, payment fields, analytics or tracking. The "Reserve" button only reveals a joke message.
- **Keep the footer disclaimer** ("Red Return is satire. No one is shipping anyone to Mars in a jar.") and the README's satire note.
- Humor register: deadpan, corporate-sincere, one beat per line. Good examples already on the page: "Will I be the first human on Mars? — In a sense." / "We just use more of you." / "Lifetime (expired)."

## How the page is built

- **One file: `index.html`.** No build step, no framework, no dependencies besides Google Fonts (Manrope, JetBrains Mono).
- It was ported from a Claude Design canvas, so most styling is **inline `style="…"`**. Shared component styles (`.opt` tier buttons, `.sw` swatches, focus rings) live in the `<style>` block in `<head>`. The repo is now the source of truth; the original Design artifact has diverged.
- Palette: ground `#050505`, panels `#0c0c0c`, text `#f2f2f0`, muted `#9a9a96`/`#b8b8b4`, borders `#1c1c1c`/`#222`, accent `#E0482E`.
- Sections in order: header nav → hero (`#top`, glowing Mars) → key figures → tiers (`#models`) → configurator (`#configure`) → founder quote → specs (`#specs`) → FAQ (`#faq`) → footer.
- **Configurator** is the `<script>` at the bottom of the page. Edit the `tiers` and `finishes` arrays there to change packages or soil blends (price, note, swatch hex, preview gradient). Upgrades are the `#fsc` (Eternal Livestream, +$15k) and `#priority` (Priority Launch, +$1M) checkboxes; their prices are in `render()`. Text that changes is filled into `<span data-bind="…">` (`finishName`, `finishNote`, `total`, `deposit`). The deposit is 10% of the total.
- Must work at phone width (390px) with no horizontal scroll, and keep real `<button>`/`<label>` elements and ≥44px tap targets.

## Checking changes

Open `index.html` directly or run `python3 -m http.server`. A quick Playwright pass is worth it after edits: load at 1280×900 and 390×844, confirm `document.documentElement.scrollWidth` equals the viewport width on mobile, click a tier/blend/upgrade and confirm the total updates, click Reserve and confirm `#reserved` shows, and confirm there are no page errors.

## Deploying

Push to `main` and GitHub Pages publishes from the repo root (classic Pages build, no Actions workflow). It goes live a minute or so later. Build status: `gh api repos/jschavey/red-return/pages/builds/latest -q .status`.

**Commit email:** GitHub blocks pushes that expose Fory's private email. Commits must use `879281+jschavey@users.noreply.github.com` (already set in this repo's git config). If a push fails with GH007, fix it with `git commit --amend --no-edit --reset-author`.

## Possible later ideas

- Custom domain: a `.click` domain is $3/yr on Route 53 (e.g. `redreturn.click`). Add a `CNAME` file with the domain and point DNS at GitHub Pages.
- Bits floated but not built: a fake livestream "launch event" section, a parody investor deck.
