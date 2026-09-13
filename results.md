# Experimental Results

## 1. Centralized GraphSAGE Baseline

The centralized GraphSAGE model was trained on the Elliptic transaction graph using class-weighted cross-entropy loss.

### Test Results

| Metric            | Result |
| ----------------- | -----: |
| Test Accuracy     | 82.30% |
| Illicit Precision | 34.59% |
| Illicit Recall    | 91.20% |
| Illicit F1 Score  | 50.16% |

The centralized model achieved high recall for illicit transactions, detecting most illicit examples, although its precision was considerably lower.

---

## 2. Federated GraphSAGE — Class-Weighted Loss

Three simulated federated clients were trained locally, and their model parameters were aggregated using Federated Averaging (FedAvg).

The original class-weighted loss assigned a substantially larger relative weight to the minority illicit class.

### Validation Accuracy by Federated Round

| Round | Average Client Loss | Validation Accuracy |
| ----- | ------------------: | ------------------: |
| 1     |              0.5810 |              44.22% |
| 2     |              0.9171 |              90.08% |
| 3     |              0.7366 |              50.58% |

### Test Results

| Metric            | Result |
| ----------------- | -----: |
| Test Accuracy     | 50.88% |
| Illicit Precision | 16.43% |
| Illicit Recall    | 98.68% |
| Illicit F1 Score  | 28.18% |
| True Positives    |    673 |
| False Positives   |  3,422 |
| False Negatives   |      9 |

The class-weighted federated model achieved extremely high recall but produced a large number of false positives. This indicates that the model became strongly biased toward predicting the minority illicit class.

---

## 3. Federated GraphSAGE — Unweighted Loss

A second federated experiment removed class weighting while keeping the same three-client FedAvg setup.

### Validation Accuracy by Federated Round

| Round | Average Client Loss | Validation Accuracy |
| ----- | ------------------: | ------------------: |
| 1     |              0.8318 |              89.45% |
| 2     |              0.5588 |              77.21% |
| 3     |              0.4222 |              90.39% |

### Test Results

| Metric            | Result |
| ----------------- | -----: |
| Test Accuracy     | 90.48% |
| Illicit Precision | 94.74% |
| Illicit Recall    |  2.64% |
| Illicit F1 Score  |  5.14% |
| True Positives    |     18 |
| False Positives   |      1 |
| True Negatives    |  6,302 |
| False Negatives   |    664 |

Although the unweighted model achieved high overall accuracy and precision, it detected only a small proportion of the illicit transactions. The high accuracy is therefore misleading because the dataset is highly imbalanced.

---

## 4. Federated GraphSAGE — Moderate Class Weighting

A third federated experiment used moderate class weighting to investigate whether a better balance between precision and recall could be achieved.

The licit class was assigned a weight of 1.0 and the illicit class a weight of 3.0.

### Validation Accuracy by Federated Round

| Round | Average Client Loss | Validation Accuracy |
| ----- | ------------------: | ------------------: |
| 1     |              1.1659 |              89.25% |
| 2     |              1.3255 |              63.39% |
| 3     |              0.6684 |              90.41% |

### Final Validation Metrics

The final global model after Round 3 was also evaluated using class-specific validation metrics.

| Metric              | Result |
| ------------------- | -----: |
| Validation Accuracy | 90.41% |
| Illicit Precision   | 58.33% |
| Illicit Recall      |  6.16% |
| Illicit F1 Score    | 11.14% |
| True Positives      |     42 |
| False Positives     |     30 |
| True Negatives      |  6,273 |
| False Negatives     |    640 |

Although the final model achieved high validation accuracy, its low illicit recall and F1 score show that accuracy alone does not reflect its ability to detect the minority illicit class.

### Test Results

| Metric            | Result |
| ----------------- | -----: |
| Test Accuracy     | 90.71% |
| Illicit Precision | 72.00% |
| Illicit Recall    |  7.92% |
| Illicit F1 Score  | 14.27% |
| True Positives    |     54 |
| False Positives   |     21 |
| True Negatives    |  6,282 |
| False Negatives   |    628 |

Moderate class weighting increased illicit recall compared with the unweighted federated model while maintaining relatively high precision. However, the model still failed to identify most illicit transactions.

This experiment demonstrates the trade-off introduced by class weighting. Increasing the importance of the minorit
