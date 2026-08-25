# 0.3

* Support `wkhtmltopdf/packaging` releases: hyphenated versions
  (e.g. `0.12.6.1-3`) download the jammy amd64 deb, allowing versions past
  0.12.4 (the last release with a linux-generic tarball). Unhyphenated
  versions keep the legacy generic-tarball URL.
* Key the download cache by version so `WKHTMLTOPDF_VERSION` changes take
  effect without a cache purge.
* Fail the download on HTTP errors (`curl -f`) instead of caching an error
  page as the archive.
* Verify the installed binary at build time by rendering a smoke-test PDF,
  so an incompatible base image fails the deploy instead of runtime PDF
  generation.

# 0.2

* Remove all of the forked ruby buildpack code. Change the buildpack to be used
  in conjunction with `heroku-buildpack-multi`.
