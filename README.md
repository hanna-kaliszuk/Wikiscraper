# WikiScraper & Language Analyzer

A Python command-line application for scraping data from wiki articles and performing statistical analysis based on word frequency.

> Final project for **Kurs Pythona** (Python Course), winter semester 2025/26, University of Warsaw.

## What is WikiScraper?

WikiScraper is a command-line tool that retrieves and analyzes data from wiki articles.

The application combines web scraping with text analysis. It can extract article summaries, parse HTML tables, count word occurrences, recursively crawl related articles, and compare the vocabulary of scraped content with general language corpora.

The project was designed as a final assignment for the Python course and focuses on practical use of Python libraries for HTTP requests, HTML parsing, data processing, statistical analysis, and visualization.

## Features

- Fetching introductory paragraphs from wiki articles
- Extracting selected HTML tables and saving them as CSV files
- Counting word occurrences across articles
- Storing accumulated word-frequency data in JSON format
- Recursive crawling of internal wiki links
- Configurable crawling depth and delay between requests
- Relative word-frequency analysis
- Comparing article vocabulary with general language frequency data
- Generating frequency charts
- Unit tests without network requests
- End-to-end integration testing
- Jupyter Notebook analysis of the language detection approach

## Technologies

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

## Scraping

The scraper can retrieve different types of information from a selected wiki article.

### Article Summary

The `--summary` command retrieves the introductory paragraph of an article and removes HTML markup.

```bash
python wiki_scraper.py --summary "phrase"
```

### HTML Tables

A selected table can be extracted from an article and saved as a CSV file.

The user can specify:

- which table to extract,
- whether the first row should be treated as a header.

```bash
python wiki_scraper.py --table "phrase" --number n [--first-row-is-header]
```

Tables are parsed from the article HTML and processed using `pandas`.

## Word Frequency Analysis

The application can count word occurrences in wiki articles and maintain the results in a JSON file.

```bash
python wiki_scraper.py --count-words "phrase"
```

The collected data can be used for further statistical analysis of the vocabulary appearing in the scraped articles.

## Recursive Crawling

WikiScraper also supports automatically following internal links and processing multiple related articles.

```bash
python wiki_scraper.py --auto-count-words "phrase" --depth n --wait t
```

The crawler allows the maximum depth and delay between requests to be configured.

The delay is intentionally configurable to avoid sending requests too frequently to the target website.

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

## Relative Word Frequency

The project includes an analysis comparing word frequencies in scraped articles with frequencies from general language corpora.

```bash
python wiki_scraper.py --analyze-relative-word-frequency \
    --mode "mode" \
    [--chart "file/path.png"]
```

Two analysis modes are available:

- `article` — ranks words according to their frequency in the scraped wiki content
- `language` — ranks words according to their frequency in the reference language corpus

The number of displayed words can also be configured.

The resulting data can optionally be visualized as a chart.

## Analysis Notebook

The repository contains `analysis.ipynb`, a Jupyter Notebook presenting a more detailed investigation of the language analysis performed by the project.

The notebook is used to explore the effectiveness of the language detection method and visualize the resulting data.

## Testing

The project contains both unit and integration tests.

### Unit Tests

Unit tests verify individual components of the scraper without making network requests.

Run them with:

```bash
python tests.py
```

### Integration Test

The integration test verifies the scraper as a complete system using a local dummy HTML file.

This allows the main scraping workflow to be tested without depending on an external wiki website.

Run it with:

```bash
python integration_test.py
```

## Installation

The project requires Python and the libraries listed in `requirements.txt`.

Create and activate a virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Alternatively, the dependencies can be installed directly with:

```bash
pip install -r requirements.txt
```

## Running

The main program is executed from the command line:

```bash
python wiki_scraper.py <arguments>
```

For example:

```bash
python wiki_scraper.py --summary "Python"
```

or:

```bash
python wiki_scraper.py --count-words "Python"
```

## Project Structure

```text
.
├── analysis.ipynb          # Jupyter Notebook with language analysis
├── analyzer.py             # Word-frequency analysis
├── integration_test.py     # End-to-end tests
├── requirements.txt        # Python dependencies
├── tests.py                # Unit tests
├── wiki_scraper.py         # Main scraper and CLI
└── README.md
```

### Implementation

- `wiki_scraper.py` — command-line interface, HTTP requests, HTML parsing, article processing, and recursive crawling
- `analyzer.py` — word-frequency analysis and comparison with language corpora
- `tests.py` — unit tests for individual components
- `integration_test.py` — end-to-end testing using local HTML data
- `analysis.ipynb` — exploratory analysis and visualization

## Useful Commands

### Install dependencies

```bash
pip install -r requirements.txt
```

### Fetch an article summary

```bash
python wiki_scraper.py --summary "Python"
```

### Extract a table

```bash
python wiki_scraper.py --table "Python" --number 1
```

### Count words

```bash
python wiki_scraper.py --count-words "Python"
```

### Crawl related articles

```bash
python wiki_scraper.py --auto-count-words "Python" --depth 2 --wait 1
```

### Analyze relative word frequency

```bash
python wiki_scraper.py --analyze-relative-word-frequency \
    --mode article \
    --count 20
```

### Run unit tests

```bash
python tests.py
```

### Run integration tests

```bash
python integration_test.py
```

## Notes

- The application operates from the command line.
- Scraped word-frequency data is stored separately from the source code.
- Recursive crawling should use a reasonable delay between requests.
- Integration tests use local HTML data rather than relying on an external website.
- The project includes both automated tests and exploratory data analysis.
- Data scraped from Bulbapedia is subject to the source website's licensing terms.

## License

The project code is distributed under the **MIT License**.

Data originating from Bulbapedia is subject to the **CC BY-NC-SA 2.5** license.

## Course

This project was developed as a final assignment for the **Kurs Pythona** (Python Course) at the University of Warsaw during the Winter Semester 2025/26.