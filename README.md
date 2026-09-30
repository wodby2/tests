# Wodby dashboard E2E build fixture

A Drupal 11 codebase based on [wodby/drupal-vanilla](https://github.com/wodby/drupal-vanilla) (branch `11.x`) that
Wodby's dashboard E2E tests connect as a repository, to check builds that a boilerplate can't cover.

- `main` builds and deploys normally. Its `php_Dockerfile` declares the build argument `E2E_BUILD_VALUE` and writes
  it to `/var/www/html/e2e-build-value.txt`, so a test can set the app service build variable and read it back.
  Without the variable, the file contains `unset`.
- `broken-build` fails its build on purpose in the first pipeline step, so a test can check that a failed build leaves
  the running deployment serving.

Don't change these branches by hand: the tests depend on their exact behavior.
