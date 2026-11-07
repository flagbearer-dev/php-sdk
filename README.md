# flagbearer for PHP

PHP SDK for Flagbearer. Checks flags locally against an environment's rules,
which are shared between requests through a cache and refreshed when they're
older than a TTL. Requires PHP 8.1 or later with the curl, json and mbstring
extensions; its only dependency is `psr/simple-cache`.

## Docs

Keys, caching, per-request checks, Laravel setup and exposures are covered at
[docs.flagbearer.dev/sdks/php](https://docs.flagbearer.dev/sdks/php).

## Development

Requires PHP 8.3 or later and Composer for the dev tools. From this directory:

```sh
composer install
vendor/bin/phpunit
vendor/bin/phpstan analyse
```

The tests include the shared evaluation fixtures in
[`tests/fixtures/evaluation.json`](tests/fixtures/evaluation.json), a copy of the cases
every Flagbearer SDK must reproduce,
and run the client against a fake SDK server under `php -S`. Flagbearer's integration tests run this SDK against the real backend through
[`testing/server`](testing/server),
one fresh PHP request per HTTP request.

## Releasing

Packagist publishes `flagbearer/flagbearer` from this repository's `vX.Y.Z` tags;
nothing is uploaded.

1. Bump `Version::VERSION` in `src/Version.php` and merge.
2. Run the **Release** workflow from the Actions tab. It runs the tests and tags
   the commit `vX.Y.Z`.
3. Packagist picks up the tag through its GitHub hook, or on **Update** in its UI.
