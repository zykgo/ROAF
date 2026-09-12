# Prompt Sensitivity of Opposition Scores

| Dataset | Relation | Comparison | N | MAE | Spearman rho | Mean Signed Difference |
|---|---|---|---:|---:|---:|---:|
| 4Forums | Reply | P1 vs P0 | 100 | 0.0752 | 0.9278 | -0.0096 |
| 4Forums | Reply | P2 vs P0 | 100 | 0.0712 | 0.9151 | -0.0075 |
| 4Forums | Quotation | P1 vs P0 | 100 | 0.0642 | 0.9370 | -0.0162 |
| 4Forums | Quotation | P2 vs P0 | 100 | 0.0806 | 0.9315 | -0.0303 |
| CreateDebate | Reply | P1 vs P0 | 100 | 0.0596 | 0.9398 | +0.0104 |
| CreateDebate | Reply | P2 vs P0 | 100 | 0.0627 | 0.9203 | -0.0074 |

P0: original prompt; P1: dimension-wise assessment; P2: local claim comparison.
MAE = mean absolute error relative to P0. Spearman rho measures rank correlation with P0.
Mean signed difference = alternative score minus P0 score. Differences are on the [0,1] score scale, not accuracy percentage points.
Each setting contains 100 topic-stratified samples (sampling seed 42). DeepSeek-V4-Flash; temperature 0.2; one successful rating per sample and profile.
P0, P1, and P2 were freshly evaluated using Chinese instructions. This analysis concerns score sensitivity, not downstream accuracy.
