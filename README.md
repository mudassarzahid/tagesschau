<!-- Add title image -->

# [![Tagesschau Favicon](https://www.tagesschau.de/favicon.ico)](https://www.tagesschau.de/)  Tagesschau Archive Article Dataset

[![Python 3.10](https://img.shields.io/badge/python-3.10-blue.svg?style=flat)](https://www.python.org/downloads/release/python-360/)
[![HuggingFace Datasets](https://img.shields.io/badge/huggingface-datasets-orange.svg?style=flat)](https://huggingface.co/datasets/bjoernp/tagesschau-2018-2023)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the code for scraping every article
from the Tagesschau.de archive. Find a deduplicated version of the dataset
from 01.01.2018 to 26.04.2023 [on HuggingFace](https://huggingface.co/datasets/bjoernp/tagesschau-2018-2023).

## Dataset Information

CSV structure:

| Field                   | Description                                                        |
|-------------------------|--------------------------------------------------------------------|
| `date`                  | Article date                                                       |
| `headline`              | Article headline                                                   |
| `short_headline`        | A short headline / Context                                         |
| `description`           | Article lead                                                       |
| `article_body`          | Raw article text                                                   |
| `detailed_article_body` | Article body with text objects (subhead, time, paragraph, topline) |
| `date_modified`         | Modified timestamp                                                 |
| `date_published`        | Published timestamp                                                |
| `keywords`              | List of keywords                                                   |
| `author`                | Author object                                                      |
| `publisher`             | Publisher object                                                   |
| `label`                 | Article label (e.g. interview, audio)<br/>                         |    
| `link`                  | Article link                                                       | 

Size:

The final dataset (2018-today) contains 225202 articles from 1942 days. Of these articles only
21848 are unique (Tagesschau often keeps articles in circulation for ~1 month). The total download
size is ~65MB.

Cleaning:

- Duplicate articles are removed
- Articles with empty text are removed
- Articles with empty short_texts are removed
- Articles, headlines and short_headlines are stripped of leading and trailing whitespace

More details in [`clean.py`](./clean.py).

## Usage

Install with:

```bash
pip install poetry
poetry install --no-root
```

Run with:

```bash
python scrape_tagesschau.py #--start_date=2018-01-01 --end_date=2023-01-01 --output=tagesschau.csv
```