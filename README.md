# Controlled Lyric Generation with Mood and Decade Conditioning

This project explores **controlled lyric generation** using a pretrained causal language model, **DistilGPT-2**. The goal is to generate short lyric samples conditioned on user-specified attributes, specifically **mood** and **decade**, and compare those outputs against an uncontrolled baseline model. The project uses a cleaned subset of Billboard song lyrics and evaluates both quantitative performance and qualitative sample outputs. :contentReference[oaicite:0]{index=0}

## Overview

Song lyrics are a form of creative text that depend heavily on tone, style, and repetition. This project investigates whether adding simple control tokens such as `<MOOD=sad>` and `<DECADE=1990s>` can guide a language model to generate more stylistically consistent lyrics than a baseline model without explicit controls. :contentReference[oaicite:1]{index=1}

Two models were compared:

- **Baseline model**: trained on lyric text only
- **Controlled model**: trained on lyric text with mood and decade control tokens prepended to each example

## Motivation

Traditional lyric generation models often produce text that is generic, repetitive, or weakly aligned with the style a user wants. This project studies whether lightweight prompt conditioning can make generated lyrics more useful for creative assistance, especially for songwriting ideation. :contentReference[oaicite:2]{index=2}

## Dataset

The dataset was built from a cleaned subset of Billboard song lyrics. Lyrics were:

- cleaned and split into smaller lyric chunks
- labeled with **mood** and **decade**
- split by **song** into train, validation, and test sets to avoid leakage

## Final split:
- **Train:** 167 examples
- **Validation:** 36 examples
- **Test:** 36 examples :contentReference[oaicite:3]{index=3}

## Methodology

This project uses **DistilGPT-2**, a smaller pretrained causal transformer, and fine-tunes it for lyric generation. The task is framed as **causal language modeling**, where the model predicts the next token in a sequence. :contentReference[oaicite:4]{index=4}

### Input formatting

**Baseline input**
```text
i still hear your voice at night...
``` 
## Controlled input

<MOOD=sad> <DECADE=1990s>
i still hear your voice at night...
## Training setup
- Tokenization with Hugging Face Transformers
- Text grouped into fixed blocks of 128 tokens
- Fine-tuning with causal language modeling
- Generation using temperature, top-k, top-p, repetition penalty, and no-repeat n-gram constraints
## Results

In the final evaluation:

Baseline: eval loss = 3.7981, perplexity = 44.62
Controlled: eval loss = 3.7863, perplexity = 44.09

The controlled model slightly outperformed the baseline on standard evaluation metrics, but the margin was small. Qualitatively, both models generated lyric-like text, though both still struggled with coherence and strong stylistic consistency.

## Key Takeaways
Prompt-based control with mood and decade tokens is feasible
The controlled model showed a small improvement over the baseline
Performance was still limited by:
small dataset size
repetitive lyric structure
relatively simple conditioning labels
Repository Contents



Example goal: generate a short lyric continuation that reflects the requested tone and era.

Tech Stack
Python
Pandas
Hugging Face Transformers
DistilGPT-2
Google Colab
Future Work

## Possible extensions to this project include:

- using a larger lyric dataset
- adding richer conditioning variables such as theme or song section
- improving human evaluation of lyrical creativity and stylistic alignment
- experimenting with larger or more specialized transformer models
## References
Dhandapani, A., Ilakiyaselvan, N., Mandal, S., Bhadra, S., & Viswanathan, V. (2023). Lyrics Generation Using LSTM and RNN. In Big Data and Cloud Computing. Springer.
Monteith, K., Martinez, T., & Ventura, D. (2012). Automatic Generation of Melodic Accompaniments for Lyrics. In Proceedings of the International Conference on Computational Creativity.
