# YouTube Video Downloader & Amharic Comment Sentiment Analysis

An exploratory NLP project that combines YouTube video downloading with sentiment analysis of YouTube comments using a pretrained Amharic sentiment classification model.

The project focuses on analyzing Ethiopian-language social media content, particularly comments written in **Amharic (Ge'ez script), English, and Romanized Amharic** (Amharic written using Latin characters).

## Overview

Social media platforms contain valuable user-generated information that can provide insights into public opinions, reactions, and discussions. However, analyzing Ethiopian-language social media content presents challenges due to language diversity, code-switching, and limited NLP resources.

This project explores the use of pretrained NLP models to classify the sentiment of YouTube comments and provides functionality for downloading YouTube videos using `yt-dlp`.

## Features

### 1. YouTube Video Downloading
- Downloads the best available video and audio streams using `yt-dlp`.
- Automatically merges video and audio into MP4 format.
- Includes retry handling for download failures.
- Saves downloaded videos in a dedicated `videos/` directory.

### 2. Amharic Sentiment Analysis
- Uses a pretrained Amharic sentiment classification model developed by the Language Technology group at the University of Hamburg.
- Processes YouTube comments using the Flair NLP framework.
- Classifies comments into:
  - **POSITIVE**
  - **NEUTRAL**
  - **NEGATIVE**
- Provides confidence scores for model predictions.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Jupyter Notebook | Development and experimentation |
| yt-dlp | YouTube video downloading |
| Flair | NLP and sentiment classification |
| Pandas | Data handling and processing |
| wget | Downloading the pretrained model |
| FFmpeg | Merging video and audio streams |

## Installation

### Requirements

- Python 3.9+
- FFmpeg
- Jupyter Notebook or Google Colab

Install the required Python packages:

```bash
pip install -U yt-dlp flair wget pandas
```

Install FFmpeg if it is not already available on your system.

An optional JavaScript runtime such as Deno can also be used with yt-dlp for YouTube extraction compatibility.

## Usage

### 1. Download YouTube Videos

The notebook uses `yt-dlp` to download videos.

```python
download_video("https://www.youtube.com/watch?v=<VIDEO_ID>")
```

Videos are saved in the `./videos/` directory.

**Download configuration:**

| Parameter | Configuration |
|---|---|
| Format | `bestvideo+bestaudio/best` |
| Output format | MP4 |
| Retries | 5 |
| Fragment retries | 5 |

### 2. Amharic Comment Sentiment Analysis

The sentiment analysis component uses a pretrained Flair model.

First, load the required libraries and download the model:

```python
import wget
from flair.models import TextClassifier
from flair.data import Sentence

model_url = "http://ltdata1.informatik.uni-hamburg.de/amharic/taskmodels/sent/final-model.pt"

model_path = wget.download(model_url)
classifier = TextClassifier.load(model_path)
```

Prepare a Pandas DataFrame containing YouTube comments in a column named `Comment`.

```python
for text in df["Comment"]:
    sentence = Sentence(text)
    classifier.predict(sentence)
    print(sentence.labels)
```

**Example prediction:**

```text
[NEUTRAL (0.7323)]
```

Each prediction includes a sentiment label and its confidence score.

> **Note:** The notebook does not currently include the YouTube comment collection pipeline. Comments must be supplied separately, for example through the YouTube Data API v3.

## Observations and Limitations

During experimentation, several limitations were observed:

- **Empty Predictions:** Some short or emoji-only comments return no sentiment labels.
- **Multiple Predictions:** Certain comments receive more than one sentiment label.
- **Language Limitations:** The pretrained model is designed for Amharic and does not reliably classify English or Romanized Amharic comments.
- **Text Preprocessing:** HTML entities, links, and formatting tags may affect classification results.
- **Duplicate Comments:** Repeated comments can appear in the dataset.
- **Evaluation Limitations:** No manually labeled ground-truth dataset was available, so formal evaluation metrics such as accuracy, precision, recall, and F1-score were not calculated.

These observations highlight the challenges of applying existing NLP models to multilingual and code-switched Ethiopian social media content.

## Future Improvements

Potential improvements include:

- Implementing text cleaning and HTML entity removal.
- Adding language and script detection to distinguish Amharic, English, and Romanized Amharic.
- Exploring multilingual and language-specific sentiment classification models.
- Improving prediction handling by selecting the highest-confidence label.
- Removing duplicate comments and handling empty predictions.
- Building a manually annotated dataset for quantitative model evaluation.
- Integrating YouTube comment collection into the existing pipeline.

## Responsible Use

- **Copyright and Terms of Service:** Download and analyze only content you have permission to use, and follow YouTube's applicable terms and copyright requirements.
- **Privacy:** Avoid publishing personal information, usernames, or identifiable comments without appropriate permission.
- **Model Reliability:** Predictions are experimental and should not be treated as definitive judgments about individuals or their opinions.

## Repository Structure

```text
.
├── youtube_scrapping.ipynb   # Video downloading and sentiment analysis
├── videos/                   # Downloaded videos (not tracked)
├── requirements.txt          # Project dependencies
├── .gitignore                # Excluded files
└── README.md
```

The downloaded videos and pretrained model files should be excluded from version control using `.gitignore`.

## Acknowledgements

- [yt-dlp](https://github.com/yt-dlp/yt-dlp) – YouTube video downloading.
- [Flair NLP](https://github.com/flairNLP/flair) – Natural Language Processing framework.
- [University of Hamburg – Language Technology Group](http://ltdata1.informatik.uni-hamburg.de/) – Pretrained Amharic sentiment classification model.

## Author

**Elshaday Desalegn Asfaw**

Research Interests: Natural Language Processing, Sentiment Analysis, Low-Resource Languages, and Ethiopian Language Technologies.

