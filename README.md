# Armenian Keywords

Lists of Armenian and Armenia-related keywords in multiple languages. 
This repository is used to filter Armenia-related cultural objects, books, paintings, etc. from Europeana, Australian Trove, Russian electronic library, Russian Goskatalog, and other public sources of digital heritage related to Armenia.

## Data Structure

All data files are comma-separated CSV files organized by language in the `data/` directory:

```
data/
├── ru/          # Russian language data
│   ├── geonames.csv
│   ├── keywords.csv
│   ├── midnames.csv
│   ├── names.csv
│   └── surnames.csv
├── en/          # English language data
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
value,category
```

Where:
- `value` - the keyword, name, or place name
- `category` - one of: `keyword`, `geoname`, `name`, `surname`, `midname`

### Categories

- **geonames.csv** - Geographic names (cities, regions, historical places, mountains, etc.)
- **keywords.csv** - Common keywords related to Armenia and Armenian culture
- **names.csv** - First names (given names)
- **surnames.csv** - Family names (last names)
- **midnames.csv** - Middle names / patronymics

## Recent Changes

### Processing Goskatalog Data (Latest Update)

The repository has been updated with data extracted from `_legacy/goskatalog/` directory:

- **Geonames**: 225 entries extracted from `armenian_toponyms.txt` including:
  - Major cities (Ереван, Гюмри, Ванадзор, etc.)
  - Historical regions (Карабах, Арцах, Киликия, etc.)
  - Geographic features (Арарат, Севан, etc.)
  - Historical and alternative names

- **Keywords**: 110 entries extracted from `patterns.txt` and filtered from `armenian.txt`:
  - Basic Armenia terms (армения, армянин, армянский, etc.)
  - Cultural and religious terms (вардапет, католикос, etc.)
  - Historical terms (урарту, спюрк, etc.)
  - Filtered out false positives (бармен, жандармен, etc.)

- **Names**: 51 entries including historical figures (Тигран, Арташес, Маштоц, Месроп, etc.)

- **Midnames**: 41 entries (patronymics like арменович, арменовна, etc.)

### English Data Expansion

The English dataset has been significantly expanded to match the coverage of the Russian dataset:

- **Geonames**: Extended to 79 entries covering major cities, regions, and historical places.
- **Keywords**: Expanded to 42 entries covering cultural, historical, and key figures.
- **Names**: Added new file with 54 common Armenian given names.
- **Surnames**: Added new file with 54 common Armenian surnames (including variations).

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
value,category
armenia,keyword
armenio,keyword
armenios,keyword
armenia,keyword
armenio/a,keyword
catolicós,keyword
vardapet,keyword
urartu,keyword
cilicia,keyword
diáspora armenia,keyword
```

#### Spanish (data/es/geonames.csv)
```csv
value,category
armenia,geoname
república de armenia,geoname
ereván,geoname
gyumri,geoname
vanadzor,geoname
karabaj,geoname
artsaj,geoname
ararat,geoname
sevan,geoname
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
3. Ensure category values are correct (`keyword`, `geoname`, `name`, `surname`, `midname`)
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

Historical data and source files are preserved in the `_legacy/` directory:
- `_legacy/goskatalog/` - Original Russian Goskatalog keyword lists
- `_legacy/data/` - Previous data structure

## License

See [LICENSE](LICENSE) file for details.
