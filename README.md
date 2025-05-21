
# 🎬 Movie Review Sentiment Analysis

This project focuses on performing unsupervised sentiment analysis on IMDb movie reviews using a variety of techniques including VADER, Gensim Word2Vec, and KMeans clustering. The goal is to assess and cluster sentiment patterns in user-generated content without relying on labeled data.

## 📝 Data Collection

The IMDb user reviews were scraped using a custom script available in a companion repository:  
🔗 [IMDB User Reviews Scrapper](https://github.com/subhammoda/imdb-user-reviews-scrapper)

The scrapper collects a varied set of reviews across different movies and formats them for downstream processing.

## 🔍 Methods Used

### VADER Sentiment Analysis

I utilized the **VADER (Valence Aware Dictionary and sEntiment Reasoner)** model, which is lexicon and rule-based. VADER returns polarity scores for input text, including a **compound score** ranging from -1 to 1. Based on this score:
- **Compound > 0** → Positive sentiment
- **Compound ≤ 0** → Negative sentiment

I experimented with both raw and preprocessed reviews (e.g., without stop words) to see how text cleaning affects sentiment polarity detection.

### Gensim Word2Vec-Based Sentiment Scoring

To explore semantic similarities, I trained a **Word2Vec** model using Gensim on tokenized review texts. Several configurations were tested:
- **Vector size** (e.g., 100 dimensions)
- **Window size** (context window for word embedding training)
- **Minimum count** for words to be included in the model

I computed custom sentiment scores using cosine similarity (n-similarity) between review words and positive/negative lexicons:
- Sentiment score = Positive similarity - Negative similarity
- If score > 0 → Positive, else → Negative

This approach provided a semantic perspective on sentiment without labeled training data.

### KMeans Clustering on TF-IDF

I constructed a **TF-IDF matrix** of the reviews to capture term relevance, and applied **KMeans clustering**:
- Various numbers of clusters were tested
- **Cosine distance** used to measure similarity between TF-IDF vectors
- Clusters were evaluated based on the **majority sentiment label** within each cluster

This approach helped uncover sentiment-based groupings and relationships between review text and user ratings.

## 📂 Repository Structure

```
.
├── movie_data.csv                              # Scraped IMDb reviews
├── Sentimental Analysis IMDB reviews.py        # All the scripts for sentiment analysis
├── Data Preprocessing.py                       # Text cleaning and tokenization functions
├── requirements.txt                            # Dependencies
└── README.md                                   # Project documentation
```

## 📈 Results & Insights

- VADER performs well on informal reviews, especially with punctuation and capitalization handling.
- Word2Vec allows for nuanced sentiment analysis based on word proximity in vector space.
- KMeans clustering revealed emergent sentiment groupings that correlated with IMDb ratings in some cases.
- Uncovered 78% alignment between textual sentiments and user assigned ratings, validating the effectiveness of sentiment models and providing actionable insights into audience perceptions and review credibility

## ⚙️ Requirements

Install dependencies with:

```bash
pip install -r requirements.txt
```

## 🧠 Future Work

- Incorporate supervised classifiers (e.g., SVM, Logistic Regression) to benchmark against unsupervised methods.
- Add visualizations for sentiment distribution and cluster separability.
- Extend scrapper to include additional metadata (genre, release year, etc.)