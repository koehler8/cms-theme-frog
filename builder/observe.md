# Observe facet — cms-theme-frog

What this repo exposes that a production sweep should watch, and how to reach
each source from the runner host (read-only). One source per section.

cms-theme-frog is the `@koehler8/cms-theme-frog` npm package, a shared Vertex
CMS theme (palette, type and surfaces). It is a member repo of the `cms`
product; the product brief lives in `cms` (`builder/phases/observe.md`),
and this file is only this repo's source map.

A merge to `main` never publishes. Only a pushed `v*` tag runs
`.github/workflows/publish.yml`, which publishes to npm.

## Sources

- **Dependencies** — `builder/scanners/dependencies.mjs` (buildmill's standard
  scanner) reads `package-lock.json`. The package has no runtime dependencies;
  its one peer, `@koehler8/cms`, is also a devDependency so the scanner tracks
  it. A `dependency major behind: @koehler8/cms` finding means a new cms major
  is out and the peer range `^1.0.0-beta.1` in `package.json` does not admit
  it: a site on that major will warn on install until this theme widens its
  range and publishes.
- **Published version** — the npm registry:
  `npm view @koehler8/cms-theme-frog version deprecated time.modified --json`
  — `version` should equal `package.json`'s `version` on `main`, and
  `deprecated` should be absent.
- **Publish workflow** — GitHub Actions:
  `gh run list --repo koehler8/cms-theme-frog --workflow publish.yml --limit 3 --json conclusion,headBranch,createdAt`
  — the latest run for a `v*` tag should be `success`. Runs only happen on
  tags, so an empty or old list is normal.
- **Consumers** — Used by: site-peepoo. Whether that site resolves the current published version:
  `gh api repos/koehler8/<site>/contents/package-lock.json --jq .content | base64 -d | node -e 'let s="";process.stdin.on("data",d=>s+=d).on("end",()=>console.log(JSON.parse(s).packages["node_modules/@koehler8/cms-theme-frog"]?.version))'`
  — a site several minors behind is that site's own refresh to fix, not this
  repo's.

## Not a source

There is no deployed service, URL or log for this repo: what visitors see
renders inside each site that installs it, and that site's facet watches it.
