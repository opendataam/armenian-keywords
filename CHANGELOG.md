# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- **`id` column** in all CSV files (`value,category,id`): concept key shared across languages, the English canonical form in lowercase (e.g. `ереван`, `эривань`, `erivan`, `երևան` → `yerevan`). Restores the cross-language links of the original `ru,en,am,category` format. Empty when no link is recorded.
- **Armenian data** in `data/hy/`: 77 geonames, 32 keywords, 45 names, 28 surnames, all linked to English via `id`.
- **`ambiguous.csv`** in `data/ru/` (42), `data/en/` (37) and `data/hy/` (3): values that need context to avoid false positives. Includes the exclusion lists from `_legacy/goskatalog/patterns.txt` (`армавир`, `карс`, `нахичевань`, `ашот`, `левон`, `лаваш`, `толма`, ...) and surname suffixes from its regexes (`ян`, `янц`, `янци`, `янцы`, `уни`) under the new `suffix` category.
- `data/ru/keywords.csv`: literal word forms for regexes in `patterns.txt` (`вардапет[аы]`, `католикос[аы]`, `килики[яи]`, `эчмиадзинск[ийогоую]`, `аревелц[и]`, `хнч` → `хнчак`, `гнчак`).

### Changed

- **`data/ru/keywords.csv` rebuilt** from `_legacy/goskatalog/armenian.txt` (107 → 170 entries). It now includes standard inflected forms that were missing (`армяне`, `армянский`, `армянская`, `армении`, `армению`, `армянка`, `ереване`, `ереванский`, `карабахский`, `древнеармянский`, ...). Pre-reform spellings are kept, with Latin `i` from OCR replaced by Cyrillic `і`.
- **Categories fixed** in `data/ru/`:
  - `католикос`, `нварсак`, `аревелц` (as `аревелци`): names → keywords
  - `мамиконян`, `арцруни`, `багратуни`: names → surnames
  - `арменак`, `арменуи`: keywords → names
  - `арменян`, `ереванян`: keywords → surnames
  - `арени`, `дсех`, `тигранакерт`, `васпуракан`, `нор-джуга`, `хорвирап`, `арменикенд`: keywords → geonames
  - `армян`: geonames → keywords
- **Moved to `ambiguous.csv`**:
  - ru: `армавир`, `закавказье`, `закавказская сфср`, `эрзерум`, `карин`, `двин` (geonames); `ашот`, `саака` (names)
  - en: `armavir`, `kars`, `nakhichevan`, `ani`, `berd`, `talin`, `vedi` (geonames); `ashot`, `levon`, `vardan`, `david`, `robert`, `karen`, `edgar`, `artur`, `valery`, `mariam`, `anais`, `ani`, `aram`, `armen`, `arman`, `petros`, `shushan`, `grigor`, `naira`, `gor`, `sevak`, `arsen` (names); `lavash`, `tolma`, `dolma`, `gregorian`, `cher`, `asala`, `kim kardashian` (keywords); `gregorian` (surnames)
- `веди`, `фиолетово`, `фонтан` and `асср`, removed from `data/ru/geonames.csv` in 1.2.0, are restored in `data/ru/ambiguous.csv`.

### Removed

- `data/ru/keywords.csv`: OCR errors and glued tokens (`армянскйо`, `армянсокго`, `армянскомм`, `армянв`, `армяниназахара`, `армянскомуписателю`, `ереванеметодом`, ...); false positives (`армендарис`, `арменонвиль`, `арменопул`, `арментерос`, `арменит`, `арменкино`, ...); stems truncated from regexes (`асла`, `килики`, `эчмиадзинск`).
- `data/ru/geonames.csv`: descriptive strings with commas (`"кавказ, армения"`, `"российская империя, армения"`, ...) and `армен` (already in `names.csv`).
- `data/en/keywords.csv`: `hayk` (kept in `names.csv`).

## [1.2.0] - 2025-12-27

### Added

- **English Data Expansion**: Significantly extended the English dataset coverage:
  - `names.csv`: Added 54 entries of common Armenian given names
  - `surnames.csv`: Added 54 entries of common Armenian surnames
  - `geonames.csv`: Expanded to 79 entries (was 4)
  - `keywords.csv`: Expanded to 42 entries (was 2)

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

