# Contributing catalog indicators

Add a `.ind` file to `sources/` with a `catalog.<name>` ID and `<name>.ind`
filename. Open a pull request explaining its inputs, plots, and warm-up needs.

Keep existing IDs stable because they identify indicators in saved chart settings.
Include a `source` URL in the `indicator(...)` declaration pointing to the file
in this repository, for example:

```text
source = "https://github.com/flowsurface-rs/indicators/blob/main/sources/atr.ind"
```

The application displays this URL in the indicator's Source tab. Preserve author
credits and keep `author_url` pointing to the author's profile.

## Validation

Build the CLI from a separate checkout of
[Flowsurface](https://github.com/flowsurface-rs/flowsurface). Use the application
revision pinned by [CI](.github/workflows/validate.yml) to reproduce its checks.

With the application checkout at `../flowsurface`, run these commands from this
catalog checkout before submitting:

```sh
cd ../flowsurface
cargo run --locked -p flowsurface-indicator-engine --bin flowsurface-indicator -- check ../indicators/sources --namespace catalog
cargo run --locked -p flowsurface-indicator-engine --bin flowsurface-indicator -- test ../indicators/sources --namespace catalog
```

These commands build only the CLI and its dependencies. They check syntax,
metadata, filenames, duplicate IDs, and execution on synthetic bars. Also verify
the formula, other input settings, and chart appearance in the application.

CI runs both commands automatically for pull requests. If a source needs newer
engine features, update the pinned application revision and describe the required
application build in the pull request.

## Developer Certificate of Origin

Sources and documentation in this repository use [Apache-2.0](LICENSE).
Sign off each commit with your real name and email for the Developer
Certificate of Origin (DCO):

```sh
git commit -s
```

This adds a line to the commit message:

```text
Signed-off-by: Your Name <you@example.com>
```

By signing off, you certify that you have the right to submit the work under
this license.
