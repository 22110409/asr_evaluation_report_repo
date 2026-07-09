# Arabic-English ASR Model Evaluation Report

Prepared: July 9, 2026

## Executive Summary

We evaluated several speech-to-text models for an Arabic-English voice assistant. The goal was to identify which model can handle Arabic, English, and mixed Arabic-English speech with acceptable accuracy and practical speed.

The strongest result for clean Arabic speech came from **SeamlessM4T ASR**. It produced natural Arabic text with good punctuation and wording. However, when the input mixed Arabic and English, SeamlessM4T often normalized or translated the content toward Arabic instead of preserving the exact mixed-language wording.

For true mixed Arabic-English transcription, **Faster-Whisper Large-v3 Turbo** remains the safest practical choice. It preserved English words better than the Arabic-specific models and is faster when GPU is available.

## Recommendation

Use two ASR modes depending on the product requirement:

| Use case | Recommended model | Reason |
|---|---|---|
| Arabic-only transcription | SeamlessM4T ASR | Best Arabic wording and punctuation in our tests |
| Mixed Arabic-English transcription | Faster-Whisper Large-v3 Turbo | Better code-switching and English word preservation |
| English-only transcription | NVIDIA Parakeet TDT V3 or Faster-Whisper | Parakeet was strong on English but weak on Arabic |
| Real-time assistant on CPU | Faster-Whisper small/turbo | SeamlessM4T is accurate but heavy on CPU |

## Tested Models

| Model | Model ID | Main result |
|---|---|---|
| SeamlessM4T ASR | facebook/hf-seamless-m4t-medium | Best Arabic-only result; mixed speech may be translated or normalized |
| Faster-Whisper Large-v3 Turbo | deepdml/faster-whisper-large-v3-turbo-ct2 | Best practical choice for Arabic-English code-switching |
| Faster-Whisper Large-v3 | large-v3 | Good Arabic-English transcription with GPU |
| WindyWord Arabic Lingua | WindyWord/listen-windy-lingua-ar | Good Arabic-only, weak mixed-language handling |
| NVIDIA Parakeet TDT V3 | nvidia/parakeet-tdt-0.6b-v3 | Good English, not suitable for Arabic |

## Key Test Results

### SeamlessM4T ASR

Arabic-only test:

```text
مرحباً. كيف حالك اليوم؟ أتمنى أن تكون بخير.
```

CPU inference time: 16.139 seconds

Clean Arabic audio test:

```text
مرحباً كيف حالكِ اليوم؟ أتمنى أن تكونَ بخير.
```

CPU inference time: 4.501 seconds

Mixed Arabic-English test:

```text
السلام عليكم كل واحد. اليوم نحن نختبر مساعد متعددة اللغات. أريد التأكد أن النظام يستطيع فهم العربية والإنجليزية بنفس الكفاءة. Can You Schedule a Meeting for Tomorrow at HALEAYAMN Send Me The Details by E-mail. بعد ذلك أرسل لي ملخصاً قصيراً باللغة العربية مع الاحتفاظ بالمصطلحات التقنية باللغة الإنجليزية.
```

CPU inference time: 21.911 seconds

Clean mixed audio test:

```text
مرحبا بكم جميعا، مرحبا بكم في معيار الكلام AI.
```

CPU inference time: 3.611 seconds

Assessment: SeamlessM4T is very strong for Arabic output. The main limitation is that it is not ideal when exact Arabic-English mixed transcription must be preserved.

### Faster-Whisper Large-v3 Turbo

Mixed Arabic-English test:

```text
مرحبا كيف تحال شو الأخبار هاي هي تست للصوت عشان تسكت إذا هو بكتر إيش بيك اللغة العربية with English Thank you
```

GPU inference time: 3.689 seconds

Assessment: The Arabic wording has some errors, but the model preserved English terms better than the Arabic-only models. This makes it more suitable for a real assistant where users mix Arabic and English naturally.

### WindyWord Arabic Lingua

Arabic-only test:

```text
مرحبا كيف حالك اليوم اتمني ان تكون بخير
```

CPU inference time: 31.602 seconds

Mixed Arabic-English test:

```text
السلام عليكم جميعا اليوم نستمتع باستخدام استخدام الانجليزيون التعليقات العربيه التعليقات العربيه اريد التاكد ان النظام يستطيع فهم العربيه والانجليزيه بنفس الكفاءه هل يمكن ان تشتتل امتلاك لتومورو في امساء و ترسل لي التفاصيل بايميل بعد ذلك ارسلي لي ملخصا قصيرا باللغه العربيه مع الاحتفاظ بالمصطلحات التقنيه باللغه الانجليزيه
```

CPU inference time: 68.268 seconds

Assessment: Good Arabic-only direction, but weak for mixed Arabic-English. English words were often converted into Arabic-sounding words.

### NVIDIA Parakeet TDT V3

English test:

```text
Hello, how are you today? I hope you are doing well.
```

CPU inference time: 16.011 seconds

Arabic test:

```text
Marahaba, Kif Hala Kilium, Atamana antakuna bihair.
```

CPU inference time: 16.98 seconds

Mixed test:

```text
Asalamu Alaikum everyone. Today we are testing a multilingual AI assistant. Uridu taakudu annan nidamiya statiyo fahmala arabiya one inglisiya bi nafsil kafa'a. Can you schedule a meeting for tomorrow at Hali am and send me the details by email? Badadalik arselili mullachasan kasiran billuh al-arabia, ma'alehtifadi bilmustalahatit takaniyya billuhal inghliziya.
```

CPU inference time: 19.3 seconds

Assessment: Strong for English, but it transliterates Arabic instead of producing Arabic script. Not recommended for Arabic or Arabic-English assistant use.

## Business Conclusion

SeamlessM4T is the best candidate when the required output is Arabic text. It produced the most professional Arabic transcription in the tests.

For a bilingual Arabic-English voice assistant, the main risk is code-switching. Users may say Arabic sentences with English terms such as "meeting", "email", "API", "GPU", or times such as "10 AM". SeamlessM4T may translate or normalize these terms, while Whisper is more likely to preserve them.

The recommended production approach is:

1. Use **Faster-Whisper Large-v3 Turbo** as the default ASR model for mixed Arabic-English speech.
2. Add **SeamlessM4T ASR** as an optional Arabic-only mode when Arabic text quality matters more than preserving English terms.
3. Avoid **NVIDIA Parakeet TDT V3** for Arabic use cases.
4. Avoid **WindyWord Arabic Lingua** for mixed-language use cases unless it is fine-tuned or improved for code-switching.

## Notes and Limitations

These tests were qualitative and based on available benchmark audio samples. We did not calculate formal WER/CER because a normalized ground-truth transcript was not prepared for every file.

Most SeamlessM4T and WindyWord tests ran on CPU, so GPU performance may be faster. Real-time production use should be tested again on the final hardware.

## Raw Result Files

The raw JSON outputs are included in:

```text
director_package/raw_results/
```

