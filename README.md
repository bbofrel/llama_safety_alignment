# Mitigating Safety Alignment Degradation via Semantic Filtering of Fine-Tuning Data

The full seminar paper is available in `report.pdf`.

This project investigates whether safety degradation in aligned large language models can be mitigated through data-centric interventions during fine-tuning.

Recent work has shown that even benign fine-tuning can weaken the safety behavior of aligned models. Inspired by findings that safety degradation correlates with semantic similarity between alignment and downstream datasets, I explore a simple mitigation strategy: filtering fine-tuning samples that are semantically similar to an alignment proxy.

## Research Question

Can safety degradation caused by fine-tuning be reduced by removing training samples that are semantically similar to alignment data?

## Method

* Base model: LLaMA-2-7B-Chat
* Fine-tuning method: QLoRA
* Downstream dataset: Dolly 15k
* Alignment proxy: PKU-SafeRLHF
* Similarity model: all-MiniLM-L6-v2 sentence embeddings
* Filtering criterion: cosine similarity threshold

Three training configurations were compared:

1. Full Dolly dataset
2. Similarity-filtered Dolly dataset
3. Randomly filtered Dolly dataset

## Evaluation

Model safety was evaluated on the PKU-SafeRLHF test split using multiple automated judges, including:

* ShieldGemma-2B
* ChatGPT-based safety classification

The evaluation focused on harmfulness rates after fine-tuning.

## Results

The experiments confirmed that fine-tuning substantially degrades safety, even when using parameter-efficient methods such as QLoRA.

However, semantic-similarity filtering did not provide a measurable safety improvement compared to standard fine-tuning or random data filtering. The results suggest that while semantic similarity may correlate with safety degradation, it is not sufficient as a standalone filtering signal in this setup.

