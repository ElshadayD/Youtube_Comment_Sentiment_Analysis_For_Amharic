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

## Example Output

```text
Comment: ምርጥ ነው በርቱ
Sentiment: POSITIVE

Comment: አንተ ሌባ ነህ
Sentiment: NEGATIVE

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
