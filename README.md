# Armenian Keywords

Lists of Armenian and Armenia-related keywords in multiple languages. 
This repository is used to filter Armenia-related cultural objects, books, paintings, etc. from Europeana, Australian Trove, Russian electronic library, Russian Goskatalog, and other public sources of digital heritage related to Armenia.

## Data Structure

All data files are comma-separated CSV files organized by language in the `data/` directory:

```
data/
├── ru/          # Russian language data
│   ├── ambiguous.csv
│   ├── geonames.csv
│   ├── keywords.csv
│   ├── midnames.csv
│   ├── names.csv
│   └── surnames.csv
├── en/          # English language data
│   ├── ambiguous.csv
│   ├── geonames.csv
│   ├── keywords.csv
│   ├── names.csv
│   └── surnames.csv
├── hy/          # Armenian language data
│   ├── ambiguous.csv
│   ├── geonames.csv
│   ├── keywords.csv
│   ├── names.csv
│   └── surnames.csv
└── [lang]/      # Other languages (see guidelines below)
    ├── geonames.csv
    └── keywords.csv
```

### CSV File Format

All CSV files follow the same structure:

```csv
value,category,id
```

Where:
- `value` - the keyword, name, or place name
- `category` - one of: `keyword`, `geoname`, `name`, `surname`, `midname`, `suffix`
- `id` - concept key shared across languages: the English canonical form in lowercase. For example, `ереван`, `эривань`, `erivan` and `երևան` all have the id `yerevan`. Empty when no cross-language link is recorded yet.

### Categories

- **geonames.csv** - Geographic names (cities, regions, historical places, mountains, etc.)
- **keywords.csv** - Common keywords related to Armenia and Armenian culture
- **names.csv** - First names (given names)
- **surnames.csv** - Family names (last names)
- **midnames.csv** - Middle names / patronymics
- **ambiguous.csv** - Values that need context (see below)

`geonames.csv` and `names.csv` hold base (nominative) forms. Russian `keywords.csv` also holds inflected forms and pre-reform spellings (`армянскаго`, `армянскій`, `арменія`) of Armenia-related words.

### Ambiguous Values

`ambiguous.csv` uses the same format and the same categories. It holds values that are Armenia-related but match too much unrelated content when used alone:

- places outside Armenia and Artsakh, or homonyms of places elsewhere (`армавир` is also a city in Krasnodar Krai, `тифлис`, `kars`, `nakhichevan`)
- toponyms with large non-Armenian contexts (`карабах`: Karabakh carpets; `киликия`, `cilicia`: Roman Cilicia)
- words or names common in other languages and cultures (`david`, `cher`, `gregorian`, `лаваш`, `ашот`, `баян`, `крестьян`)
- surname suffixes, category `suffix`, matched at the end of a word (`ян`, `янц`, `уни`)

Do not use these values alone as a filter. Require another match from the main files in the same record. Most Russian entries come from the exclusion lists and the "when Armenian context" notes in `_legacy/goskatalog/patterns.txt` and `armenian_toponyms.txt`.

## Matching

The lists are designed for whole-word matching:

1. **Normalize the text.** Convert it to lowercase. In Russian text, replace `ё` with `е`. In Armenian text, replace `եւ` with `և` (classical and Western Armenian spelling).
2. **Match whole words and phrases.** A value matches only between word boundaries. Never match it as a substring: `армен` occurs inside `бармен`, `кармен`, `казарменный`. Values can contain spaces, hyphens and periods (`оз. севан`, `нор-джуга`, `арм. сср`). Match them as literal phrases.
3. **Do not stem.** Russian `keywords.csv` lists inflected forms explicitly. A few values are catalog abbreviations (`армянск`, `ереванск`).
4. **Match `suffix` values at the end of a word.** `ян` matches `саргсян`.
5. **Use `ambiguous.csv` only with context.** Count a match from it only together with a match from the main files in the same record.

## Changes

See [CHANGELOG.md](CHANGELOG.md).

## Adding Keywords in Other Languages

To add Armenia-related keywords in other languages (Spanish, French, German, Italian, etc.), follow these guidelines:

### 1. Create Language Directory

Create a new directory under `data/` using the ISO 639-1 language code:

```bash
mkdir -p data/es  # Spanish
mkdir -p data/fr  # French
mkdir -p data/de  # German
mkdir -p data/it  # Italian
# etc.
```

### 2. Create CSV Files

Create the appropriate CSV files for your language. At minimum, create:
- `geonames.csv` - Geographic names
- `keywords.csv` - Common keywords

Optionally add:
- `names.csv` - First names (if applicable)
- `surnames.csv` - Family names (if applicable)
- `midnames.csv` - Middle names/patronymics (if applicable)
- `ambiguous.csv` - Values that need context (if applicable)

Fill the `id` column with the English canonical form of the concept, as used in `data/en/`. Leave it empty if there is no English equivalent.

### 3. Translation Guidelines

#### Geonames (Geographic Names)

Include:
- **Country name** and variations:
  - Spanish: `Armenia`, `República de Armenia`
  - French: `Arménie`, `République d'Arménie`
  - German: `Armenien`, `Republik Armenien`

- **Major cities**:
  - Spanish: `Ereván`, `Gyumri`, `Vanadzor`
  - French: `Erevan`, `Gyumri`, `Vanadzor`
  - German: `Jerewan`, `Gjumri`, `Wanadsor`

- **Historical regions**:
  - Spanish: `Karabaj`, `Artsaj`, `Cilicia`
  - French: `Karabagh`, `Artsakh`, `Cilicie`
  - German: `Bergkarabach`, `Arzach`, `Kilikien`

- **Geographic features**:
  - Spanish: `Ararat`, `Sevan`
  - French: `Ararat`, `Sévan`
  - German: `Ararat`, `Sewan`

- **Historical names** (when different from modern):
  - Spanish: `Eriván` (historical name for Ereván)
  - French: `Erivan` (historical name for Erevan)

#### Keywords

Include:
- **Basic terms**:
  - Spanish: `armenio`, `armenios`, `armenia`, `armenio/a`
  - French: `arménien`, `arméniens`, `arménienne`, `arméniennes`
  - German: `armenisch`, `Armenier`, `Armenierin`, `Armenierinnen`

- **Cultural terms**:
  - Spanish: `catolicós`, `vardapet`
  - French: `catholicos`, `vardapet`
  - German: `Katholikos`, `Vardapet`

- **Historical terms**:
  - Spanish: `Urartu`, `Cilicia`, `diáspora armenia`
  - French: `Ourartou`, `Cilicie`, `diaspora arménienne`
  - German: `Urartu`, `Kilikien`, `armenische Diaspora`

- **Language terms**:
  - Spanish: `idioma armenio`, `alfabeto armenio`
  - French: `langue arménienne`, `alphabet arménien`
  - German: `armenische Sprache`, `armenisches Alphabet`

### 4. Example Files

#### Spanish (data/es/keywords.csv)
```csv
value,category,id
armenio,keyword,armenian
armenia,keyword,armenian
armenios,keyword,armenians
armenias,keyword,armenians
catolicós,keyword,catholicos
vardapet,keyword,vardapet
diáspora armenia,keyword,armenian diaspora
```

#### Spanish (data/es/geonames.csv)
```csv
value,category,id
armenia,geoname,armenia
república de armenia,geoname,armenia
ereván,geoname,yerevan
gyumri,geoname,gyumri
vanadzor,geoname,vanadzor
alto karabaj,geoname,nagorno-karabakh
artsaj,geoname,artsakh
urartu,geoname,urartu
cilicia,geoname,cilicia
ararat,geoname,ararat
sevan,geoname,sevan
```

### 5. Quality Guidelines

- **Use lowercase** for all entries (except proper nouns if your language requires capitalization)
- **Remove duplicates** - check existing entries before adding
- **Use standard transliterations** - follow common conventions for your language
- **Include variations** - add alternative spellings and historical names
- **Filter false positives** - avoid generic terms that might match non-Armenian content
- **Maintain consistency** - use the same transliteration system throughout

### 6. Testing

After adding new language data:
1. Verify CSV files are valid (no syntax errors)
2. Check for duplicates within the file
3. Ensure category values are correct (`keyword`, `geoname`, `name`, `surname`, `midname`, `suffix`)
4. Test with sample queries to ensure keywords match relevant content

## Contribution

Contributions are welcome! Please:

1. **Fork the repository**
2. **Create a branch** for your changes
3. **Add or update** CSV files following the guidelines above
4. **Test** your changes
5. **Submit a pull request** with a description of your changes

### Priority Languages

High priority for adding keywords:
- Spanish (es)
- French (fr)
- German (de)
- Italian (it)
- Portuguese (pt)
- Turkish (tr)
- Persian/Farsi (fa)
- Arabic (ar)

## Legacy Data

Historical data and source files are preserved unchanged in the `_legacy/` directory:
- `_legacy/goskatalog/` - Original Russian Goskatalog keyword lists
- `_legacy/data/` - Data files of the 1.0.0 release (flat structure, columns `ru,en,am,category`)

## License

See [LICENSE](LICENSE) file for details.
