# Changelog

## 2026-04-07

### Homepage framework
- Added a custom homepage shell in `layouts/index.html`.
- Kept the homepage split into four independent sections: `Hero`, `Navigator`, `News`, `Projects`, and `Experience`.
- The homepage now assembles data through partials instead of hardcoding everything in one template.

### Navigator
- Added a config-driven navigator via `layouts/partials/home-navigator.html`.
- Navigator items are declared in `hugo.toml` under `[[params.navigator]]`.
- Added an `enabled` flag so links like `Posts` or `About Me` can be hidden without editing templates.

### News
- Added `layouts/partials/home-news.html` and `data/news.toml`.
- Homepage news is rendered from data entries instead of content pages.
- `text` is rendered with `markdownify`, so partial inline links such as `[paper](...)` work inside a news sentence.

### Projects
- Added `layouts/partials/home-projects.html` for homepage project cards.
- Projects are now rendered from the `projects` section and sorted by `Params.weight`.
- Project cards resolve a bundle-local `cover.*` first, and only fall back to front matter if needed.
- Project metadata was refined so venue and outbound links share one line, project links open in a new tab, and only the site owner's name is bold in the author list.

### Experience
- Added `layouts/partials/home-experience.html` and `data/experience.toml`.
- Experience is implemented as a compact homepage CV block driven by data entries.
- Role and summary fields support Markdown links through `markdownify`.

### Posts and content bundles
- Migrated posts to page bundle structure, e.g. `content/posts/<slug>/index.md`.
- Added a project-level Markdown image render hook in `layouts/_markup/render-image.html`.
- Core logic: relative image paths inside a post are rewritten against `.Page.RelPermalink`, so post-local images can live in the same directory as `index.md`.

### Post pages
- Added a project-level post template override in `layouts/_default/single.html`.
- Post pages now place metadata directly below tags in the order `date / author / reading time`.
- Metadata is shown only for the `posts` section, so `About`-style pages stay clean.
- The default author is read from `params.author.name` in `hugo.toml`.
- Added a local `layouts/partials/date.html` override to remove the trailing whitespace from the date partial.

### Styling and interaction
- Consolidated custom presentation logic into `assets/css/custom.css`.
- Tuned hero spacing, navigator layout, news density, project card ratios, and experience card styling.
- Standardized link treatment across homepage modules: clearer default colors and underline feedback on hover.
- Added a mobile-focused polish pass: reduced viewport padding, switched the homepage hero to a stacked layout earlier, kept navigator links centered on small screens, and tightened project / experience spacing for narrow displays.
- Kept visual changes project-local so `themes/shibui` stays untouched.

### Documentation and maintainability
- Added concise comments in key templates and stylesheet sections to explain data flow and override strategy.
- Restored a root `README.md` describing how to create and remove posts and projects with page bundles.

## 2026-04-06

### Initial Hugo setup
- Initialized the repository as a Hugo site and attached `Shibui` as a Git submodule theme.
- Added base site configuration in `hugo.toml`.
- Verified local development with `hugo server -D`.

### Early homepage and taxonomy work
- Added the first homepage intro content in `content/_index.md`.
- Added custom tags rendering in `layouts/tags/taxonomy.html` so `/tags/` displays inline tag links instead of dated list rows.
- Added a custom posts list template in `layouts/posts/list.html` to surface tag navigation above the posts list.

### Image and theme overrides
- Added `assets/css/custom.css` as the main project-level style override layer.
- Overrode the theme image treatment to remove the default border/padding look for article images.
- Added initial sample content to validate text posts, image posts, and homepage customization.
