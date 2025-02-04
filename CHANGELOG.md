# Changelog

All notable changes to this project will be documented in this file, per [the Keep a Changelog standard](http://keepachangelog.com/).

## [Unreleased] - TBD

## [1.0.2] - 2025-02-04

### Fixed

- Handle the error `detected dubious ownership in repository at '/github/workspace'` when using a `.gitattributes` file (props [@dkotter](https://github.com/dkotter), [@iamdharmesh](https://github.com/iamdharmesh) via [#7](https://github.com/10up/action-wordpress-plugin-build-zip/pull/7)).
- Ensure built files are included when used without a `BUILD_DIR` and `.distignore` file (props [@dkotter](https://github.com/dkotter), [@iamdharmesh](https://github.com/iamdharmesh) via [#7](https://github.com/10up/action-wordpress-plugin-build-zip/pull/7)).
- Install SVN as part of the workflow, if needed (props [@kirtangajjar](https://github.com/kirtangajjar), [@dkotter](https://github.com/dkotter), [@faisal-alvi](https://github.com/faisal-alvi) via [#8](https://github.com/10up/action-wordpress-plugin-build-zip/pull/8)).

### Developer

- Replaced `lee-dohm/no-response` with `actions/stale` to help with closing no-response/stale issues (props [@jeffpaul](https://github.com/jeffpaul), [@dkotter](https://github.com/dkotter) via [#5](https://github.com/10up/action-wordpress-plugin-build-zip/pull/5)).

## [1.0.1] - 2024-03-20

### Changed

- Updated to v4 of `upload-artifact`, the action now exposes the artifact URL with: `${{ steps.upload-plugin-artifact.outputs.artifact-url }}` (props [@jdevalk](https://github.com/jdevalk), [@dkotter](https://github.com/dkotter) via [#3](https://github.com/10up/action-wordpress-plugin-build-zip/pull/3)).

## [1.0.0] - 2022-12-01

- Initial release.

[Unreleased]: https://github.com/10up/action-wordpress-plugin-build-zip/compare/stable...develop
[1.0.2]: https://github.com/10up/action-wordpress-plugin-build-zip/compare/1.0.1...1.0.2
[1.0.1]: https://github.com/10up/action-wordpress-plugin-build-zip/compare/1.0.0...1.0.1
[1.0.0]: https://github.com/10up/action-wordpress-plugin-build-zip/releases/tag/1.0.0
