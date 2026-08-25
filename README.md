# wkhtmltopdf Buildpack

This is a [Heroku buildpack][0] for bundling a compatible [wkhtmltopdf][1]
binary with your environment.

## Versions

* wkhtmltopdf: `0.12.4` by default

Upstream published Linux builds in two places, and the version format picks
the download source:

* **Unhyphenated versions** (e.g. `0.12.4`) download the self-contained
  `linux-generic-amd64.tar.xz` from [wkhtmltopdf/wkhtmltopdf releases][3].
  0.12.4 is the last release that ships this asset.
* **Hyphenated versions** (e.g. `0.12.6.1-3`) download the
  `jammy_amd64.deb` from [wkhtmltopdf/packaging releases][4] — upstream's
  newest Linux builds, and the same build the `wkhtmltopdf-binary` gem ships
  for Ubuntu 22.04 and 24.04.

## Usage

Add this buildpack to your application (via `.buildpacks` with dokku, or
[multiple buildpacks][2] on Heroku) to install the `wkhtmltopdf` and
`wkhtmltoimage` binaries into `bin/`, the `libwkhtmltox` library into
`vendor/wkhtmltox/lib/`, and the bundled CJK fonts into `~/.fonts`.

To use a version other than the default, set `WKHTMLTOPDF_VERSION`:

```bash
$ dokku config:set appname WKHTMLTOPDF_VERSION="0.12.6.1-3"
```

Downloads are cached per version, so changing `WKHTMLTOPDF_VERSION` takes
effect on the next deploy without purging the build cache.

## Build-time verification

The compile step ends by running `wkhtmltopdf --version` and rendering a
smoke-test PDF with the installed binary and fonts. If the binary cannot run
on the current stack's base image (e.g. after a base image upgrade), the
deploy fails at build time instead of PDF generation failing at runtime.

[0]: http://devcenter.heroku.com/articles/buildpacks
[1]: http://wkhtmltopdf.org/
[2]: https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app
[3]: https://github.com/wkhtmltopdf/wkhtmltopdf/releases
[4]: https://github.com/wkhtmltopdf/packaging/releases
