# Flowsurface indicators

Optional `.ind` indicators for [Flowsurface](https://github.com/flowsurface-rs/flowsurface).
Install these sources without rebuilding the application. The engine and bundled
indicators remain in the application repository.

Each indicator is a `.ind` file defining its calculations and presentation.
Its filename must match the final ID segment: `alice.rsi` goes in `rsi.ind`.
Full IDs must be unique; matching filenames can coexist in separate folders.
Folder names do not assign IDs.

| Collection | IDs | License | Availability |
| --- | --- | --- | --- |
| [Bundled](https://github.com/flowsurface-rs/flowsurface/tree/main/data/indicators) | `core.*` | [GPL-3.0-or-later](https://github.com/flowsurface-rs/flowsurface/blob/main/data/indicators/LICENSE) | Included in Flowsurface |
| [Catalog](sources/) | `catalog.*` | [Apache-2.0](LICENSE) | Optional; install manually |

## Install and run

Use a Flowsurface build that includes scripted-indicator support.
Copy the desired `.ind` files or folders from [sources/](sources/) into `<data-directory>/indicators/`,
then restart Flowsurface. The data directory is `$FLOWSURFACE_DATA_PATH` when
set, otherwise the platform data directory's `flowsurface/` folder.
Flowsurface creates this directory at startup and searches subfolders,
skipping symlinks.

For development, pass an explicit file (repeat the option for more files):

```sh
flowsurface --indicator-path /path/to/example.ind
```

Or, from a checkout of this catalog, use all sources with an installed application:

```sh
FLOWSURFACE_INDICATORS_PATH="$PWD/sources" flowsurface
```

Bundled indicators remain available when using either option.

Sources load once at startup. Invalid installed sources are skipped with
diagnostics. Bundled IDs take precedence over installed duplicates; otherwise,
the first installed source with an ID wins.

For authoring, see the [language reference](https://github.com/flowsurface-rs/flowsurface/blob/main/indicator-engine/LANGUAGE.md)
and [CLI workflow](https://github.com/flowsurface-rs/flowsurface/tree/main/indicator-engine#cli). Run `check` and `test`
before installing a source.

## Compatibility

The [validation workflow](.github/workflows/validate.yml) pins the application
revision whose engine checks these sources. Indicators using newer language
features may require a newer application build. Update that revision and document
the application requirement when adding such features.

## Catalog contributions

Add sources to `sources/` using `catalog.<name>` IDs and `<name>.ind` filenames.
See [CONTRIBUTING.md](CONTRIBUTING.md) for validation, Apache-2.0 licensing,
and DCO sign-off requirements.
