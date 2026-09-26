# The Osy# package index

`index.json` is the list of Osy# packages this toolchain knows about. **`osy search` reads it**, so one
unauthenticated request answers what a GitHub search plus a release lookup per hit used to.

## It is generated, not curated

Most of it comes from GitHub's search for repositories carrying the **`osy-package`** topic, which `osy publish`
applies for you. **If you publish a package, you are in this file automatically** — nobody has to accept you, and
there is nothing to ask for.

A small hand-written overlay adds packages that search cannot see yet. An overlay entry is dropped the moment the
search finds its repository, and the generator refuses to build until it is deleted — so the overlay can never
quietly shadow a real package, and this file can never drift into a gatekeeping list.

## Two states, and the difference matters

| `availability` | what it means |
|---|---|
| `Published` | a GitHub release exists. `use` resolves, and the entry carries the exact line. |
| `Known` | we know the package exists and where it lives. **No release yet, so there is nothing to depend on** — and deliberately no `use` line, because one that cannot resolve costs the reader more than the absence does. |

## Adding your package

Publish it with `osy publish`. That tags the repository `osy-package` and cuts the release, and the next
regeneration picks it up. Nothing here to edit.

If your package is not on GitHub, open an issue — that is what the overlay is for.
