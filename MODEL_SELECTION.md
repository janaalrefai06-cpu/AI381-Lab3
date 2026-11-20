\# Model Selection



\## The question



The model predicts whether a customer is likely to leave the service (churn). A wrong prediction can cause the company to miss customers who are about to leave or waste retention resources on customers who would stay.



\## Candidates



| Candidate | Why I tried it | AUC | F1 | F1 per slice (lowest) | p95 latency (ms) | Size (KB) | MLflow run ID |

|---|---|---:|---:|---:|---:|---:|---|

| Logistic Regression | Simple and lightweight baseline | 0.7982 | 0.4948 | 0.2500 | 3.43 | 3.55 | 5bc9f9525cd1405d9646fc88e32f174c |

| Random Forest | To capture non-linear patterns | 0.7589 | 0.4536 | 0.2222 | 15.79 | 3160.10 | 2b4a038011dd437d97573520a5cf88dc |

| Gradient Boosting | To test boosting performance | 0.7476 | 0.4167 | 0.2222 | 3.53 | 141.64 | b964914f93d14289a259fa698961c2b8 |



\## The champion



I selected Logistic Regression as the champion because it achieved the highest AUC (0.7982) and F1 (0.4948). It also had very low latency (3.43 ms) and the smallest model size (3.55 KB). I accepted that its lowest contract-slice F1 was only 0.2500, so performance on some customer groups needs further investigation.



\## My promotion rules



\- \*\*Latency budget (p95): 25 ms\*\*, because the model should respond quickly enough for online predictions.

\- \*\*Minimum gain to replace the champion (F1 points): 0.005\*\*, because a new model should demonstrate a meaningful improvement before replacing the current champion.



\## What I would check next



I would investigate performance across contract types, especially the one-year and two-year groups, and check whether these groups have enough customers. I would also monitor data changes and model performance over time.



