# Marathi ASR fine-tuning with LoRA — Bodhan AI Indic-Transcribe

Take-home assignment, AI Research Engineer, AI4Bharat (IIT Madras) · Author: Ankita

**Full write-up: [`Document_Bodhan_AI_Assignment_Ankita.pdf`](Document_Bodhan_AI_Assignment_Ankita.pdf)**

**Artifacts (LoRA checkpoint, logs, per-utterance results):** [Google Drive](https://drive.google.com/drive/folders/15SH7LyjG26wtqQxBQ5bQGJ89LGvtokJ?usp=sharing)

---

## What this is

Indic-Transcribe-Flex (Bodhan AI / AI4Bharat, 1.22B parameters, NVIDIA Canary architecture) fine-tuned on **Marathi** with **LoRA**, on a single free-tier Colab T4.

The pretrained model stays frozen. Low-rank adapters are injected into the encoder's self-attention and feed-forward layers and the decoder's self- and cross-attention, giving 41.9M trainable parameters (3.4% of the model). Training data is a 1,000-utterance subset of FLEURS Marathi (~3.3 h of read speech).

## Results

**Marathi test set (297 utterances)**

| Model | WER | CER |
|---|---|---|
| Base model | 18.24% | 6.42% |
| + LoRA adapter | **15.23%** | **4.51%** |
| Relative change | −16.5% | −29.7% |

123 utterances improved, 42 degraded, 132 unchanged. Training: 228 steps (2 epochs), 46.7 minutes, 10.2 GB peak GPU memory; best checkpoint at step 57.

**Further analysis** — the Marathi adapter applied to a language it was never trained on (Hindi, 100 utterances): WER 11.85% → 14.08%. Because the base weights are unmodified, the adapter is applied only for Marathi at deployment, so other languages keep their original accuracy. See §6.3 of the report.

## Repository contents
