# TTS Benchmark Results

Prepared: July 9, 2026

## Executive Summary

This repository now includes the generated TTS voice samples and benchmark result files from the local text-to-speech evaluation.

The current benchmark ranking identifies **Audar TTS V1 Flash** as the strongest self-hosted option across Arabic, English, mixed-language support, voice cloning, latency, and resource usage categories.

## Included Materials

Generated voice samples are stored in:

```text
tts_benchmark_results/outputs/
```

Benchmark reports are stored in:

```text
tts_benchmark_results/reports/
```

Key report files:

- `tts_benchmark_results/reports/final_comparison.csv`
- `tts_benchmark_results/reports/final_comparison.xlsx`
- `tts_benchmark_results/reports/rankings.json`

## Main Ranking Result

According to `rankings.json`, **Audar TTS V1 Flash** ranked best in these categories:

- Best Arabic Quality
- Best English Quality
- Best Mixed Language Support
- Best Voice Cloning
- Lowest Latency
- Lowest Resource Usage
- Best Commercial Self-Hosted Option

## Audar TTS V1 Flash Summary

Model:

```text
Audar TTS V1 Flash
```

License:

```text
AudarAI Open License v1.0
```

Commercial use:

```text
Yes
```

Supported scenarios:

- Arabic
- English
- Mixed Arabic-English
- Voice cloning
- Self-hosted deployment

Measured benchmark summary:

| Metric | Value |
|---|---:|
| Inference time | 42.2105 sec |
| Audio duration | 16.18 sec |
| Real-time factor | 4.9744 |
| RAM usage | 2021.7695 MB |
| Output size | 776684 bytes |

## Voice Sample Folders

The uploaded voice samples include outputs from:

- Audar TTS V1 Flash
- ElevenLabs API
- Chatterbox Multilingual
- Chatterbox Turbo
- Kokoro 82M
- Piper
- Silma TTS
- Mistral Voxtral API
- Arabic Speech Synthesis MMS
- Fish Audio API

## Recommendation

For the Arabic-English assistant project:

1. Use **Audar TTS V1 Flash** as the leading self-hosted TTS candidate.
2. Keep **ElevenLabs API** as a strong hosted/API baseline for quality and speed comparison.
3. Continue testing mixed Arabic-English voice quality, because natural code-switching is the most important production requirement for this assistant.

