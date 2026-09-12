# Human validation of LLM-derived opposition scores

This repository contains the sampled records and score-comparison results used to validate LLM-derived opposition scores in the accompanying study.

## Contents

- `sampled_annotation_comparison.csv`: 75 sampled directed interactions, with relation identifiers, source/response texts, LLM opposition scores, and independent 0--4 ratings from two human annotators.
- `comparison_summary.csv`: overall and relation-specific human agreement and LLM--human correspondence results.

## Sampling and scoring

The sample includes 25 4Forums reply relations, 25 4Forums quotation relations, and 25 CreateDebate reply relations. Each group contains 8 lower-third, 9 middle-third, and 8 upper-third LLM-score records, randomly sampled within strata. These strata cover the score distribution; they are not human labels.

Two annotators independently rated opposition intensity from 0 (no substantive challenge) to 4 (explicit and comprehensive rebuttal). The table includes source_text and response_text from the original sampling workbook, matched using dataset, relation type, topic, discussion ID, both post IDs, and the LLM score. For replies, source_text is the parent text; for quotations, it is the source/quoted content shown in that workbook. These are the archived sample texts, not a newly reconstructed or rescored input set. Machine translations are not included; source records remain subject to the original dataset terms.

The prompt_version column has been omitted. All existing numerical scores and summary statistics remain unchanged.

## Main comparison

Across the 75 records, quadratic-weighted Cohen's κ between human annotators was 0.822. The Spearman correlation between the LLM score and the mean of the two human ordinal ratings was 0.806 (two-sided permutation p < 0.0001).
