# ASR Benchmark for Indian Conversational Speech

Benchmarking Automatic Speech Recognition (ASR) systems for multilingual Indian conversational speech in telephony-style environments using real-world noisy audio and custom entity-extraction focused evaluation metrics.

## Overview

This project evaluates how well modern ASR systems handle:

- Hinglish / Tanglish conversational speech
- Indian accents and pronunciation drift
- Bangalore locality name extraction
- Noisy real-world mobile recordings
- Code-switching between Hindi, English, and Tamil

Instead of focusing only on traditional Word Error Rate (WER), this benchmark emphasizes **business-critical entity extraction**, specifically locality detection for blue-collar hiring workflows.


# Models Benchmarked

| Model | Type |
|---|---|
| Deepgram Nova-2 | API-based |
| OpenAI Whisper | Open-source |
| Sarvam Saarika v2.5 | Indian multilingual ASR |


# Dataset

A custom dataset of 20 self-recorded audio samples was created using a mobile phone microphone.

Features:
- Conversational speech
- Mixed Hindi / English / Tamil
- Quiet + noisy environments
- Realistic telephony-style phrasing
- Natural locality mentions

Example utterances:
- “Main JP Nagar side rehta hoon.”
- “Koramangala mein traffic bahut zyada hai.”
- “Naan Bellandur la oru dress shop pakkathula irukken.”


# Evaluation Metrics

Traditional WER was insufficient for this use-case because preserving locality entities matters more than exact grammar.

Custom metrics used:

| Metric | Purpose |
|---|---|
| Locality Detection Rate (LDR) | Measures successful locality extraction |
| Cross-Model Agreement Rate (CMAR) | Measures transcript similarity across ASRs |
| Transcript Entropy | Measures instability/ambiguity in outputs |
| Hallucination Risk | Detects fabricated or unrelated outputs |

This evaluation is intended as a practical stress-test rather than a statistically rigorous benchmark.


# Key Results

| Model | Locality Detection Rate | Avg Latency |
|---|---|---|
| Deepgram Nova-2 | 35% | 2.10s |
| Whisper | 65% | 2.20s |
| Sarvam Saarika v2.5 | 70% | 1.95s |

## Key Findings

- Sarvam performed best for multilingual Indian conversational speech
- Whisper was the most robust open-source fallback
- Deepgram struggled under heavy code-switching and accent variation
- Transliteration normalization was necessary for fair evaluation across scripts



# Tech Stack

- Python
- Faster-Whisper
- Deepgram API
- Sarvam API
- RapidFuzz
- Pandas
- Unidecode



# Important Engineering Insight

A major challenge was handling script mismatch:

- Sarvam frequently outputs Devanagari text
- Whisper outputs Romanized English

Example:

```text
केंगेरी  ↔  Kengeri
```

Direct string comparison failed across scripts, so transliteration normalization (`unidecode`) was added before evaluation.



# Limitations

- Small dataset (20 recordings)
- Bangalore-focused locality names
- Limited speaker diversity
- No telephony-compressed audio
- Heuristic metrics instead of formal ASR benchmarks



# Future Improvements

- Larger multilingual datasets
- Real call-center audio
- Streaming ASR evaluation
- Confidence scoring for entity extraction
- Better phonetic matching for Indian accents



# Final Recommendation

For this specific telephony-style locality extraction use-case:

- **Primary ASR:** Sarvam Saarika v2.5
- **Fallback / Self-hosted Option:** Whisper

Production systems should additionally include:
- locality alias dictionaries
- phonetic normalization
- fuzzy matching pipelines

---

# Author

Karthikeyan M  
B.Tech Artificial Intelligence & Data Science  
ASR Benchmarking Project for Indian Conversational Speech
