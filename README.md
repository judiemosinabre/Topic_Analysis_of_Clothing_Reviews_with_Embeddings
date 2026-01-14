# Topic Analysis of Clothing Reviews with Embeddings

## Overview

This project performs **semantic topic analysis** on e-commerce clothing reviews using **text embeddings**. Instead of relying on traditional keyword-based topic modeling techniques (e.g., LDA), it leverages **dense vector representations** to capture semantic similarity between customer reviews and group them into meaningful themes.

The approach is well-suited for unstructured, user-generated text and enables deeper insight into recurring customer concerns, product feedback patterns, and latent topics at scale.

---

## Objectives

* Convert customer reviews into vector embeddings using a modern embedding model
* Cluster semantically similar reviews into latent topics
* Identify representative reviews for each topic cluster
* Enable similarity search for new, unseen reviews
* Produce interpretable outputs usable by product, marketing, and CX teams

---

## Dataset

**Source:**
Women’s Clothing E-Commerce Reviews dataset (CSV)

**Primary field used:**

* `Review Text` – free-form customer review content

**Preprocessing steps:**

* Removal of missing or empty reviews
* Basic dataset validation (row counts, null checks)
* Minimal text cleaning to preserve semantic richness for embeddings

---

## Technology Stack

* **Python**
* **Pandas** – data loading and preprocessing
* **OpenAI Embeddings API** – semantic vector generation
* **ChromaDB** – vector database for similarity search
* **SQLite (via pysqlite3)** – local persistence backend

### Embedding Model

* `text-embedding-3-small`

This model offers a good balance between semantic accuracy, performance, and cost efficiency for short-to-medium length review text.

---

## Project Workflow

1. **Environment Setup**

   * Install required dependencies
   * Configure SQLite compatibility for ChromaDB

2. **Data Loading**

   * Load reviews from CSV
   * Validate data integrity
   * Extract review text into a working corpus

3. **Embedding Generation**

   * Convert each review into a dense numerical vector
   * Maintain alignment between text and embeddings

4. **Vector Storage**

   * Store embeddings in a ChromaDB collection
   * Enable efficient similarity-based retrieval

5. **Clustering & Topic Discovery**

   * Group reviews based on semantic similarity
   * Identify representative reviews per cluster
   * Use embedding proximity as a proxy for topic coherence

6. **Similarity Search**

   * Embed a new input review
   * Retrieve the most semantically similar existing reviews
   * Assign the review to the closest topic cluster(s)

---

## Key Functionality

### `find_similar_reviews(...)`

**Purpose:**
Identifies reviews that are semantically similar to a given input review and groups them into clusters.

**Parameters:**

* `input_review` (str): New review text to analyze
* `review_texts` (list[str]): Existing review corpus
* `review_embeddings` (list[list[float]]): Precomputed embeddings
* `n_cluster` (int, default = 3): Number of semantic clusters to return

**Process:**

1. Generate an embedding for the input review
2. Compute similarity against stored embeddings
3. Group similar reviews into clusters
4. Return representative reviews per cluster

**Use Cases:**

* Mapping new customer feedback to existing themes
* Automated review categorization
* Customer support triage and prioritization

---

## Outputs

* Semantic clusters representing latent review topics
* Representative review samples per cluster
* Similarity-ranked results for ad-hoc comparison

These outputs can support:

* Product improvement analysis
* UX and fit-related issue detection
* Marketing and messaging insights
* Customer experience optimization

---

## Design Rationale

* **Embeddings over keywords:** Captures meaning even when different wording is used
* **Vector database:** Enables scalable similarity search without repeated computation
* **Notebook-based implementation:** Optimized for experimentation and iterative analysis

---

## Limitations

* Topics are implicit and not automatically labeled
* Clustering quality depends on dataset size and diversity
* Embedding generation incurs API costs at scale
* Sentiment is not explicitly modeled (can be added as an extension)

---

## Future Improvements

* Automatic topic labeling using LLM-based summarization
* Sentiment-aware clustering
* Temporal trend analysis
* Visualization dashboards
* API deployment for real-time review analysis

