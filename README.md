#  **Reddit NSFW Classification Using SQL, Machine Learning & Gemini AI**

A complete end-to-end project combining **SQL analysis**, **EDA**, **TF-IDF +  Machine Learning**, and a **Hybrid NSFW Classifier** using **Rule-based filtering + Gemini 2.0 Flash API**.

This project predicts:

###  Whether a Reddit post (title only) is **NSFW**

###  Whether a Reddit post is **likely to be removed** (moderated)

---

##  **Project Overview**

Reddit hosts millions of posts, many of which get:

* Flagged as **NSFW**
* **Removed** by moderators
* Downvoted or given awards

This project uses **193,091 Reddit posts** from `/r/dataisbeautiful` and applies:

1. **SQL analysis** for insights
2. **Full text cleaning & NLP preprocessing**
3. **TF-IDF + Metadata feature engineering**
4. **Decision Tree & Random Forest models**
5. **A Hybrid NSFW classifier** combining

   * **Rule-based filters for piracy, gambling, adult content, violence**
   * **Gemini 2.0 Flash AI** for sexual-content classification

---

## 📊 **Dataset Description**

The dataset contains **193k rows** and **10+ columns**, including:

| Column                  | Description                       |
| ----------------------- | --------------------------------- |
| `title`                 | Reddit post title                 |
| `score`                 | Upvotes – downvotes               |
| `author`                | Username                          |
| `num_comments`          | Total comments                    |
| `removed_by`            | Who removed the post (if removed) |
| `over_18`               | NSFW tag                          |
| `total_awards_received` | Number of awards received         |

Target variables:

* **`is_deleted`** → predicts moderation
* **`nsfw_flag`** → predicts adult content (Gemini classifier)

---

##  **1. SQL Analysis (via pandasql)**

The project includes **advanced SQL queries** inside Python:

### ✔ Top authors

### ✔ Avg. score by flair

### ✔ CTE queries for high-performing posts

### ✔ NSFW/SFW distribution

### ✔ Deletion patterns using CASE + CTE

### ✔ Window functions (RANK, ROW_NUMBER)

### ✔ Top 3 posts per author

These insights help understand:

* User behavior
* Moderation patterns
* NSFW distribution
* High-engagement posts

---

## **2. Data Cleaning & Preprocessing**

Major cleaning steps:

* Fill missing titles
* Normalize categorical fields
* Convert awards to numeric
* Create **`is_deleted`** flag
* Convert timestamps
* Remove punctuation & stopwords
* Apply Porter stemming
* Build tokenized cleaned text

---

## **3. TF-IDF + Metadata Feature Engineering**

Final feature matrix = **TF-IDF text features (5000 dims)**

* **Metadata features**:

- score
- num_comments
- total_awards
- over_18
- title_len



## ** Machine Learning Models**

Two ML models were used:

### ** Decision Tree Classifier**

* max_depth = 70
* class_weight = balanced
* min_samples_split = 5

Useful as a baseline & interpretable model.

---

### ** Random Forest Classifier (Best ML Model)**

* 400 trees
* max_depth = 200
* balanced_subsample
* n_jobs = -1

### **Results:**

* F1-score ≈ **0.72**
* Handles text + metadata well
* Much better recall on deleted posts

---

## **5. Hybrid NSFW Classification System**

Reddit NSFW is NOT only sexual content.
It includes:

* Piracy
* Gambling
* Adult dating
* Violence
* Drugs
* Sexual content

So we built a **two-stage classifier**:

### **1️. Rule-Based Filter (0 API cost)**

Detects:

* "crack", "patch", "torrent"
* "situs judi", "poker", "casino"
* "nude", "porn", "sex"
* "murder", "blood", "killed"
* "cocaine", "weed"
* "adult dating", "escort"


### **2️. Gemini 2.0 Flash

For sexual ambiguity:

* Uses JSON response schema
* Structured output
* Hit only if rule-based filter fails

**Final Accuracy **: **91%**
