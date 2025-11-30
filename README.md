## 📑 Table of Contents
* [Overview](#overview)
* [Project Structure](#project-structure)
* [Dataset Description](#dataset-description)
* [Methodology](#methodology)

  * [Bag-of-Words Vectorization](#1-bag-of-words-vectorization)
  * [Dimensionality-Reduction-PCA](#2-dimensionality-reduction-using-pca)
  * [Combining Embeddings](#3-combining-the-embeddings)
  * [K-Means Clustering](#4-k-means-clustering-custom-implementation)
  * [Evaluation](#5-evaluation)
* [Results Summary](#results-summary)
* [Predicting Genre for a New Song](#predicting-genre-for-a-new-song)
* [Bonus Analysis](#bonus-analysis)
* [Potential Improvements](#potential-improvements)
* [References](#references)
* [Acknowledgements](#acknowledgements)

---

## Overview

This project explores how songs can be classified into genres **using only textual keywords**.
Using vectorization, dimensionality reduction, and a custom implementation of **K-Means clustering**, the notebook demonstrates how to group songs based on their instrument, mood, and style descriptors — entirely without labels.

---

## Project Structure

```
├── Music genre analysis.ipynb        # Main notebook
├── music genre analysis whitepaper.pdf
└── README.md
```

---

## Dataset Description

The dataset contains **147 songs**, each labeled with:

* Instrument keyword
* Mood keyword
* Style keyword
* Ground truth genre (Hip-hop, Classical, Country, Pop, Rock)

These keyword-based features are used to create embeddings for clustering.

---

## Methodology

### **1. Bag-of-Words Vectorization**

Bag-of-Words (BoW) is used to convert keywords into numerical vectors.
BoW is chosen over TF-IDF because:

* All keywords are equally important
* No stopwords exist in the dataset
* TF-IDF weighting would not provide meaningful benefits
* BoW is simple, efficient, and interpretable

---

### **2. Dimensionality Reduction Using PCA**

PCA reduces the high-dimensional sparse vectors into a **2D representation** by:

1. Standardizing features
2. Computing covariance matrix
3. Extracting eigenvalues/eigenvectors
4. Selecting principal components
5. Projecting data into lower dimensions

This helps simplify clustering and improves separation.

---

### **3. Combining the Embeddings**

Each song has 3 separate embeddings (instrument, mood, style).
The final embedding is obtained by **averaging** the three PCA-reduced vectors.

Reasons for averaging:

* All components carry equal weight
* Prevents dimensionality explosion
* Simple and computationally efficient

---

### **4. K-Means Clustering (Custom Implementation)**

* Implemented from scratch using NumPy + Pandas
* Multiple values of *k* tested using **WCSS (Within-Cluster Sum of Squares)**
* **Elbow Method** used to find optimal *k*
* Optimal number of clusters: **k = 3**

---

### **5. Evaluation**

#### **a. Genre distribution per cluster**

* Cluster 0 → Mostly Hip-hop
* Cluster 1 → Mostly Classical
* Cluster 2 → Mix of Rock + Country

#### **b. Silhouette Score**

* Average silhouette score ≈ **0.42**
* Indicates **moderate cluster quality**: reasonable separation but some overlap

---

## Results Summary

* Hip-hop and Classical show strong cluster formation
* Rock and Country show overlap due to shared keyword patterns
* PCA + K-Means effectively extract meaningful structure from keyword-only data
* Demonstrates the potential of unsupervised learning in text-based music classification

---

## Predicting Genre for a New Song

For a new song:

1. Convert its keywords into embeddings
2. Find nearest cluster using Euclidean distance
3. Assign the genre with the **highest frequency** within that cluster

This creates a simple yet intuitive genre prediction method.

---

## Bonus Analysis

Additional insights include:

* Genre frequency distribution
* Keyword frequency distribution
* Keyword similarities causing cluster overlap

  * Pop & Rock share “energetic”, “melodic”
  * Hip-hop & Synth-Pop share “synth”, “rhythmic”

---

## Potential Improvements

* Use TF-IDF on larger datasets
* Try UMAP or t-SNE for dimensionality reduction
* Test DBSCAN for irregular cluster shapes
* Add extrinsic metrics like ARI and NMI for label-based evaluation

---

## References

* Bag-of-Words & TF-IDF tutorials
* PCA fundamentals
* K-Means & Elbow Method resources
* Silhouette score documentation
* Clustering metrics (ARI, NMI)

---


