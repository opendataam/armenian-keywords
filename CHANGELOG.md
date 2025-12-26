# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] - 2025-12-26

### Added

- **Language-specific data organization**: Reorganized data files into language-specific directories (`data/ru/`, `data/en/`)
- **Russian keywords from Goskatalog**: Processed and extracted keywords from `_legacy/goskatalog/` files:
  - 225 geonames (cities, regions, historical places, geographic features)
  - 110 keywords (cultural terms, basic Armenia terms, historical terms)
  - 51 names (historical figures and Armenian first names)
  - 41 midnames (patronymics)
- **Legacy data preservation**: Moved original data files to `_legacy/data/` directory
- **Source files**: Added original Goskatalog source files to `_legacy/goskatalog/`:
  - `armenian.txt` - Raw Armenian-related word list
  - `armenian_toponyms.txt` - Structured list of Armenian place names
  - `armenian_toponyms_patterns.txt` - Regex patterns for toponym matching
  - `patterns.txt` - Regex patterns for keyword matching
- **Documentation**: Comprehensive README.md with:
  - Updated data structure documentation
  - Guidelines for adding keywords in other languages (Spanish, French, German, etc.)
  - Translation examples and quality guidelines
  - Contribution guidelines

### Changed

- **Data structure**: Migrated from flat `data/*.csv` structure to language-organized `data/[lang]/*.csv`
- **CSV format**: Standardized all CSV files to use `value,category` format
- **README.md**: Complete rewrite with new structure, recent changes, and contribution guidelines

### Fixed

- Fixed typo in `data/en/keywords.csv` (changed "ketword" to "keyword")
- Removed duplicate entries in English keywords file

### Removed

- Old flat data structure files (moved to `_legacy/data/`)

## [1.0.0] - 2023-09-08

### Added

- Initial release of Armenian keywords dataset
- Russian language data files:
  - `geonames.csv` - Geographic names
  - `keywords.csv` - Common keywords
  - `names.csv` - First names
  - `surnames.csv` - Family names
  - `midnames.csv` - Middle names/patronymics
- English language data files:
  - `geonames.csv` - Geographic names
  - `keywords.csv` - Common keywords
- Basic README.md documentation
- LICENSE file

[Unreleased]: https://github.com/opendataam/armenian-keywords/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/opendataam/armenian-keywords/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/opendataam/armenian-keywords/releases/tag/v1.0.0

