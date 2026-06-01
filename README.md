# YouTube Channel Analytics Pipeline

> MSc Artificial Intelligence - Programming for Data Analysis (B9AI001 · CA02) | Dublin Business School
---

## Project Overview

This project implements an end-to-end **YouTube Channel Analytics Data Pipeline** that acquires, processes, analyses, and stores YouTube data using the **YouTube Data API v3** and **web scraping**. The pipeline automatically collects channel metadata, video statistics, and about-page content, then transforms raw data into structured analytical features including **SEO scores**, **engagement metrics**, and **content clusters**.

Built as part of the **Programming for Data Analysis (B9AI001 · CA02)** module at Dublin Business School.

---

## Pipeline Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    DATA ACQUISITION                      │
│  YouTube Data API v3  ──►  Channel Info, Videos, Stats  │
│  Web Scraper (BeautifulSoup)  ──►  About Page Content   │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                   PREPROCESSING                          │
│  Text Cleaning  ──►  Stopword Removal  ──►  Lemmatisation│
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                  FEATURE ENGINEERING                     │
│  SEO Scoring  │  Engagement Metrics  │  TF-IDF Clustering│
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                    STORAGE (SQLite)                      │
│  channels  │  videos  │  seo_scores  │  clusters        │
└─────────────────────────────────────────────────────────┘
```

---

## Key Features

### Data Acquisition
- **YouTube Data API v3** - searches channels by keyword, retrieves channel metadata (subscribers, views, video count, country), and fetches detailed video statistics (likes, comments, views, tags)
- **Web Scraper** - scrapes YouTube channel About pages using `requests` + `BeautifulSoup`, extracting emails, external links, and channel descriptions
- **Pagination support** - handles multi-page API responses for comprehensive data collection

### Preprocessing
- URL removal, emoji stripping, punctuation cleaning
- NLTK-based stopword removal and lemmatisation
- Batch text cleaning pipeline for scalable processing

### Feature Engineering
- **SEO Scoring** - evaluates title length, keyword density, tag relevance, and description quality against YouTube best practices
- **Engagement Metrics** - computes like rate, comment rate, and upload frequency per channel
- **TF-IDF Clustering** - uses `scikit-learn` KMeans to group channels by content niche based on text similarity

### Database Storage (SQLite)
Four structured tables:

| Table | Contents |
|---|---|
| `channels` | Channel ID, name, subscribers, views, cleaned descriptions |
| `videos` | Video ID, title, tags, likes, comments, views |
| `seo_scores` | SEO title score, keyword density, TF-IDF top words |
| `clusters` | Channel cluster label and niche name |

### Testing
- Unit tests for key transformation functions (text cleaning, SEO scoring, engagement calculation)
- Integration test validating end-to-end pipeline: API acquisition → preprocessing → SQLite storage
  
---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.10+ |
| Data Acquisition | YouTube Data API v3, Requests, BeautifulSoup4 |
| NLP & Preprocessing | NLTK (stopwords, lemmatisation), Regex |
| Feature Engineering | Scikit-learn (TF-IDF, KMeans), Pandas |
| Storage | SQLite3 |
| Environment | Google Colab, python-dotenv |
| Testing | Python `unittest` |

---

## How to Run

### Option 1 - Google Colab (Recommended)
1. Open `CA02_YouTube_Pipeline.ipynb` in Google Colab
2. Add your YouTube Data API key to the `.env` cell
3. Click **Runtime → Run all**

> Get a free YouTube Data API v3 key at [console.cloud.google.com](https://console.cloud.google.com/)

### Option 2 - Local
```bash
# Clone the repo
git clone https://github.com/AyeshSharuka/programming-for-data-analysis-ca02.git
cd programming-for-data-analysis-ca02

# Install dependencies
pip install -r requirements.txt

# Add your API key to .env
echo "YOUTUBE_API_KEY=your_key_here" > .env

# Run the notebook
jupyter notebook CA02_YouTube_Pipeline.ipynb
```

---

## Environment Variables

Create a `.env` file in the root directory:

```env
YOUTUBE_API_KEY=your_youtube_api_key_here
DATABASE_PATH=./data/youtube_pipeline.db
USER_AGENT=youtube-pipeline/1.0 (your_email@example.com)
```

---

## Key Dependencies

```
google-api-python-client
beautifulsoup4
nltk
scikit-learn
pandas
python-dotenv
lxml
requests
```

Full list in `requirements.txt`.

---

## Ethical Considerations

- Data is collected only from **publicly available** YouTube channel pages and API endpoints
- Web scraping follows YouTube's `robots.txt` and uses a descriptive `User-Agent` header
- No private or authenticated user data is collected
- API usage complies with YouTube Data API v3 Terms of Service and quota limits

---

## Author

**Ayesh Sharuka** 
MSc Artificial Intelligence - Dublin Business School
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Ayesh%20Sharuka-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ayesh-sharuka-34065b204/)

---

## 📄 License

This project is submitted for academic assessment at Dublin Business School.
