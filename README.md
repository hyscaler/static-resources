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
