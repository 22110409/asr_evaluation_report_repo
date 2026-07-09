# Arabic-English Speech Evaluation Repo

STT and TTS test materials focused on Arabic-English voice assistant evaluation.

This repository contains cleaned report packages prepared for sharing with management.

## Files

- `ASR_Evaluation_Report.md` - executive report with findings, results, and recommendation.
- `TTS_Benchmark_Report.md` - summary of TTS benchmark results and uploaded voice samples.
- `model_comparison_summary.csv` - compact model comparison table.
- `raw_results/` - original JSON result files from the ASR model tests.
- `tts_benchmark_results/reports/` - TTS benchmark CSV, XLSX, and ranking files.
- `tts_benchmark_results/outputs/` - generated TTS voice samples.

## ASR Recommendation

Use **Faster-Whisper Large-v3 Turbo** as the default model for a real Arabic-English assistant.

Use **SeamlessM4T ASR** for Arabic-only transcription when Arabic text quality is the priority.

Avoid **NVIDIA Parakeet TDT V3** for Arabic use cases because it transliterates Arabic instead of producing Arabic script.

## TTS Recommendation

Use **Audar TTS V1 Flash** as the leading self-hosted TTS candidate for Arabic-English speech.

Keep **ElevenLabs API** as a hosted quality and speed baseline.
