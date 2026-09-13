# LLM Backend Sensitivity

We compared GLM-5.3-Flash and Doubao-Seed-2.0-lite against the archived DeepSeek-V4-Flash P0 scores on the same 300 interactions used for prompt sensitivity: 100 4Forums replies, 100 4Forums quotations, and 100 CreateDebate replies. Sampling was proportional by topic with seed 42.

## Protocol

- All models received the exact same original P0 messages and input texts. See the [P0 templates](../prompt_sensitivity/prompts/Prompt_Templates.md).
- Temperature was 0.2. Provider-default reasoning behavior was not overridden, so backend defaults were not necessarily equivalent.
- API model identifiers for the new runs were `glm-5.3-flash` and `doubao-seed-2-0-lite-260215`; the returned model identifiers were checked.
- One valid rating was retained per model and interaction. Transient failures were retried; this is not a repeated-generation analysis.
- Reply confidence: `C_R = 0.30*d + 0.30*l + 0.20*c + 0.10*t + 0.10*(1-a)`.
- Quotation confidence: `C_Q = (0.30*d + 0.30*l + 0.20*c + 0.10*(1-a)) / 0.90`.
- DeepSeek is a comparison reference, not human ground truth. No downstream model was retrained for this experiment.
- An interrupted GLM-4.7 run is incomplete and is not included or combined with GLM-5.3-Flash.

## Results

Mean signed difference is comparison model minus DeepSeek on the 0-1 score scale.

| Dataset | Relation | Model | N | MAE | Spearman rho | Mean signed difference |
|---|---|---|---:|---:|---:|---:|
| 4Forums | Reply | GLM-5.3-Flash | 100 | 0.0754 | 0.9302 | -0.0073 |
| 4Forums | Quotation | GLM-5.3-Flash | 100 | 0.0917 | 0.9057 | -0.0300 |
| CreateDebate | Reply | GLM-5.3-Flash | 100 | 0.0664 | 0.9375 | -0.0222 |
| 4Forums | Reply | Doubao-Seed-2.0-lite | 100 | 0.1067 | 0.8570 | +0.0116 |
| 4Forums | Quotation | Doubao-Seed-2.0-lite | 100 | 0.1102 | 0.8773 | -0.0223 |
| CreateDebate | Reply | Doubao-Seed-2.0-lite | 100 | 0.1011 | 0.8637 | +0.0089 |

GLM agreed more closely with DeepSeek than Doubao did in all three groups. Rankings were relatively consistent, but absolute differences were non-negligible. This does not establish correctness, score equivalence, identical threshold decisions, or downstream ROAF robustness. Generation variability may also contribute to observed differences.

## Files and Text Provenance

- [per_sample_comparison.csv](per_sample_comparison.csv): 300 rows with public sample IDs, topic, discussion topic, exact scoring input text pairs, all three composite scores, and differences from DeepSeek.
- [dimensional_scores.csv](dimensional_scores.csv): 900 rows with P0 profile, model, dimension scores, composite score, and the returned short scoring reason. Join to the text table by `sample_id`. Missing quotation response relevance is blank, not zero.
- [summary.csv](summary.csv): six comparisons with full-precision aggregate statistics.

For replies, `source_text` is the parent post and `response_text` is the reply. For quotations, they are the quoted passage and the quoting post. These are the actual inputs after the original whitespace processing and truncation to 1,600 characters, with ` ...` appended when truncated; they are not necessarily the complete raw posts. IDs match the prompt-sensitivity release. Internal reasoning traces, credentials, and implementation code are not published. Source datasets remain subject to their respective terms.
