# YouTube Video Downloader & Amharic Sentiment Analysis

## Overview

This project combines YouTube video downloading with sentiment analysis of YouTube comments. It uses `yt-dlp` to download individual videos in high quality and a pretrained Amharic sentiment classification model from Flair to analyze comments.

The sentiment analysis supports comments written in Amharic, English, and mixed languages, as demonstrated in the sample outputs.

## Features

- Download individual YouTube videos in the best available video and audio quality.
- Merge downloaded audio and video into MP4 format.
- Analyze YouTube comments using a pretrained Amharic sentiment model.
- Predict sentiment labels: **Positive, Negative, and Neutral**.
- Display sentiment predictions and confidence scores.

## Technologies

- Python
- yt-dlp
- Flair
- PyTorch
- wget
- Pandas

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd <repository-folder>
```

Install the dependencies:

```bash
pip install yt-dlp flair wget pandas
```

For video and audio merging, install [FFmpeg](https://ffmpeg.org/).

## Usage

### 1. Download a YouTube Video

Run the downloader and enter a YouTube video URL:

```bash
python download_video.py
```

The downloaded video will be saved in the `videos/` directory.

### 2. Analyze Comment Sentiment

The sentiment analysis uses a pretrained Flair model:

```python
from flair.models import TextClassifier
from flair.data import Sentence

model_url = "http://ltdata1.informatik.uni-hamburg.de/amharic/taskmodels/sent/final-model.pt"
```

Load the model and classify comments from a Pandas DataFrame containing a `Comment` column.

The model returns sentiment labels with confidence scores.

## Example Output

```text
Comment: ምርጥ ነው በርቱ
Sentiment: POSITIVE

Comment: አንተ ሌባ ነህ
Sentiment: NEGATIVE

Comment: Interesting episode
Sentiment: NEUTRAL
```

## Notes

- The sentiment model is pretrained; this project uses it for inference rather than training a new model.
- The comment DataFrame must be prepared before running sentiment classification.
- Sentiment predictions may be inaccurate, particularly for sarcasm, mixed-language comments, transliteration, and context-dependent expressions.
- YouTube downloading should comply with YouTube's terms of service and applicable copyright laws.

## Future Improvements

- Automate YouTube comment collection.
- Save predictions and confidence scores to CSV.
- Visualize sentiment distribution.
- Add support for more Ethiopian languages.
