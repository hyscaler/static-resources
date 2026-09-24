# static-resources

Static assets served over HTTPS by GitHub Pages from the `main` branch.

Base URL: `https://hyscaler.github.io/static-resources/`

`.nojekyll` is present so Pages publishes the tree verbatim rather than running
it through Jekyll.

## Layout

Each asset set lives under an opaque directory identifier. This repository is
public, so directory names deliberately carry no meaning: which deployment
consumes which path is recorded in the relevant private infrastructure
repository, not here.

Do not add hostnames, environment names, server names, or other infrastructure
detail to paths, filenames, comments, or commit messages.

## Staging banner

`staging-banner.css` draws a fixed triangle in the bottom-left corner of a
non-production deployment: translucent at rest, fully opaque on hover, with
hazard stripes drifting underneath.

It expects the consuming reverse proxy to inject two things into every HTML
response:

```html
<link rel="stylesheet" href="/<local path>/staging-banner.css?v=<token>">
<div class="hs-staging-badge"></div>
```

Two constraints shaped the implementation, both worth preserving:

- **It styles a real element, not a pseudo-element.** Chrome does not reliably
  hit-test generated content, so `:hover` never fires on a `::after` badge and
  it can never go opaque.
- **The wordmark is embedded as a `data:` URI.** The consuming application sends
  a `Content-Security-Policy` whose `img-src` is `'self' data:`, so an
  externally hosted image is blocked by the browser. The logo is recoloured to
  white with `fill` attributes rather than shipping a separate white asset.

### Changing it

Edit, commit, push. Pages rebuilds within about a minute.

If the consuming site sits behind a CDN that rewrites `Cache-Control`, browsers
may hold the old file well past the origin's TTL. In that case the proxy's `?v=`
token has to be bumped too, otherwise the change will not be visible.
