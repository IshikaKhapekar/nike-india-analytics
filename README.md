# 👟 Nike India — Consumer Sentiment & Sales Analytics

> Analysing 40,000+ Nike customer reviews and sales data to uncover
> what Indian consumers love, what they complain about, and what
> Nike should do differently to grow in the Indian market.

---

## 📌 Project Overview

India's sportswear market is growing at 16.58% CAGR and is expected
to reach USD 3,298 million by 2030. Nike India is the market leader
in premium sportswear but faces growing competition from Adidas,
Puma, and domestic brands.

This project uses real Nike customer review data, product data, and
sales data to answer five key business questions:

1. How satisfied are Nike India customers overall?
2. What are customers most happy and most unhappy about?
3. Does price affect customer satisfaction?
4. Which sales channel and product category performs best?
5. What specific actions should Nike India take to improve?

All analysis done in Google Colab using Python.
No dashboarding tools — every chart generated in the notebook.


---

## 📊 Datasets Used

| Dataset | Source | Rows | Key Columns |
|---|---|---|---|
| Nike Reviews | Kaggle | 40,000+ | Rating, Review text, Fit Feedback, Comfort Feedback, Recommend Feedback, Price |
| Nike Products | Kaggle | 9,600+ | Product name, Price, Avg rating, Review count, Description |
| Nike Sales | Kaggle | 1,200+ | Product, Region, Sales Method, Units Sold, Total Sales |

### Reviews Dataset — Column Explanation

| Column | What it means |
|---|---|
| Rating | Star rating given by customer (1 = worst, 5 = best) |
| Review | Full text of customer review |
| Location | Country where customer is based |
| Fit Feedback | Customer's feedback on shoe sizing (True to Size / Runs Small / Runs Large) |
| Comfort Feedback | Comfort level rated by customer (Very Comfortable to Uncomfortable) |
| Recommend Feedback | Did the customer recommend this product? Yes / No |
| currentPrice | Price customer actually paid |
| fullPrice | Original price before any discount |
| discounted | Was the product discounted when purchased? True / False |
| title | Nike product name |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Python | Core programming language |
| Pandas | Data loading, cleaning, manipulation |
| NumPy | Numerical operations |
| Matplotlib + Seaborn | All 14 EDA and ML charts |
| NLTK VADER | Sentiment scoring on review text |
| WordCloud | Visual representation of common review words |
| Scikit-learn | Random Forest model, train/test split, evaluation |
| Google Colab | Cloud notebook environment — free, no installation |

---

## 🔍 Analysis Performed

### 1. Data Cleaning
- Renamed all columns to clean standard names
- Removed reviews with missing text or invalid ratings
- Removed reviews shorter than 4 words
- Removed duplicate reviews
- Fixed price columns (removed $ signs, converted to numbers)
- Added sentiment label (Positive / Neutral / Negative) based on rating

### 2. Exploratory Data Analysis — 9 Charts

**Chart 1 — Rating Distribution**
Shows the spread of all star ratings across 40,000+ reviews.
Tells us what percentage of customers are happy vs unhappy overall.

**Chart 2 — Top 10 Most Reviewed Products**
Shows which Nike products receive the highest engagement from
customers. These are the products Indians are buying the most.

**Chart 3 — Positive vs Neutral vs Negative Split**
Shows the percentage breakdown of satisfied, neutral, and
dissatisfied customers across all reviews.

**Chart 4 — Fit Feedback Distribution**
Shows how customers rate Nike shoe sizing.
Critical for India where sizing standards differ from US norms.

**Chart 5 — Comfort Feedback Distribution**
Shows the breakdown of comfort levels reported by customers.
Comfort is Nike's core product promise — this validates it.

**Chart 6 — Recommend Feedback**
Pie chart showing what percentage of customers would
recommend Nike to friends and family. Net Promoter signal.

**Chart 7 — Price vs Rating Scatter**
Scatter plot showing whether expensive Nike products
receive better ratings than cheaper ones. Colored by
discount status to show if discounts affect satisfaction.

**Chart 8 — Total Sales by Product Category**
Bar chart from sales data showing which Nike product
category generates the most revenue.

**Chart 9 — Sales by Sales Method**
Shows split between online, in-store, and outlet sales.
Critical for understanding India's digital buying shift.

### 3. VADER Sentiment Analysis — 3 Charts

VADER (Valence Aware Dictionary and sEntiment Reasoner) reads
the text of every review and assigns a score from -1 to +1.
- Score above +0.05 → Positive sentiment
- Score below -0.05 → Negative sentiment
- In between → Neutral

This is separate from the star rating — it reads the actual
language customers use, not just the number they clicked.

**Chart 10 — VADER Score Distribution**
Shows histogram of all compound scores and label breakdown.
Tells us the overall emotional tone of Nike India reviews.

**Chart 11 — VADER Score by Product**
Shows which specific Nike products generate the most
positive language in reviews vs the least positive.

**Chart 12 — Star Rating vs VADER Agreement**
Validates the NLP model by checking if VADER labels
agree with actual star ratings given by customers.
Agreement above 70% confirms the model is working correctly.

### 4. Word Cloud Analysis — 4 Visuals

Word clouds convert thousands of reviews into one image.
Bigger word = used more times by customers.
Three clouds made — all reviews, positive reviews only,
and negative reviews only — then compared side by side.

**What positive reviews say most:**
Words like comfortable, cushion, support, quality, lightweight,
perfect, stylish, smooth — tell us what Nike is doing right.

**What negative reviews say most:**
Words like small, narrow, sole, stitching, expensive, return,
tight — tell us exactly where customers are disappointed.

### 5. Random Forest ML Model

A Random Forest model was trained to predict whether a review
will be Positive or Negative based on 10 input features.

**What Random Forest means in simple terms:**
The model creates 100 decision trees. Each tree learns
patterns like — "if comfort feedback is Very Comfortable
AND vader score is above 0.3, likely Positive review."
All 100 trees vote together and the majority wins.

**Features used to predict:**
- Rating, VADER compound score, VADER positive score
- VADER negative score, Review word count
- Fit feedback (encoded as number)
- Comfort feedback (encoded as number)
- Recommend feedback (yes=1, no=0)
- Is product discounted (yes=1, no=0)
- Current price paid

---

## 📈 Key Findings

### Finding 1 — Overall Satisfaction is High but Sizing is the #1 Complaint

The majority of reviews are 4 or 5 star. However the Fit Feedback
chart shows a significant portion of customers report shoes
running small. The negative word cloud is dominated by words
related to sizing — small, narrow, tight, size. This is
especially relevant for India where foot width averages
differ from US standard sizing used by Nike globally.

### Finding 2 — Comfort is the Strongest Driver of Positive Reviews

The Random Forest feature importance chart shows comfort feedback
is one of the top 3 predictors of whether a review will be
positive. The positive word cloud confirms this — comfortable,
cushion, support, lightweight are the most frequent words in
happy customer reviews. When Nike delivers on comfort, customers
not only give 5 stars but use strong positive language in text.

### Finding 3 — Discounted Products Receive More Mixed Reviews

The Price vs Rating scatter chart shows that discounted products
(yellow dots) have a wider spread of ratings — more 1 and 2
star reviews compared to full-price products. This suggests
discounted products are often older stock that does not meet
current customer expectations, or that customers buying on
discount have higher expectations for the price paid.

### Finding 4 — Online Sales Channel is Dominant

The Sales by Method chart confirms online is the top channel
for Nike. This aligns with India's 32% YoY growth in online
sportswear purchases. In-store comes second, outlet third.
This has direct implications for where Nike should invest
in India — digital experience over physical store expansion.

### Finding 5 — Recommend Rate is Strong but Underutilised

The Recommend Feedback pie chart shows the large majority
of customers say Yes to recommending Nike. This is a strong
organic word-of-mouth signal that Nike India is not formally
capturing or converting into referral growth.

---

## ✅ Recommendations for Nike India

### Recommendation 1 — Fix Sizing for the Indian Market
**Based on:** Fit Feedback chart + Negative Word Cloud

India has different average foot dimensions compared to the
US market where Nike's sizing standard was built. A large
proportion of Indian customers report shoes running small.

Actions to take:
- Publish an India-specific size guide on Nike.com India
- Introduce half sizes across all footwear SKUs sold in India
- Add width options (narrow / regular / wide) to product pages
- Partner with Myntra and Flipkart to show size recommendation
  tool based on past purchase history

---

### Recommendation 2 — Lead All India Marketing with Comfort Messaging
**Based on:** Comfort Feedback chart + Feature Importance chart + Positive Word Cloud

Comfort is statistically the strongest predictor of a positive
Nike India review. Customers who report Very Comfortable
overwhelmingly leave 4 and 5 star reviews and use positive
language. This is Nike's biggest strength in India right now.

Actions to take:
- Lead all India digital ads with comfort and cushioning story
- Highlight foam and sole technology in product descriptions
- Create India-specific content around Nike Run Club for
  the growing running community in cities like Mumbai,
  Bangalore, Delhi, and Pune
- Target gym-goers and fitness community in Tier 1 cities
  with comfort-focused performance messaging

---

### Recommendation 3 — Rethink Discounting Strategy in India
**Based on:** Price vs Rating scatter + Discounted product analysis

Discounted Nike products receive a wider spread of negative
reviews. India is a price-sensitive market but discounting
premium products sends a mixed quality signal and attracts
customers whose expectations do not match the product.

Actions to take:
- Reserve discounts for lifestyle and casual category only
- Never discount flagship running, training, or basketball models
- Instead offer value through bundling — shoe plus sock plus
  water bottle at a combined price rather than percentage off
- Protect the premium brand positioning Nike has built in India

---

### Recommendation 4 — Invest Heavily in Digital India Experience
**Based on:** Sales by Method chart + Online channel dominance

Online is Nike India's top revenue channel. India's e-commerce
sportswear segment grew 32% in 2024. The opportunity to
capture more of this growth exists right now.

Actions to take:
- Add Hindi and major regional language support to Nike.com India
- Build an AI-powered size recommendation feature for online buyers
- Improve the Nike App experience for Indian users specifically
- Invest in faster delivery partnerships in Tier 2 cities
  like Nagpur, Jaipur, Lucknow, Surat, Coimbatore
- Run India-exclusive drops and limited editions on the Nike app
  to drive app downloads and engagement

---

### Recommendation 5 — Build a Formal Referral Program
**Based on:** Recommend Feedback chart + VADER positive scores

The majority of Nike India customers say they would recommend
Nike to others. This organic willingness is not being captured
in any formal way. Every customer who recommends Nike to a
friend is free customer acquisition.

Actions to take:
- Launch Nike India Refer and Earn program through the app
- Give existing customers a reward (store credit or exclusive
  product access) for every new customer they bring in
- Feature real Indian customer reviews in all ad campaigns
- Build the Nike Run Club India community as a content platform
  where happy customers naturally promote the brand
- Partner with micro-influencers in fitness — not Bollywood
  celebrities — for more authentic reach in Tier 1 and 2 cities

---

## 💡 Key Takeaways

- Nike India customers are largely satisfied but sizing is a
  persistent pain point specific to the Indian market
- Comfort is the single biggest driver of a positive Nike review
  and should anchor all India product and marketing strategy
- Online channel dominates and will grow further — digital
  investment in India will give the highest return
- Discounting premium products hurts brand perception in India
  more than it helps short term revenue
- Word of mouth is already strong — a formal referral program
  would convert this organic asset into measurable growth

---

## 🚀 How to Run This Project

1. Go to 👉 https://colab.research.google.com
2. Open `notebooks/Nike_India_Project.ipynb`
3. Upload the 3 CSV files from `data/` to your Google Drive
4. Run all cells 
5. All charts save automatically to your Drive outputs folder

---

## 👤 Author

**Ishika Khapekar**
