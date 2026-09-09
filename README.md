# adrienbouttier.com

Source of my personal site — a single-page profile built with [Hugo](https://gohugo.io),
published at <https://www.adrienbouttier.com>.

## Structure

All the content lives in **`config.yaml`**. There is no `content/` directory: every
section of the page — hero, about, technologies, experience, education, projects — is a
block under `params`, and the theme renders whichever ones are enabled.

```
config.yaml            all the content and the section toggles
static/                CNAME, og-cover.png (the social preview card)
themes/hugo-theme/     the theme, vendored (see below)
```

The theme began as a fork of [hugo-profile](https://github.com/gurusabarish/hugo-profile)
and was tracked as a git submodule until that fork's repository disappeared, which left
the site unbuildable — every CI run failed at submodule checkout. It is now vendored
in-tree, so the site no longer depends on an external repository to build.

## Local preview

```sh
hugo server        # http://localhost:1313
```

CI builds with Hugo 0.134.0; use the same version locally to avoid surprises.

## Deployment

Pushing to `main` runs [`.github/workflows/hugo.yml`](.github/workflows/hugo.yml), which
builds the site and publishes it to GitHub Pages. The custom domain comes from
`static/CNAME`.

Note that GitHub serves the site with `cache-control: max-age=600`: for ten minutes after
a deploy, a normal reload may still show the previous version. Force-refresh to check a
change.
