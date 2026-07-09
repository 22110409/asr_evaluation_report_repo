# ASR Evaluation Report Repo

SST and TTS test materials focused on Arabic-English speech-to-text evaluation.

This repository contains a cleaned report package prepared for sharing with management.

## Files

- `ASR_Evaluation_Report.md` - executive report with findings, results, and recommendation.
- `model_comparison_summary.csv` - compact model comparison table.
- `raw_results/` - original JSON result files from the ASR model tests.

## Final Recommendation

Use **Faster-Whisper Large-v3 Turbo** as the default model for a real Arabic-English assistant.

Use **SeamlessM4T ASR** for Arabic-only transcription when Arabic text quality is the priority.

Avoid **NVIDIA Parakeet TDT V3** for Arabic use cases because it transliterates Arabic instead of producing Arabic script.
