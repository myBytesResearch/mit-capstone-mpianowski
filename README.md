# 🎯 Customer Segmentation with Unsupervised Clustering

**Turning 2,240 anonymous customers into three actionable marketing segments - so campaigns stop treating everyone the same.**

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-clustering-F7931E?logo=scikitlearn&logoColor=white)
![Task](https://img.shields.io/badge/task-unsupervised%20learning-8A2BE2)
![Best model](https://img.shields.io/badge/model-K--Means%20(k%3D3)-success)
![Segments](https://img.shields.io/badge/segments-3-blue)

> MIT Professional Education - Applied AI and Data Science Program · Capstone Project · Mariusz Pianowski

---

## The problem

A retailer runs campaigns across web, catalog and store for six product categories - and gets **campaign acceptance of only ~1 - 15 %**, because every customer is targeted the same way. The goal: use **unsupervised learning to discover the natural customer segments hidden in the behavioural data**, so budget can flow to where it actually converts.

No target label, no supervised shortcut - the structure has to be *found*.

## The data

- `marketing_campaign.csv` - **2,240 customer records**, 26 attributes: demographics, category spend (wine, fruit, meat, fish, sweets, gold), channel behaviour (web/catalog/store/deals) and responses to five campaigns.
- Cleaning: median-imputed `Income` (24 missing), one extreme income outlier removed → **2,232 records modelled**.
- **17 behavioural features** used for clustering; demographics reserved for profiling the resulting segments.
- *Public educational dataset used in the MIT program.*

## The approach

- **EDA** → income is the dominant spend driver; wine + meat ≈ 75 % of all spend; children sharply reduce premium spend.
- **Feature engineering** - 8 new features (Age, Family_Size, Expenses, NumTotalPurchases, TotalAcceptedCmp, AmountPerPurchase, …).
- **StandardScaler** + **PCA** (10 components, **90.7 % variance**) for a clean modelling space; t-SNE for 2-D intuition.
- **Five clustering algorithms compared** on silhouette score and business interpretability:
  K-Means · K-Medoids (PAM) · Hierarchical (Ward) · DBSCAN · Gaussian Mixture.

## Results

| Algorithm (k = 3) | Silhouette | Verdict |
|---|---|---|
| **K-Means (selected)** | **0.2888** | Balanced, interpretable, assigns new customers |
| K-Medoids | 0.2670 | Comparable, slower |
| Hierarchical (Ward) | 0.2661 | Confirms the same 3-segment structure |
| GMM | 0.1808 | Weaker separation |
| DBSCAN | 0.4820 | **Rejected** - 2,216 in one blob + 10 noise points; can't score new customers |

DBSCAN scored highest but is **useless in production** (one dominant cluster, no way to assign future customers). The K-Means silhouette of **0.2888 marks moderate, still operationally interpretable structure** - not a case of cleanly isolated clusters. **K-Means (k = 3)** was chosen *because* its three segments are reproduced by K-Medoids *and* Hierarchical clustering - the confidence comes from that reproduction, not from the size of the score.

### The three segments

| Segment | Share | Avg income | Avg spend | Campaigns accepted |
|---|---|---|---|---|
| 💎 **Premium Enthusiasts** | 25.4 % | $76,319 | $1,420 | 1.01 |
| 🛒 **Moderate Mainstream** | 27.8 % | $57,292 | $721 | 0.40 |
| 👨‍👩‍👧 **Budget Families** | 46.8 % | $35,475 | $99 | 0.17 |

## From clusters to strategy

- **Three-tier campaigns** - Premium: exclusive/VIP, catalog + in-store; Mainstream: cross-sell/loyalty, omnichannel; Budget: deals & family bundles, mobile + email.
- **Reallocate budget** toward the segment that converts (Premium share up, Budget down).
- **Channel fit** - stop catalog mailings to Budget; double down on catalog for Premium.

> 💡 The projected financial upside (~$98 K net benefit / ~196 % first-year ROI) is an **illustrative model calculation** on stated assumptions, not a measured result.

## Run it

```bash
pip install pandas numpy scikit-learn scikit-learn-extra matplotlib seaborn
jupyter notebook Capstone_Final_Marketing_Campaign_Analysis_FullCode_Mariusz_Pianowski.ipynb
```

## Repo contents
- `Capstone_Final_Marketing_Campaign_Analysis_FullCode_Mariusz_Pianowski.ipynb` - full, executed capstone notebook (EDA → feature engineering → 5-algorithm comparison → segment profiling → strategy).
- `Capstone_Final_Marketing_Campaign_Analysis_FullCode_Mariusz_Pianowski.html` - rendered export, viewable without a Jupyter environment.
- `Capstone_Presentation_Marketing_Campaign_Analysis_Mariusz_Pianowski.pdf` - capstone presentation.

## Related repositories - other MIT program projects

### 🏠 [Boston House Price Prediction](https://github.com/myBytesResearch/boston-house-price-prediction)
OLS linear regression predicting median home value (log-transformed `MEDV`), with VIF multicollinearity checks, 10-fold cross-validation and residual diagnostics. **Test R² 0.77** - note that RMSE/MAE/MAPE are computed on the log scale, so the ~5 % MAPE is not a 5 % price error.

### 🍔 [FoodHub - Exploratory Data Analysis](https://github.com/myBytesResearch/foodhub-order-analysis-mpianowski)
Business EDA of 1,898 food-delivery orders: cuisine mix, weekend demand, ratings coverage (38.8 % unrated) and delivery-time analysis.

Full founder portfolio: [github.com/myBytesResearch](https://github.com/myBytesResearch)

## Author
**Mariusz Pianowski** - Co-Founder, [myBytes](https://mybytes.com)
- 🎓 [MIT Professional Education - Applied AI and Data Science (verified credential)](https://credentials.professional.mit.edu/b96204c8-87dc-4c8f-a27b-51a946695f00)
- 💼 [LinkedIn](https://www.linkedin.com/in/mariusz-p-34780316/)
- 🔗 Full write-up: [Customer Segmentation with Clustering](https://mybytes.com/en/research/customer-segmentation-clustering) on mybytes.com/research

*License: code MIT. Dataset rights remain with the original publisher.*
