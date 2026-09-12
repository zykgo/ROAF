# ROAF

Supplementary materials for **ROAF: Relation-Specific Opposition Weighting and Reliability-Aware Fusion for Stance Detection**.

This repository contains prompt templates and experimental results. It does not include implementation or training code.

## Contents

| Directory | Contents |
|---|---|
| [prompts](prompts/) | Main-experiment reply and quotation scoring templates |
| [experiment/prompt_sensitivity](experiment/prompt_sensitivity/) | P0/P1/P2 templates, aggregate results, and per-sample scores |
| [experiment/human_validation](experiment/human_validation/) | Human annotation comparisons with the sampled text pairs |

The human-validation results originate from commit `df1b1810503cb1515cf70a2f163e81bdbadcacbc` of [llm-opposition-score-validation](https://github.com/zykgo/llm-opposition-score-validation). The sample table adds texts from the original sampling workbook and omits the prompt_version column. Ratings and summary statistics are unchanged.

Sampled text pairs are provided alongside their scores. Full datasets, credentials, model checkpoints, and local execution logs are not distributed here. Original datasets remain subject to their respective terms.
