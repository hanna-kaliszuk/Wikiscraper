# WikiScraper & Language Analyzer

A Python command-line application for scraping wiki articles, processing their content, and analyzing word-frequency data.

---

## What is WikiScraper?

WikiScraper is a single command-line web scraping, text processing, statistical analysis, and data visualization application.

The scraper can retrieve article summaries, extract HTML tables, count word occurrences, and recursively crawl related wiki articles. The collected word-frequency data can then be analyzed and compared with frequencies from general language corpora.

The project follows the pipeline:

```text
Wiki article
     │
     ▼
HTTP request
     │
     ▼
HTML parsing
     │
     ├───────────────┐
     ▼               ▼
Summary          HTML tables
     │               │
     ▼               ▼
Word extraction   Pandas / CSV
     │
     ▼
Word-frequency data
     │
     ▼
Statistical analysis
     │
     ├───────────────┐
     ▼               ▼
Wiki frequency   Language corpus
     │               │
     └───────┬───────┘
             ▼
       Comparison / charts
```

---

## Key Features

### Article scraping

- Fetching introductory paragraphs from wiki articles
- Removing HTML markup from extracted summaries
- Extracting selected HTML tables
- Saving extracted tables as CSV files

### Word-frequency analysis

- Counting word occurrences across articles
- Storing accumulated word-frequency data in JSON format
- Calculating relative word frequencies
- Comparing scraped vocabulary with general language frequency data
- Ranking words according to different frequency sources
- Generating frequency charts

### Recursive crawling

- Following internal wiki links automatically
- Configurable crawling depth
- Configurable delay between requests

The crawling process can be visualized as:

```text
Starting article
      │
      ├── linked article
      │      ├── linked article
      │      └── linked article
      │
      └── linked article
             └── linked article
```

The depth parameter determines how many levels of links are followed from the starting article.

---

## Scraping

The main scraper is implemented in `wiki_scraper.py` and provides several command-line operations.

### Article Summary

Retrieve the introductory paragraph of an article:

```bash
python wiki_scraper.py --summary "Python"
```

### HTML Tables

Extract a selected table from an article:

```bash
python wiki_scraper.py --table "Python" --number 1
```

The command also supports treating the first row of the table as a header.

The extracted HTML table is parsed and converted into a `pandas` DataFrame before being saved as CSV.

### Word Counting

Count word occurrences in an article:

```bash
python wiki_scraper.py --count-words "Python"
```

The collected data can be accumulated in a JSON file and used for further analysis.

---

## Recursive Crawling

WikiScraper can automatically follow internal links and collect word-frequency data from multiple related articles.

```bash
python wiki_scraper.py --auto-count-words "Python" --depth 2 --wait 1
```

Two parameters control the crawling process:

- `--depth` — maximum number of link levels to follow
- `--wait` — delay between requests

The configurable delay allows requests to be spaced out instead of being sent continuously to the target website.

---

## Relative Word Frequency

The project includes an analysis comparing word frequencies in scraped wiki content with frequencies from a general language corpus.

```bash
python wiki_scraper.py --analyze-relative-word-frequency \
    --mode article \
    --count 20
```

Two analysis modes are available:

- `article` — ranks words according to their frequency in the scraped wiki content
- `language` — ranks words according to their frequency in the reference language corpus

The results can also be visualized as a chart:

```bash
python wiki_scraper.py --analyze-relative-word-frequency \
    --mode article \
    --chart "output.png"
```

The analysis functionality is implemented separately in `analyzer.py`.

---

## Analysis Notebook

The repository contains `analysis.ipynb`, a Jupyter Notebook used for a more detailed investigation of the language analysis performed by the project.

The notebook explores the language detection approach and visualizes the resulting data.

---

## Testing

The project contains both unit and integration tests.

### Unit Tests

Unit tests verify individual components of the scraper without making network requests.

The tests cover functionality such as:

- article URL generation,
- article summary extraction,
- internal link extraction,
- HTML table processing.

Run the tests with:

```bash
python tests.py
```

### Integration Test

The integration test verifies the scraper workflow using a local HTML fixture rather than an external website.

This allows the scraping process to be tested without depending on a live wiki.

Run it with:

```bash
python integration_test.py
```

---

## Project Structure

```text
.
├── analysis.ipynb          # Jupyter Notebook with language analysis
├── analyzer.py             # Word-frequency analysis
├── integration_test.py     # Integration test using local HTML data
├── requirements.txt        # Python dependencies
├── tests.py                # Unit tests
├── wiki_scraper.py         # Main scraper and command-line interface
└── README.md
```

### Implementation

| File | Responsibility |
|---|---|
| `wiki_scraper.py` | Command-line interface, HTTP requests, HTML parsing, article processing, and recursive crawling |
| `analyzer.py` | Word-frequency analysis and comparison with language corpora |
| `tests.py` | Unit tests for individual scraper components |
| `integration_test.py` | Integration testing using local HTML data |
| `analysis.ipynb` | Exploratory analysis and visualization |

---

## Technologies Used

### Language and Libraries

- Python
- `requests`
- `BeautifulSoup`
- `pandas`
- `wordfreq`
- `matplotlib`
- `seaborn`
- `lxml`

### Data Formats

- HTML
- CSV
- JSON
- Jupyter Notebook (`.ipynb`)

### Testing

- Python unit tests
- Integration testing with local HTML fixtures

---

## Running Locally

### 1. Clone the repository

```bash
git clone https://github.com/hanna-kaliszuk/Wikiscraper.git
cd Wikiscraper
```

### 2. Create a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the application

The main program is executed from the command line:

```bash
python wiki_scraper.py <arguments>
```

For example:

```bash
python wiki_scraper.py --summary "Python"
```

---

## Context

This project was developed as a final assignment for the **Kurs Pythona** (Python Course) at the **University of Warsaw** during the Winter Semester 2025/26.

The project focuses on practical use of Python for:

- HTTP communication,
- HTML parsing,
- data processing,
- statistical analysis,
- data visualization,
- automated testing.
---

## Notes

- The application operates from the command line.
- Scraped word-frequency data is stored separately from the source code.
- Recursive crawling should use a reasonable delay between requests.
- Integration tests use local HTML data rather than relying on an external website.
- Data scraped from Bulbapedia is subject to the source website's licensing terms.

## License

The project code is distributed under the **MIT License**.

Data originating from Bulbapedia is subject to the **CC BY-NC-SA 2.5** license.
