# Rumor Detection on Twitter Threads Using Graph Neural Networks

## Project Overview
This project aims to classify Twitter conversation threads as **"Rumor"** or **"Non-Rumor"** by modeling them as directed propagation graphs. Traditional classifiers often struggle to capture the complex structural dependencies of information propagation on social media. [cite_start]We address this by leveraging **Graph Neural Networks (GNNs)** to learn structural patterns and node-level features for accurate detection[cite: 5, 6, 9].

## Dataset & Graph Construction
[cite_start]We utilized the **Twitter15** and **Twitter16** datasets for training and evaluation[cite: 20].

* **Graph Structure:** Each conversation thread constitutes a graph where:
    * **Nodes:** Individual tweets.
    * [cite_start]**Edges:** Interactions between tweets (Reply or Retweet)[cite: 21].
* **Node Features:** We extracted **20 distinct features** for each node (tweet), including:
    * [cite_start]**Temporal Delays:** Time passed since the original root tweet[cite: 22, 189].
    * [cite_start]**Interaction Types:** Retweet vs. Reply information[cite: 190].
    * [cite_start]**Structural Metrics:** Degree metrics, Root/Leaf status, and subtree information[cite: 191, 192].
    * [cite_start]**Centrality Metrics:**[cite: 193].

## Methodology

### 1. Feature Projection Layer
To enhance the representation of our raw data, we implemented a linear projection layer before feeding data into the GNNs.
* **Input:** 20 raw features.
* **Transformation:** `Linear -> BatchNorm -> ReLU`.
* [cite_start]**Output:** 128-dimensional rich encoded feature vectors[cite: 206, 209].

### 2. Models Implemented
We compared traditional machine learning baselines against various GNN architectures:

**Baselines:**
* [cite_start]Random Forest (RF) [cite: 196]
* [cite_start]Support Vector Machine (SVM) [cite: 197]

**GNN Architectures:**
* [cite_start]**GAT (Graph Attention Network):** Uses attention heads to assign importance weights to neighbors[cite: 199].
* [cite_start]**GCN (Graph Convolutional Network):** Aggregates neighborhood information using fixed weights[cite: 200].
* [cite_start]**BiGCN (Bi-directional GCN):** Processes propagation graphs in both Top-Down and Bottom-Up directions[cite: 201].
* [cite_start]**Custom BiGCN:** A modified implementation featuring a **residual block** to improve information flow[cite: 202].

## Experiments & Results

### Performance Summary
[cite_start]Our experiments showed that **GNN models consistently outperformed traditional methods**[cite: 277]. [cite_start]The **GCN** and **Custom BiGCN** were the top performers[cite: 273].

* [cite_start]**Best Model:** Built-in **GCN** achieved the highest robustness with high Accuracy and F1 scores[cite: 302, 307].
* **Class Imbalance:** The dataset was imbalanced (75% Rumor / 25% Non-Rumor). [cite_start]We applied class weights during training, which significantly improved the Macro F1 scores across all models[cite: 221, 222, 226].

### Key Metrics (GCN Model)
| Metric | Score |
| :--- | :--- |
| **Accuracy** | [cite_start]**87.88%** [cite: 326] |
| **Macro F1** | [cite_start]**0.85** [cite: 326] |
| **ROC AUC** | [cite_start]**0.93** [cite: 352] |
| **Rumor Precision** | [cite_start]0.96 [cite: 326] |
| **Non-Rumor Recall** | [cite_start]0.90 [cite: 326] |

### Latent Space Visualization
The GCN model successfully learned a meaningful representation of the data. [cite_start]Visualizing the latent space shows a defined shape where "Rumor" and "Non-Rumor" classes are clearly separated[cite: 305, 308].

![Confusion Matrix](path_to_confusion_matrix_image)
[cite_start]*Confusion Matrix for the GCN model showing 151 True Positives for Rumors and 52 True Positives for Non-Rumors[cite: 332].*

## Future Improvements
* Further tuning of the Custom BiGCN residual connections.
* Integration of text-based embeddings (e.g., BERT) alongside structural features.

---
*Project for Graph Theory Course.*
