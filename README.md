# Shopify Product Recommendation System 🛍️

An end-to-end Python project that scrapes product data from public Shopify stores and builds a content-based recommendation system using **TF-IDF Vectorization** and **K-Nearest Neighbors (KNN)**.

## 🚀 Features

* **Automated Scraper**: Fetches product data (titles, tags, descriptions, types) directly from Shopify's hidden public API (`/products.json`).
* **Data Cleaning**: Automatically parses and strips HTML tags from product descriptions to ensure clean text input for the model.
* **Machine Learning**:
    * **TF-IDF Vectorization**: Converts text data into numerical vectors, intelligently prioritizing unique keywords over common filler words.
    * **KNN (Cosine Similarity)**: Identifies products with the most semantically similar descriptions and tags.
* **Zero-Config**: Works on almost any Shopify-hosted website without requiring API keys.

## 🛠️ Tech Stack

* **Python 3.8+**
* **Requests**: For handling HTTP requests to the Shopify store.
* **Pandas**: For data manipulation and structured storage.
* **BeautifulSoup (bs4)**: For parsing and cleaning raw HTML content.
* **Scikit-Learn**: For Vectorization (TF-IDF) and the Nearest Neighbors algorithm.

## 📦 Installation

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/chanuu123/Selenium-data-scrapping-and-Product-Recommendation.git]
    cd shopify-recommender
    ```

2.  **Install dependencies**
    ```bash
    pip install requests pandas scikit-learn beautifulsoup4
    ```

## ⚙️ Usage

1.  **Open the script** (`main.py` or the filename you used).
2.  **Set the Target URL**:
    Scroll to the `__main__` block at the bottom of the file and replace the `TARGET_URL` variable with the Shopify store you want to scrape.
    ```python
    if __name__ == "__main__":
        # Example: Gymshark (UK)
        TARGET_URL = "[https://uk.gymshark.com](https://uk.gymshark.com)" 
    ```
3.  **Run the script**:
    ```bash
    python main.py
    ```

## 📊 How It Works

### 1. The Scraper
Most Shopify stores expose a public endpoint at `/products.json`. This script iterates through paginated JSON data to extract:
* Product Title
* Product Type
* Tags
* HTML Description (Cleaned)

### 2. The Recommender
Once the data is collected, the system performs the following steps:

1.  **Feature Engineering**: It combines `Title`, `Tags`, `Type`, and `Description` into a single "soup" of text for every product.
2.  **Vectorization**: It uses **TF-IDF (Term Frequency-Inverse Document Frequency)** to convert that text into a matrix of numbers. This ensures that rare, descriptive words (e.g., "vintage", "leather") carry more weight than common words (e.g., "the", "and").
3.  **Nearest Neighbors**: It uses the **K-Nearest Neighbors (KNN)** algorithm with **Cosine Similarity** to calculate the distance between product vectors. The "closer" the vectors, the more similar the products.

## 📝 Example Output

```text
--- Starting scrape for [https://uk.gymshark.com](https://uk.gymshark.com) ---
Fetched page 1: 50 products.
...
--- Building Vectorizer and KNN Model ---
Model trained successfully.

Recommended for: Vital Seamless 2.0 Leggings - Black
----------------------------------------
1. Vital Seamless 2.0 Leggings - Grey Marl (Similarity: 0.92)
   Link: .../products/vital-seamless-2-0-leggings-grey-marl

2. Vital Seamless 2.0 Crop Top - Black (Similarity: 0.85)
   Link: .../products/vital-seamless-2-0-crop-top-black

3. Vital Seamless 2.0 Shorts - Black (Similarity: 0.81)
   Link: .../products/vital-seamless-2-0-shorts-black
