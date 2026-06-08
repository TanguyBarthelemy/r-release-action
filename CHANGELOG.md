# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres
to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] - 2026-06-08

### Added

* New deps to libuv (related to the [R package {fs}](https://github.com/r-lib/fs/compare/v2.0.1..main))
* Call to heylogs to check version number update CHANGELOG, and generate release note (release body)

### Removed 

* Arg gh_repo (no more used)


## [1.0.2] - 2026-03-16

### Changed

* Accept current Java version

### Fixed

* Update apt version


## [1.0.1] - 2026-01-28

### Fixed

* shell field for each step
* main -> dev branch by default
* Add tag and rename `Tag` in `tag` for consistency


## [1.0.0] - 2025-11-12

### Added

- First release of the action
- Adapt to the {releaser} R package release on CRAN (v1.0.0)


[Unreleased]: https://github.com/TanguyBarthelemy/r-release-action/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/TanguyBarthelemy/r-release-action/compare/v1.0.2...v1.1.0
[1.0.2]: https://github.com/TanguyBarthelemy/r-release-action/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/TanguyBarthelemy/r-release-action/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/TanguyBarthelemy/r-release-action/releases/tag/v1.0.0
