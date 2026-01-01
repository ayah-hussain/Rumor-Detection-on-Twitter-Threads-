# Rumor Detection on Twitter Threads Using Graph Neural Networks

## Project Overview
This project aims to classify Twitter conversation threads as "Rumor" or "Non-Rumor" by treating the threads as directed propagation graphs. Traditional classifiers often struggle to capture the complex graph propagation structures inherent in social media conversations. Our objective is to leverage Graph Neural Networks (GNNs) to learn these structural patterns and accurately detect rumors.

## Dataset and Graph Construction
We utilized the Twitter15 and Twitter16 datasets for this project.

* **Graph Structure:** Each conversation thread is constructed as a graph where nodes represent tweets and edges represent interactions (replies or retweets).
* **Node Features:** For each node (tweet), we extracted 20 features, including:
    * **Temporal Delays:** Time passed since the original root tweet.
    * **Interaction Type:** Distinguishing between retweets and replies.
    * **Degree Metrics:** Quantifying node connectivity.
    * **Tree Position:** Root/Leaf status and subtree information.
    * **Centrality Metrics:** Measuring node importance within the propagation tree.

## Methodology

### 1. Feature Projection Layer
To map the raw node features into a richer latent space before GNN processing, we implemented a linear projection layer:
* **Input:** 20 raw features.
* **Process:** Linear -> BatchNorm -> ReLU.
* **Output:** 128-dimensional encoded feature vectors.

### 2. Models Implemented
We compared the performance of traditional machine learning models against various GNN architectures:

**Traditional Baselines:**
* Random Forest (RF)
* Support Vector Machine (SVM)

**Graph Neural Networks:**
* **GAT (Graph Attention Network):** Uses attention heads to assign importance weights to neighbors.
* **GCN (Graph Convolutional Network):** Uses neighborhood information with fixed weights.
* **BiGCN (Bi-directional GCN):** Processes propagation graphs in both Top-Down (propagation) and Bottom-Up (dispersion) directions.
* **Custom BiGCN:** An enhanced BiGCN implementation featuring a residual block to improve gradient flow and feature retention.

## Experiments and Results

### Performance Summary
Our experiments demonstrated that GNN models outperformed traditional baselines (RF and SVM). The GCN and Custom BiGCN were the top-performing models.

* **Best Model:** The built-in GCN achieved the highest robustness, Accuracy, and F1 scores.
* **Class Imbalance:** The dataset consists of 75% Rumors and 25% Non-Rumors. Applying class weights significantly improved the Macro F1 scores across all models.

### Metrics (Best Model: GCN)
| Metric | Score |
| :--- | :--- |
| Accuracy | 87.88% |
| Macro F1 | 0.85 |
| ROC AUC | 0.93 |
| Rumor Precision | 0.96 |
| Non-Rumor Recall | 0.90 |

### Visualization
* **Latent Space:** The GCN model learned a meaningful representation, creating a clearly defined shape in the latent space that separates Rumors from Non-Rumors.
* **Confusion Matrix:** The model successfully identified 151 out of 173 Rumors and 52 out of 58 Non-Rumors in the test set.

## Conclusion
The project confirms that modeling Twitter threads as graphs and applying GNNs—specifically GCN and BiGCN with residual connections—provides a superior approach to rumor detection compared to flat, tabular classifiers.

---
Project created for the Graph Theory Course.
