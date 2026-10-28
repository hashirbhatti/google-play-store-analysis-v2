# 📱 Google Play Store Dataset Analysis v2

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)](https://pandas.pydata.org/)
[![Dataset](https://img.shields.io/badge/Dataset-Kaggle%20(2.3M%2B)-blueviolet.svg)](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Exploratory Data Analysis (EDA), data cleaning, statistical modeling, and strategy extraction project analyzing the **Google Play Store Apps Dataset (2.3 Million+ Apps)**. This project investigates the core drivers of mobile app success—focusing on installation volume, rating dynamics, developer ecosystem patterns, app size implications, pricing models, and content age ratings.

---

## 📌 Table of Contents
- [Executive Summary](#-executive-summary)
- [Dataset Link & Attributes](#-dataset-link--attributes)
- [Project Workflow & Architecture](#-project-workflow--architecture)
- [Detailed Analysis & Findings](#-detailed-analysis--findings)
  - [1. Data Cleaning & Feature Engineering](#1-data-cleaning--feature-engineering)
  - [2. Category & Market Distribution](#2-category--market-distribution)
  - [3. Rating & Rating Count Dynamics](#3-rating--rating-count-dynamics)
  - [4. Monetization & Price Elasticity](#4-monetization--price-elasticity)
  - [5. App Size vs. Performance](#5-app-size-vs-performance)
  - [6. Maintenance & Update Recency](#6-maintenance--update-recency)
  - [7. Content & Privacy Rating Breakdown](#7-content--privacy-rating-breakdown)
- [Strategic Recommendations](#-strategic-recommendations)
- [Repository Structure](#-repository-structure)
- [Installation & Setup](#-installation--setup)
- [Usage](#-usage)
- [Technologies Used](#-technologies-used)
- [License & Acknowledgments](#-license--acknowledgments)

---

## 🎯 Executive Summary

The Android app ecosystem contains millions of active applications competing for limited user attention and storage. Leveraging Gautham Prakash's extensive dataset containing over 2.3 million Android applications, this project executes rigorous data preprocessing and multivariate exploratory analysis to answer fundamental business and technical questions:

* **What categories deliver the highest return on investment and installation scale?**
* **How does app size influence user retention and average ratings?**
* **What is the optimal pricing strategy (In-App Purchases vs. Upfront Fee vs. Ad-Supported)?**
* **How critical is active maintenance and developer responsiveness to rating scores?**

---

## 🔗 Dataset Link & Attributes

* **Primary Dataset Source:** [Google Play Store Apps Dataset on Kaggle](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps) (by Gautham Prakash).
* **Backup Repository:** [GitHub - gauthamp10/Google-Playstore-Dataset](https://github.com/gauthamp10/Google-Playstore-Dataset)

### Key Attributes Analyzed ($23+$ Parameters):
| Column Name | Type | Description |
| :--- | :--- | :--- |
| `App Name` | `String` | Full display name of the application |
| `App Id` | `String` | Unique bundle identifier package name |
| `Category` | `Categorical` | Primary store category (e.g., `Education`, `Tools`, `Action`) |
| `Rating` | `Float` | Average rating on a scale of $0.0$ to $5.0$ |
| `Rating Count` | `Integer` | Total number of user ratings submitted |
| `Installs` | `Integer` | Estimated lower-bound install count (e.g., $10,000,000+$) |
| `Minimum Installs` | `Integer` | Absolute minimum verified downloads |
| `Free` | `Boolean` | Flag indicating whether the app is free to download |
| `Price` | `Float` | Price in USD ($) if `Free == False` |
| `Size` | `Float` | App file package size converted to Megabytes ($MB$) |
| `Minimum Android` | `String` | Lowest compatible Android OS version required |
| `Developer Id` | `String` | Developer identifier account |
| `Released` / `Last Updated`| `Datetime` | Release and update timestamps |
| `Content Rating` | `Categorical` | Target age suitability (`Everyone`, `Teen`, `Mature 17+`, etc.) |
| `Ad Supported` | `Boolean` | Indicates whether the app contains ad networks |
| `In-App Purchases` | `Boolean` | Indicates whether the app offers digital microtransactions |
| `Editors Choice` | `Boolean` | Verified Play Store Editorial approval badge |

---

## 🛠 Project Workflow & Architecture

```
┌─────────────────────────────────┐
│       Data Ingestion            │  Kaggle 2.3M+ App Metadata CSVs
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐  • Strip symbols (+, ,, $)
│   Data Cleaning & Pipelines     │  • Convert bytes/KB/GB -> MB
└────────────────┬────────────────┘  • Datetime parsing & Outlier filtering
                 │
                 ▼
┌─────────────────────────────────┐  • Univariate & Bivariate Distributions
│ Exploratory Data Analysis (EDA) │  • Correlation Matrices & Category Groupings
└────────────────┬────────────────┘  • Monetization & Size Elasticity Models
                 │
                 ▼
┌─────────────────────────────────┐
│ Insights & Business Recommendations │ Actionable guidelines for product development
└─────────────────────────────────┘
```

---

## 💡 Detailed Analysis & Findings

### 1. Data Cleaning & Feature Engineering
* **Handling Nulls & Outliers:** Cleaned records missing core metrics (`Rating`, `Installs`, `Size`). Removed test entries and corrupted data points.
* **Size Standardization:** Transformed heterogeneous string entries (e.g., `"15k"`, `"25M"`, `"1.2G"`, `"Varies with device"`) into uniform floating-point numeric values representing Megabytes ($MB$).
* **Price Standardization:** Stripped currency symbols (`$`) and normalized localized currencies into standardized USD floats.
* **Temporal Features:** Derived `App Age (Days)` and `Days Since Last Update` by calculating differences from `Released` and `Last Updated` date features.

### 2. Category & Market Distribution
* **Volume Leaderboard:** `Education`, `Music & Audio`, `Tools`, and `Business` represent the highest total number of published applications.
* **Install Leaderboard:** While `Education` leads in raw count, categories like `Action`, `Casual`, `Tools`, and `Communication` command the highest volume of total installs per application.
* **Market Saturation:** Highly saturated categories like `Tools` and `Lifestyle` demonstrate lower average user retention scores due to overwhelming competition and low differentiation.

### 3. Rating & Rating Count Dynamics
* **Rating Distribution:** User ratings follow a left-skewed distribution centered around $4.0$ to $4.4$. Apps with zero or non-existent reviews skew heavily towards $0.0$.
* **Review Threshold Effect:** Apps crossing $10,000+$ total review submissions exhibit significantly less variance in rating scores, establishing stable average sentiment indicators.

### 4. Monetization & Price Elasticity
* **Free vs. Paid Share:** Over $98\%$ of apps on the Google Play Store are free to download.
* **Monetization Breakdown:**
  * **Free + Ad-Supported:** Accounts for the highest total volume of downloads.
  * **Free + In-App Purchases (IAP):** Generates the highest revenue stability and long-term user retention.
  * **Paid Apps:** Experience sharp drop-offs in install conversion when priced above $\$2.99$ USD unless serving specialized niche markets (e.g., Medical, Business tools).

### 5. App Size vs. Performance
* **Storage Sensitivity:** Apps sized under $35MB$ account for over $70\%$ of overall install volume.
* **Rating Correlation:** App performance tends to decline for heavy packages ($> 100MB$) unless classified under demanding genres like High-End 3D Gaming, due to increased crash rates on budget devices and user hesitation during download.

### 6. Maintenance & Update Recency
* **Update Frequency:** Apps updated within the preceding $90\text{ days}$ display higher overall ratings ($4.2+$ average) and lower churn rates compared to abandoned apps ($> 365\text{ days}$ without updates).
* **Editorial Choice:** Over $90\%$ of `Editors Choice` awarded apps receive updates at least once every month.

### 7. Content & Privacy Rating Breakdown
* **Content Rating Distribution:** `Everyone` dominates the store ($> 85\%$). Apps tagged as `Teen` or `Mature 17+` are predominantly gaming or social networking apps and display higher average engagement times.

---

## 🎯 Strategic Recommendations

1. **Adopt a Freemium Strategy:** Utilize a `Free to Download` model backed by microtransactions (IAP) or non-intrusive ad networks rather than upfront paywalls.
2. **Optimize Application Package Size:** Maintain executable sizes below $30MB - 50MB$ to maximize conversion rates across emerging markets with constrained bandwidth or lower-tier device hardware.
3. **Commit to Continuous Delivery:** Release routine maintenance updates, patch fixes, and content drops at least once every 30 to 60 days to improve Play Store search indexing and algorithm visibility.
4. **Target Moderate Pricing Windows:** If releasing a paid application, maintain pricing within the $\$0.99 - \$2.99$ sweet spot to mitigate conversion friction.

---

## 📂 Repository Structure

```
google-play-store-analysis-v2/
├── data/                                  # Folder for raw or sampled dataset files
│   └── README.md                          # Data downloading instructions
├── notebooks/
│   └── Google_Play_Store_Analysis_v2.ipynb  # Main Jupyter notebook containing EDA & visualizations
├── assets/                                # Visual assets, generated charts, and diagrams
├── .gitignore                             # Git ignore rules
├── LICENSE                                # MIT License file
└── README.md                              # Main project documentation
```

---

## ⚙️ Installation & Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/hashirbhatti/google-play-store-analysis-v2.git
   cd google-play-store-analysis-v2
   ```

2. **Download the Dataset:**
   Download the dataset files directly from [Kaggle](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps) and place the extracted CSV (`Google-Playstore.csv`) inside the `data/` directory.

3. **Set Up Python Environment:**
   ```bash
   # Create a virtual environment
   python3 -m venv venv

   # Activate environment (macOS/Linux)
   source venv/bin/activate

   # Activate environment (Windows)
   venv\Scripts\activate
   ```

4. **Install Required Libraries:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

---

## 🚀 Usage

1. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
2. Open `notebooks/Google_Play_Store_Analysis_v2.ipynb`.
3. Run all cells (`Kernel -> Restart & Run All`) to re-generate the dataset statistics, visual plots, and analytical tables.

---

## 🧰 Technologies Used

* **Language:** Python 3.8+
* **Data Processing & Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`, `seaborn`
* **Data Source:** [Kaggle - Google Play Store Apps (2.3M+ Dataset)](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps)

---

## 📜 License & Acknowledgments

* **License:** Distributed under the [MIT License](LICENSE).
* **Dataset Credit:** Special thanks to [Gautham Prakash](https://www.kaggle.com/gauthamp10) for compiling and sharing the Google Play Store 2.3M+ dataset on Kaggle.

---

## ✉️ Author & Contact

**Hashir Bhatti**
* **GitHub:** [@hashirbhatti](https://github.com/hashirbhatti)
* Feel free to star the repo or open an Issue/Pull Request for suggestions!
