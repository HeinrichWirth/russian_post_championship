# Predicting Lost Postal Shipments

A concise, end‑to‑end **research notebook** that placed in the top 5 % of the *All‑Russian Championship – Russian Post track*. The goal: predict which parcels will be lost before delivery.

<sub>*This repo contains a **single Jupyter notebook** (`Pocht_Rus_Lost_Parcels.ipynb`). It walks through EDA, feature engineering, model training, evaluation, and submission creation in one place.*</sub>

---

## 1  Problem statement

Identify shipments whose digital trail breaks off (`label = 1`). A correct early warning lets Russian Post investigate and reduce customer frustration.

## 2  Data snapshot

| File                  | Rows  | Role                |
| --------------------- | ----- | ------------------- |
| `train.csv`           | ≈ 6 M | fully labeled       |
| `test.csv`            | ≈ 4 M | hidden labels       |
| `sample_solution.csv` | —     | submission template |

The public dataset is not redistributed here due to licence constraints.

## 3  Metric

Weighted blend emphasising discrimination:
$**Score** = 0.1 × Recall + 0.9 × ROC‑AUC$

## 4  Solution outline (notebook sections)

| Section                   | Highlights                                                  |
| ------------------------- | ----------------------------------------------------------- |
| **1 EDA**                 | imbalance (3 % positives)                                   |
| **2 Feature engineering** | loss‑rate encoding, regional loss %, operator ratios        |
| **3 Class re‑balancing**  | controlled oversampling to \~40 % positives                 |
| **4 Model**               | CatBoost (depth 9, 21 600 iters, LR 0.05)                   |
| **5 Validation**          | Blend ≈ 0.86                                                |
| **6 Feature importance**  | region & unknown‑operator ratios dominate                   |
| **7 Submission creation** | one‑liner once model is fitted                              |

## 5  Key takeaways

* **Simple > complex** — CatBoost + domain‑aware features beat TabNet/XGBoost with far less engineering.
* **Domain heuristics matter** — zip‑region mapping and operator statistics were top predictors.
* **Metric‑driven thresholding** — optimising the Recall/AUC blend required dedicated grid search around the decision threshold (0.25).

## 6  Credits

* Russian Post & the championship organisers for the data.
* Open‑source maintainers of CatBoost and the PyData stack.

---

*Written in 2025 by Heinrich Wirth*
