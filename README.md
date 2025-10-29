# YouTube Sentiment Analysis

Analyze the sentiment of YouTube comments using Python. This project explores basic NLP techniques to classify comments as positive, neutral, or negative, and visualizes frequently used words with word clouds.

## Overview

This repository contains a Jupyter notebook that:
- Loads a large corpus of YouTube comments
- Cleans and prepares the data (handles nulls and mixed dtypes)
- Computes comment sentiment using TextBlob polarity (−1 to 1)
- Explores distributions and samples
- Generates word clouds for qualitative insights

## Tech Stack

- Python 3.8+
- Pandas, NumPy
- Seaborn, Matplotlib
- TextBlob (for sentiment polarity)
- WordCloud (for visualization)

## Dataset

- Expected CSV file: `UScomments.csv` (columns typically include `video_id`, `comment_text`, `likes`, `replies`).
- Place the CSV in a convenient local path and update the path inside the notebook before running.
- Suggested sources: public datasets on Kaggle or data exported via the YouTube API. Ensure you have the right to use and share the data.

## Project Structure

```
YouTube-Sentiment_Analysis/
├─ README.md
└─ YOU TUBE SENTIMENT ANALYSIS PROJECT.ipynb
```

## Setup

1. Create and activate a virtual environment (recommended):

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install pandas numpy seaborn matplotlib textblob wordcloud
python -m textblob.download_corpora
```

3. (Optional) If using Jupyter locally, install:

```bash
pip install notebook
jupyter notebook
```

## Usage

1. Open the notebook `YOU TUBE SENTIMENT ANALYSIS PROJECT.ipynb`.
2. Update the CSV path to your local `UScomments.csv` file.
3. Run cells sequentially.

Minimal example of computing polarity with TextBlob:

```python
from textblob import TextBlob
TextBlob("This video is absolutely amazing!").sentiment.polarity  # returns value in [-1, 1]
```

## Methodology

- **Sentiment Metric**: TextBlob polarity in \([-1, 1]\)
  - Negative (< 0), Neutral (≈ 0), Positive (> 0)
- **Processing**:
  - Drop missing `comment_text`
  - Loop through comments (or vectorize) to compute polarity
  - Append polarity as a new column for downstream analysis
- **Visualization**:
  - Word clouds for positive/high-polarity comments
  - Distributions via histograms or KDE plots

## Results and Interpretation

- Inspect the distribution of polarity scores to understand overall sentiment.
- Sample top positive/negative comments for qualitative insights.
- Word clouds highlight commonly used tokens; consider basic cleaning (lowercasing, stopword removal) for better clarity.

## Troubleshooting

- Pandas warnings about `error_bad_lines` deprecation: use the modern `on_bad_lines` parameter, e.g. `pd.read_csv(..., on_bad_lines="skip")`.
- Mixed dtypes (`DtypeWarning`): add `low_memory=False` or specify `dtype` per column.
- `SettingWithCopyWarning`: prefer `.loc` assignment, e.g. `df.loc[idx, "Polarity"] = values`.
- Large CSVs: consider chunked loading with `pd.read_csv(..., chunksize=...)`.

## Notes and Limitations

- TextBlob uses a lexicon-based approach; results may be simplistic on sarcasm, slang, or domain-specific language.
- For production-grade sentiment analysis, consider transformer-based models (e.g., fine-tuned BERT) and robust preprocessing.

## License

Specify your license here (e.g., MIT). If unspecified, the default is “all rights reserved.”

## Acknowledgements

- Inspired by publicly available YouTube comment datasets and the TextBlob library.