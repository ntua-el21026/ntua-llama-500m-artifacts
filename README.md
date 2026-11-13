# NTUA LLaMA-style 500M — companion artifacts

Report, configurations and selected model-only checkpoints for the **Team 12** NTUA ECE Pattern Recognition project, Winter 2025–2026. The implementation and training/fine-tuning/evaluation workflows live in [ntua-llama-500m-nanotron](https://github.com/ntua-el21026/ntua-llama-500m-nanotron). These are two packages of one team project.

The report credits **Evaggelos Asitzoglou, Panagiotis Avgerinos, Michail-Athanasios Peppas, Andreas Saounatsos and Giannis Chatzigeorgiadis**. Individual implementation responsibilities have not been reconstructed from the imported history.

## Artifact index

| Material | Location and role |
| --- | --- |
| Report | [Report.pdf](docs/Report.pdf) and [main.tex](docs/main.tex): preserved scientific narrative and source |
| Main configurations | [config/](config/): Stage-1 pretraining, Stage-2 code/math continuation, Stage-3 reasoning continuation and Stage-4 SFT |
| Pre-SFT export | [stage3_12000_modelonly/](weights/stage3_12000_modelonly/): selected Stage-3 step-12,000 model |
| SFT export | [sft_stage3_smoltalk_run1_5000_modelonly/](weights/sft_stage3_smoltalk_run1_5000_modelonly/): selected step-5,000 model |
| Provenance | [release-provenance.json](docs/release-provenance.json): retained report/config hashes, expected LFS inventory and unresolved runtime fields |
| Qualification | [Model card](docs/MODEL_CARD.md) and [artifact verification](docs/ARTIFACT_VERIFICATION.md): result scope and historical checks |

The main architecture configuration declares 32 layers, hidden size 1024, intermediate size 2816, 16 attention heads, four key/value heads, tied embeddings and vocabulary size 128256. The project calls this a 500M model. The historical safetensors record counts 492,110,848 serialized tensor elements per checkpoint; serialized counts and nominal architecture descriptions should not be substituted for an independently executed parameter audit.

The [Stage-3 checkpoint metadata](weights/stage3_12000_modelonly/checkpoint_metadata.json) records step 12,000 and 3,145,728,000 stage-local consumed tokens. [SFT metadata](weights/sft_stage3_smoltalk_run1_5000_modelonly/checkpoint_metadata.json) records step 5,000 and 81,920,000 tokens. These counters do not resolve the report's overall curriculum-token total.

## Review without downloading weights

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/ntua-el21026/ntua-llama-500m-artifacts.git
cd ntua-llama-500m-artifacts
```

The report, configuration and metadata are ordinary repository files. Safetensors files use Git LFS; the command above leaves small pointers in their place. Each export comprises 194 shards, for 388 unique objects and 1,968,528,560 logical payload bytes across both exports. Do not treat pointer files as loaded model tensors.

For authorized model use, obtain the required checkpoint's LFS objects with Git LFS in a suitable external model environment and verify SHA-256 and size against the pointers. The preserved [12 November 2026 record](docs/ARTIFACT_VERIFICATION.md) reports successful transfer and byte/serialization checks for all companion objects, alongside missing-object errors from the workflow repository's own endpoint. That historical record supersedes the earlier pointer-only observation in `release-provenance.json`; both are retained unchanged. This documentation update did not repeat object downloads or verify current server availability.

## Reproduction boundaries

This repository has **no training entry point or resolved Python environment**. Use the workflow repository's [reproduction guide](https://github.com/ntua-el21026/ntua-llama-500m-nanotron/blob/main/docs/REPRODUCING.md) for data preparation, stage configurations, Slurm execution and tiered evaluation. Full optimizer/scheduler checkpoints, training caches, all intermediate models and complete evaluation outputs are not included here. Model-only exports do not support full-state training resume.

These Nanotron shards are not a qualified Transformers `from_pretrained` directory. The exact custom SFT tokenizer/chat template is absent; the pretraining tokenizer revision and historical Nanotron/dependency pins are unresolved. The historical exporter uses RoPE/BOS/EOS settings that differ from retained configuration. Recover those inputs and resolve conversion semantics before inference.

Read the [model card](docs/MODEL_CARD.md) before citing scores. The report's 22B/23.13B token statements remain inconsistent; task suites, splits and character-normalized QA scoring limit comparisons. Preserved SFT-native evidence includes 12% all-checks pass and 0% JSON validity on 50 prompts. Byte identity does not validate these numerical claims. No new training, inference or benchmark was run for this update.

## Terms

[MIT](LICENSE) applies to original contributions within the authors' rights. Framework code, tokenizers, datasets and weight redistribution each require their own provenance and terms. The root notice is not a blanket asset license. Historical paths, checkpoint identities, reports, configurations and verification records remain preserved.
