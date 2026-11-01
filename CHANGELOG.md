# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- **`id` column** in all CSV files (`value,category,id`): concept key shared across languages, the English canonical form in lowercase (e.g. `ереван`, `эривань`, `erivan`, `երևան` → `yerevan`). Restores the cross-language links of the original `ru,en,am,category` format. Empty when no link is recorded.
- **Armenian data** in `data/hy/`: 77 geonames, 32 keywords, 45 names, 28 surnames, all linked to English via `id`.
- **`ambiguous.csv`** in `data/ru/` (89), `data/en/` (38) and `data/hy/` (3): values that need context to avoid false positives. Includes the exclusion lists from `_legacy/goskatalog/patterns.txt` (`армавир`, `карс`, `нахичевань`, `ашот`, `левон`, `лаваш`, `толма`, ...), toponyms that `armenian_toponyms.txt` marks "when Armenian context", and surname suffixes from the regexes in `patterns.txt` (`ян`, `янц`, `янци`, `янцы`, `уни`) under the new `suffix` category.
- `data/ru/keywords.csv`: literal word forms for regexes in `patterns.txt` (`вардапет[аы]`, `католикос[аы]`, `эчмиадзинск[ийогоую]`, `аревелц[и]`, `хнч` → `хнчак`, `гнчак`).
- `data/ru/geonames.csv`: `мравян`, the alternative name of Танжелу lost from parentheses in 1.1.0.
- `.gitattributes`: LF line endings for all text files.
- README: matching rules (whole-word matching, normalization, ambiguous values).

### Changed

- **`data/ru/keywords.csv` rebuilt** from `_legacy/goskatalog/armenian.txt` (107 → 151 entries). It now includes standard inflected forms that were missing (`армяне`, `армянский`, `армянская`, `армении`, `армению`, `армянка`, `ереване`, `ереванский`, `древнеармянский`, ...). Pre-reform spellings are kept, with Latin `i` from OCR replaced by Cyrillic `і`.
- **Categories fixed** in `data/ru/`:
  - `католикос`, `нварсак`, `аревелц` (as `аревелци`): names → keywords
  - `мамиконян`, `арцруни`, `багратуни`: names → surnames
  - `арменак`, `арменуи`: keywords → names
  - `арменян`, `ереванян`: keywords → surnames
  - `арени`, `дсех`, `тигранакерт`, `васпуракан`, `нор-джуга`, `хорвирап`, `арменикенд`: keywords → geonames
  - `армян`: geonames → keywords
- **Moved to `ambiguous.csv`**:
  - ru geonames: `армавир`, `закавказье`, `закавказская сфср`, `эрзерум`, `карин`, `двин`, `камо` (also a nickname and an archaic word), `тифлис`, `тифлиская`, `елизаветполь` (outside Armenia), `карабах`, `киликия` (Karabakh carpets, Roman Cilicia)
  - ru keywords: word forms of `карабах` and `киликия`
  - ru names: `ашот`, `саака`
  - ru surnames: Russian given names and common words that end in `-ян` (`демьян`, `емельян`, `касьян`, `лукьян`, `марьян`, `севастьян`, `татьян`, `троян`, `баян`, `буян`, `бурьян`, `крестьян`, `полян`, `северян`, ...)
  - en geonames: `armavir`, `kars`, `nakhichevan`, `ani`, `berd`, `talin`, `vedi`, `cilicia` (`kilikia` stays)
  - en names: `ashot`, `levon`, `vardan`, `david`, `robert`, `karen`, `edgar`, `artur`, `valery`, `mariam`, `anais`, `ani`, `aram`, `armen`, `arman`, `petros`, `shushan`, `grigor`, `naira`, `gor`, `sevak`, `arsen`
  - en keywords: `lavash`, `tolma`, `dolma`, `gregorian`, `cher`, `asala`, `kim kardashian`; en surnames: `gregorian`
- `веди`, `фиолетово`, `фонтан` and `асср`, removed from `data/ru/geonames.csv` in 1.2.0, are restored in `data/ru/ambiguous.csv`. `зсфср` is added there next to `закавказская сфср`.
- All text files use LF line endings.
- README: the "Recent Changes" section is replaced by a link to this file.

### Fixed

- `_legacy/data/*.csv` and `LICENSE` restored byte for byte from 1.0.0. In 1.1.0 they were rewritten with CRLF line endings.
- `data/ru/surnames.csv`: removed `cаакян`, `cимонян`, `куpьян`, `тpоян`, which had Latin `c`/`p` inside Cyrillic. Each has a correctly spelled twin in the file.
- Entry counts and dates in this file for 1.0.0–1.2.0, and the version links below.

### Removed

- `data/ru/keywords.csv`: OCR errors and glued tokens (`армянскйо`, `армянсокго`, `армянскомм`, `армянв`, `армяниназахара`, `армянскомуписателю`, `ереванеметодом`, ...); false positives (`армендарис`, `арменонвиль`, `арменопул`, `арментерос`, `арменит`, `арменкино`, ...); stems truncated from regexes (`асла`, `килики`, `эчмиадзинск`).
- `data/ru/geonames.csv`: descriptive strings with commas (`"кавказ, армения"`, `"российская империя, армения"`, ...) and `армен` (already in `names.csv`).
- `data/en/keywords.csv`: `hayk` (kept in `names.csv`).

## [1.2.0] - 2025-12-28

### Added

- **English Data Expansion**: Significantly extended the English dataset coverage:
  - `names.csv`: Added 54 entries of common Armenian given names
  - `surnames.csv`: Added 54 entries of common Armenian surnames
  - `geonames.csv`: Expanded to 79 entries (was 4)
  - `keywords.csv`: Expanded to 42 entries (was 2)

### Fixed

- `data/en/geonames.csv`: `Erivan` lowercased to `erivan`

### Removed

- `data/ru/geonames.csv`: 5 entries (`"азия, армения"`, `асср`, `веди`, `фиолетово`, `фонтан`)

## [1.1.0] - 2025-12-26

**Breaking:** files moved from `data/*.csv` to `data/ru/*.csv`, and the columns changed from `ru,en,am,category` to `value,category`. The English translations moved to `data/en/`; the empty `am` column was dropped.

### Added

- **Language-specific data organization**: Reorganized data files into language-specific directories (`data/ru/`, `data/en/`)
- **Russian keywords from Goskatalog**: Processed and extracted keywords from `_legacy/goskatalog/` files:
  - 223 geonames (cities, regions, historical places, geographic features)
  - 107 keywords (word forms from `armenian.txt` and terms from `patterns.txt`)
  - 51 names (historical figures and Armenian first names)
  - 41 midnames (patronymics)
- **English data**: `data/en/geonames.csv` (4 entries) and `data/en/keywords.csv` (2 entries)
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
- **CSV format**: Replaced the `ru,en,am,category` columns with `value,category`
- **README.md**: Complete rewrite with new structure, recent changes, and contribution guidelines

### Fixed

- Fixed typo in the category of `армяне` (changed "ketword" to "keyword")
- Removed duplicate entries in English keywords file

### Removed

- Old flat data structure files (moved to `_legacy/data/`)

## [1.0.0] - 2023-09-08

### Added

- Initial release of Armenian keywords dataset
- Flat `data/` directory with columns `ru,en,am,category` (Russian value, English and Armenian translations):
  - `geonames.csv` - 120 geographic names
  - `keywords.csv` - 3 common keywords, the only file with English translations (`armenian`, `armenians`)
  - `names.csv` - 27 first names
  - `surnames.csv` - 3652 family names
  - `midnames.csv` - 32 middle names/patronymics
- The `am` column is empty in all files
- Basic README.md documentation
- LICENSE file

[Unreleased]: https://github.com/opendataam/armenian-keywords/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/opendataam/armenian-keywords/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/opendataam/armenian-keywords/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/opendataam/armenian-keywords/releases/tag/v1.0.0
