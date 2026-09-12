# Prompt Sensitivity of Opposition Scores

## Design

We sampled 100 interactions from each of 4Forums replies, 4Forums quotations, and CreateDebate replies. Sampling was proportional to topic frequencies, without replacement, using sampling seed 42. Each sampled interaction was scored using P0, P1, and P2.

- P0: original prompt.
- P1: dimension-wise assessment.
- P2: local claim comparison.

All profiles used the same inputs and batch composition, DeepSeek-V4-Flash, and temperature 0.2. Text whitespace was collapsed; each text was truncated to 1,600 characters when necessary, followed by " ...". Requests contained up to eight interactions.

All P0 scores were freshly generated; quotation scores were not reused from reply caches. There are 900 valid scores and no unresolved failed batches.

## Files

- [Prompt templates](prompts/Prompt_Templates_English.md): all six reply/quotation templates.
- [Summary table](results/Prompt_Sensitivity_of_Opposition_Scores.md): six comparisons with P0.
- [Summary CSV](results/Prompt_Sensitivity_of_Opposition_Scores.csv): the same table in CSV format.
- [Per-sample comparison](results/per_sample_comparison.csv): 300 rows containing P0, P1, P2 and signed differences.
- [Dimensional scores](results/dimensional_scores.csv): 900 rows with individual dimension scores and composite confidence C.

Public sample IDs are anonymous within each dataset-relation group and link the two detailed tables. Forum texts, source identifiers, and free-text scoring reasons are omitted. The targeted_response field is blank for quotations because this dimension is not evaluated.

## Score Calculation

For replies, C = 0.30*d + 0.30*l + 0.20*c + 0.10*t + 0.10*(1-a).

For quotations, C = [0.30*d + 0.30*l + 0.20*c + 0.10*(1-a)] / 0.90.

d, l, c, t, and a correspond to direct_disagreement, logic_or_evidence_challenge, counter_claim, targeted_response, and agreement_or_neutral.

## Interpretation

MAE is the mean absolute difference from P0. Spearman rho is calculated from average ranks for tied values. Mean signed difference is alternative C minus P0 C. These are score-scale differences, not accuracy percentage points.

Spearman correlations range from 0.915 to 0.940; MAE ranges from 0.060 to 0.081. Rankings are consistent across the tested prompts, but absolute scores vary. Each sample/profile has one successful rating, so differences can also include generation variability. The sampling seed does not make LLM generation deterministic. This experiment does not evaluate downstream prediction robustness or alternative LLM backends.
