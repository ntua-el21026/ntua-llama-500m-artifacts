# NTUA-Llama-500M (Nanotron)

Official repository for Team 12 project in the NTUA ECE course "Pattern Recognition" (Winter 2025-2026).

## Project Scope

This project trains and evaluates a 500M-parameter LLaMA-style model with a staged curriculum:

- Stage 1: base pretraining
- Stage 2: high-quality code/math continuation
- Stage 3: reasoning-oriented continuation
- Stage 4: supervised fine-tuning (SFT)

Evaluation follows a tiered protocol:

- Tier 1: training health analytics
- Tier 2: perplexity slices
- Tier 3: conditional-likelihood multiple-choice QA
- Tier 4 (Stage 4): SFT-native prompt behavior checks

## Repository Contents

- `config/`: canonical training and SFT configurations for the reported pipeline:
  `config_stage1.yaml`, `config_stage2.yaml`, `config_stage3.yaml`, `sft_stage3_smoltalk.yaml`.
- `docs/`: paper sources and compiled report (`main.tex`, `Report.pdf`).
- `weights/`: selected model-only checkpoint exports for reproducibility and comparison baselines:
  `stage3_12000_modelonly`, `sft_stage3_smoltalk_run1_5000_modelonly`.

## Reproducibility Note

Full training checkpoints, dataset caches, and complete evaluation outputs are produced on Leonardo HPC storage and are not fully versioned in this repository. This repository keeps the canonical configs, report artifacts, and selected release-ready weights.

## License

Original contributions: MIT (see `LICENSE`), subject to the asset terms below.

## Release role and status

This is the compact artifact package for the [full workflow](https://github.com/ntua-el21026/NTUA-Llama_500M_Nanotron_Full). The report, four canonical configs and selected model-only exports describe the same Team 12 project, not a second experiment. Preserve this package while the Full LFS endpoint is repaired. Its role can become a secondary release/archive only after replacement access and hashes are verified.

The team report credits Evaggelos Asitzoglou, Panagiotis Avgerinos, Michail-Athanasios Peppas, Andreas Saounatsos, and Giannis Chatzigeorgiadis. This is shared course work; no individual implementation-role allocation has been verified from the imported history.

A 12 November 2026 audit obtained download actions for all 388 unique objects at this endpoint, totaling 1,968,528,560 logical bytes. Full reported missing objects for those OIDs. Preparation checked the local pointer inventory only. Server metadata does not establish successful transfer, tensor integrity or inference correctness.

## Browsing and reproduction

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/ntua-el21026/NTUA-Llama_500M_Nanotron.git
cd NTUA-Llama_500M_Nanotron
```

This code-free package has no training entry point or reproducible Python environment. The model-only directories are Nanotron exports, not a promised ready-to-load Transformers model. Recover the exact framework revision, tensor files, tokenizer/chat template and runtime through the Full repository's [reproduction guide](https://github.com/ntua-el21026/NTUA-Llama_500M_Nanotron_Full/blob/main/docs/REPRODUCING.md). Verify pointer SHA-256 and size against downloaded objects in an authorized model environment. Never install a GPU stack simply to inspect this repository.

Read the local [model card](docs/MODEL_CARD.md) and [release provenance](docs/release-provenance.json) before citing results. The report's 22B/23.13B token statements remain unresolved, task suites and character-normalized validation scoring limit comparisons, and retained SFT evidence includes 12% all-checks pass and 0% JSON validity on 50 prompts. No new model execution or benchmark accompanies this preparation.

## Asset terms

MIT applies to original contributions within the authors' rights. The upstream tokenizer, datasets, framework code and model weights require distinct access/license provenance. The root notice does not establish a blanket license for those assets. The Meta Llama 3 tokenizer and custom SFT chat template must be recovered exactly; no source/model version or license is inferred from the repository name.

The [artifact verification record](docs/ARTIFACT_VERIFICATION.md) confirms the
Compact checkpoint bytes and matching Full pointers, with explicit tokenizer,
conversion, inference and licensing limits.
