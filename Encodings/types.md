

# 📌 Categorical Encoding Techniques in Machine Learning

Machine learning models require numerical input. Categorical variables must be transformed into numeric representations using encoding techniques.

---

# 1️⃣ Label Encoding (Ordinal Encoding)

## 📖 Explanation

Label Encoding assigns an integer to each category.

[
\text{Category}_i \rightarrow k, \quad k \in {0,1,2,...}
]

---

## 🔢 Example

| Size   |
| ------ |
| Small  |
| Medium |
| Large  |

After encoding:

| Size |
| ---- |
| 0    |
| 1    |
| 2    |

---

## 🧮 Mathematical View

If categories are ordered:

[
Small < Medium < Large
]

Then mapping preserves order:

[
Small = 0,; Medium = 1,; Large = 2
]

---

## ✅ Use Cases

* Ordinal data (Education level, Rating, Size)
* Tree-based models (less sensitive to ordering)

---

## ❌ Not Suitable For

Nominal data (e.g., City names)

---

# 2️⃣ One-Hot Encoding (OHE)

## 📖 Explanation

Creates binary columns for each category.

If a feature has ( k ) categories:

[
\text{OHE produces } k \text{ binary features}
]

With drop='first':

[
k - 1 \text{ features}
]

---

## 🔢 Example

| Color |
| ----- |
| Red   |
| Blue  |
| Green |

After One-Hot Encoding:

| Red | Blue | Green |
| --- | ---- | ----- |
| 1   | 0    | 0     |
| 0   | 1    | 0     |
| 0   | 0    | 1     |

With drop='first':

| Blue | Green |
| ---- | ----- |
| 0    | 0     |
| 1    | 0     |
| 0    | 1     |

---

## 🧮 Mathematical View

Each category is represented as a basis vector:

[
Red = (1,0,0)
]
[
Blue = (0,1,0)
]
[
Green = (0,0,1)
]

---

## ✅ Use Cases

* Nominal categories
* Linear Regression
* Logistic Regression
* SVM

---

## ❌ Limitation

High dimensionality for large number of categories.

---

# 3️⃣ Binary Encoding

## 📖 Explanation

1. Convert category to integer
2. Convert integer to binary representation

Reduces dimensionality compared to OHE.

---

## 🔢 Example

| Category |
| -------- |
| A        |
| B        |
| C        |
| D        |

Step 1 (Label Encoding):

A = 1
B = 2
C = 3
D = 4

Step 2 (Binary):

1 → 001
2 → 010
3 → 011
4 → 100

---

## 🧮 Mathematical View

If category index = ( k ),

Binary representation:

[
k = \sum_{i=0}^{n} b_i 2^i
]

---

## ✅ Use Cases

* Medium to high-cardinality categorical variables
* Reduces feature explosion

---

# 4️⃣ Frequency / Count Encoding

## 📖 Explanation

Replace category with its frequency or count.

---

## 🔢 Example

| City   |
| ------ |
| Mumbai |
| Delhi  |
| Mumbai |

After Count Encoding:

| City   | Count |
| ------ | ----- |
| Mumbai | 2     |
| Delhi  | 1     |

---

## 🧮 Mathematical View

[
Encoded(Category_i) = \frac{Count(Category_i)}{Total\ Samples}
]

or raw count.

---

## ✅ Use Cases

* High-cardinality features
* Tree-based models

---

# 5️⃣ Target Encoding (Mean Encoding)

## 📖 Explanation

Replace category with average target value.

---

## 🔢 Example (House Price)

| Area | Price |
| ---- | ----- |
| A    | 50L   |
| A    | 60L   |
| B    | 80L   |

Encoding:

[
A = \frac{50 + 60}{2} = 55
]
[
B = 80
]

---

## 🧮 Mathematical Formula

For category ( c ):

[
Enc(c) = \frac{\sum y_i \text{ where } x_i=c}{N_c}
]

---

## ⚠ Risk: Data Leakage

Must use cross-validation encoding:

[
Enc(c) = \text{Mean computed excluding current fold}
]

---

## ✅ Use Cases

* High-cardinality features
* Boosting models (XGBoost, LightGBM)

---

# 6️⃣ Hash Encoding (Feature Hashing)

## 📖 Explanation

Uses hash function to map categories into fixed number of buckets.

[
Encoded = hash(category) \mod N
]

---

## 🔢 Example

If N = 5 buckets:

[
hash("Mumbai") \mod 5 = 3
]

---

## ✅ Use Cases

* Very large datasets
* NLP systems
* Memory efficiency required

---

# 7️⃣ Embedding Encoding

## 📖 Explanation

Neural networks learn dense vector representations.

Each category is mapped to a vector:

[
Category_i \rightarrow \mathbf{v_i} \in \mathbb{R}^d
]

---

## 🔢 Example

City → [0.23, -0.45, 1.2]

---

## 🧮 Mathematical View

Embedding matrix:

[
E \in \mathbb{R}^{k \times d}
]

Where:

* ( k ) = number of categories
* ( d ) = embedding dimension

---

## ✅ Use Cases

* Deep Learning
* Recommendation Systems
* NLP

---

# 📊 Practical Selection Guide

| Condition                | Encoding           |
| ------------------------ | ------------------ |
| Ordered categories       | Label Encoding     |
| Small nominal categories | One-Hot            |
| Medium cardinality       | Binary             |
| High cardinality         | Target / Frequency |
| Very large-scale         | Hash               |
| Deep learning            | Embeddings         |


---
