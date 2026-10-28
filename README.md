# 📱 Google Play Store Data Analysis v2

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)](https://pandas.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Exploratory Data Analysis (EDA) and sentiment analysis project on the Google Play Store dataset. This project extracts actionable insights for mobile app developers, product managers, and marketers to optimize app store positioning, user engagement, monetization strategy, and rating performance.

---

## 📌 Table of Contents
- [Executive Summary](#-executive-summary)
- [Dataset Overview](#-dataset-overview)
- [Project Workflow](#-project-workflow)
- [Key Insights & Findings](#-key-insights--findings)
- [Repository Structure](#-repository-structure)
- [Installation & Setup](#-installation--setup)
- [Usage](#-usage)
- [Technologies Used](#-technologies-used)
- [License & Acknowledgments](#-license--acknowledgments)

---

## 🎯 Executive Summary

The mobile app market is highly competitive, with millions of apps vying for user attention. This project analyzes over 10,000 Android applications and associated user reviews from the Google Play Store to identify key determinants of app engagement, popularity, and monetization success.

### **Core Objectives:**
1. **Clean & Standardize Raw Data:** Handle missing values, duplicate entries, inconsistent data formats, and type conversions.
2. **Category & Market Dynamics Analysis:** Identify high-demand categories and dominant app types.
3. **Monetization & Pricing Strategy:** Evaluate the trade-offs between free vs. paid pricing models.
4. **Sentiment & Review Dynamics:** Uncover correlations between customer review sentiment and rating scores.
5. **Data-Driven Recommendations:** Provide actionable strategic guidelines for new and existing app releases.

---

## 📊 Dataset Overview

The project leverages two core datasets:

1. **`googleplaystore.csv`** (App Metadata):
   * **`App`**: Name of the application.
   * **`Category`**: Category the app belongs to (e.g., `GAME`, `FAMILY`, `FINANCE`).
   * **`Rating`**: Overall average user rating (out of 5).
   * **`Reviews`**: Total number of user reviews.
   * **`Size`**: Size of the app in megabytes (`M`) or kilobytes (`k`).
   * **`Installs`**: Total number of user downloads/installs (e.g., `1,000,000+`).
   * **`Type`**: Free or Paid.
   * **`Price`**: Cost of the app in USD ($).
   * **`Content Rating`**: Target age group (`Everyone`, `Teen`, `Mature 17+`, etc.).
   * **`Genres`**: Specific sub-category or secondary genre.
   * **`Last Updated`**: Date when the app was last updated on the Play Store.

2. **`googleplaystore_user_reviews.csv`** (User Sentiment Data):
   * **`App`**: Name of the app.
   * **`Translated_Review`**: Pre-processed English review text.
   * **`Sentiment`**: Sentiment classification (`Positive`, `Negative`, `Neutral`).
   * **`Sentiment_Polarity`**: Score ranging from `-1.0` (most negative) to `1.0` (most positive).
   * **`Sentiment_Subjectivity`**: Score ranging from `0.0` (objective) to `1.0` (subjective).

---

## 🛠 Project Workflow

```
┌─────────────────┐    ┌──────────────────┐    ┌──────────────────────┐    ┌─────────────────┐
│  Data Ingestion │ ──►│  Data Cleaning   │ ──►│  Exploratory Data    │ ──►│  Sentiment &    │
│  & Loading      │    │  & Preprocessing │    │  Analysis (EDA)      │    │  Insights       │
└─────────────────┘    └──────────────────┘    └──────────────────────┘    └─────────────────┘
```

1. **Data Cleaning & Wrangling:**
   * Handled missing ratings and invalid values (e.g., removing erroneous rows/outliers).
   * Cleaned the `Installs` column by stripping `+` and `,` symbols, converting to integer format.
   * Converted app sizes (`Size`) into numeric values in Megabytes ($MB$).
   * Cleaned `Price` string characters (`$`) to floating-point numbers.
   * Dropped duplicate app entries while retaining the most recent/reviewed record.

2. **Exploratory Data Analysis (EDA):**
   * Categorical distribution and density analysis across categories and genres.
   * Bivariate and multivariate correlation analysis (`Installs` vs `Reviews`, `Rating` vs `Size`).
   * Price elasticity and conversion insights comparing Free vs. Paid models.

3. **Sentiment Analysis:**
   * Analysis of user sentiment polarity across top categories and rating brackets.
   * Merging review sentiments with store metadata for deeper behavioral profiling.

---

## 💡 Key Insights & Findings

* **Dominant Categories:** The `FAMILY`, `GAME`, and `TOOLS` categories contain the highest concentration of apps. However, `COMMUNICATION` and `GAME` categories dominate total overall installs.
* **Free vs. Paid Dynamics:** ~92% of Play Store apps are free. Free apps exhibit significantly higher install volumes, while paid apps face higher user friction and harsher review tendencies.
* **App Size Impact:** Lightweight apps ($< 30MB$) generally enjoy higher average download volumes and rating retention compared to heavier applications.
* **Update Recency:** Apps updated frequently (within the last 6 months) demonstrate significantly higher active user ratings and install metrics.
* **Sentiment Alignment:** High positive sentiment polarity correlates directly with apps that maintain an average rating above $4.2$.

---

## 📂 Repository Structure

```
google-play-store-analysis-v2/
├── data/
│   ├── googleplaystore.csv                  # Raw dataset containing app details
│   └── googleplaystore_user_reviews.csv     # Raw dataset containing user reviews
├── notebooks/
│   └── Google_Play_Store_Analysis_v2.ipynb  # Primary Jupyter notebook with code & visuals
├── assets/                                  # Plots, charts, and image exports
├── .gitignore                               # Standard Git ignore file
├── LICENSE                                  # Open-source license (MIT)
└── README.md                                # Project documentation
```

---

## ⚙️ Installation & Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/hashirbhatti/google-play-store-analysis-v2.git
   cd google-play-store-analysis-v2
   ```

2. **Set Up a Virtual Environment (Recommended):**
   ```bash
   # On macOS/Linux
   python3 -m venv venv
   source venv/bin/activate

   # On Windows
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

---

## 🚀 Usage

1. Launch the Jupyter Notebook environment:
   ```bash
   jupyter notebook
   ```
2. Navigate to `Google_Play_Store_Analysis_v2.ipynb` in the browser interface.
3. Execute all cells sequentially (`Kernel -> Restart & Run All`) to reproduce the data cleaning pipeline, data visualizations, and analytical report.

---

## 🧰 Technologies Used

* **Language:** Python 3.x
* **Data Processing:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`, `seaborn`
* **Environment:** Jupyter Notebook / Google Colab

---

## 📜 License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.

---

## ✉️ Contact & Support

**Hashir Bhatti**
* GitHub: [@hashirbhatti](https://github.com/hashirbhatti)
* Portfolio / Contact: Feel free to open an Issue or Pull Request for any queries or suggestions!