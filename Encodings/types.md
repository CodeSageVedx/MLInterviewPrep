
---

# 📌 Categorical Encoding Techniques in Machine Learning

Machine learning models require numerical inputs. Categorical variables must be converted into numerical format using encoding techniques.

---

# 1️⃣ Label Encoding (Ordinal Encoding)

## Explanation

Label Encoding assigns a unique integer to each category.

Mapping rule:

Category_i → Integer value k
where k ∈ {0,1,2,...,n-1}

---

## Example

Size column:

Small
Medium
Large

After encoding:

Small  → 0
Medium → 1
Large  → 2

---

## Mathematical Representation

If categories are ordered:

Small < Medium < Large

Then mapping preserves order:

Small = 0
Medium = 1
Large = 2

Important:
The model assumes numeric relationship like:

Large (2) > Medium (1) > Small (0)

---

## Use Cases

* Ordinal data (Education level, Rating, Size)
* Tree-based models

---

## Not Suitable For

Nominal data (e.g., City names)

---

# 2️⃣ One-Hot Encoding (OHE)

## Explanation

Creates separate binary columns for each category.

If a feature has k unique categories:

OHE creates k new columns.

If drop='first':

Creates (k - 1) columns to avoid multicollinearity.

---

## Example

Color column:

Red
Blue
Green

After One-Hot Encoding:

Red  → (1,0,0)
Blue → (0,1,0)
Green → (0,0,1)

Table format:

Red | Blue | Green
1   | 0    | 0
0   | 1    | 0
0   | 0    | 1

---

## Mathematical View

Each category is represented as a basis vector in k-dimensional space.

For 3 categories:

Red   = [1,0,0]
Blue  = [0,1,0]
Green = [0,0,1]

---

## Use Cases

* Nominal data
* Linear Regression
* Logistic Regression
* SVM

---

## Limitation

If categories are large (e.g., 10,000 cities):

Creates 10,000 new columns → High dimensionality problem.

---

# 3️⃣ Binary Encoding

## Explanation

Step 1: Apply Label Encoding
Step 2: Convert integer into binary format

Reduces number of columns compared to One-Hot Encoding.

---

## Example

Categories:

A, B, C, D

Label Encoding:

A = 1
B = 2
C = 3
D = 4

Binary representation:

1 → 001
2 → 010
3 → 011
4 → 100

---

## Mathematical Representation

If category index = k

Binary representation:

k = b0*(2^0) + b1*(2^1) + b2*(2^2) + ...

where bi ∈ {0,1}

---

## Use Cases

* Medium to high-cardinality categorical variables
* Reduces feature explosion

---

# 4️⃣ Frequency / Count Encoding

## Explanation

Replace each category with its count or frequency in the dataset.

---

## Example

City column:

Mumbai
Delhi
Mumbai

Count Encoding:

Mumbai → 2
Delhi → 1

Frequency Encoding:

Encoded value = Count(category) / Total samples

Mumbai → 2 / 3 = 0.67
Delhi → 1 / 3 = 0.33

---

## Mathematical Formula

Encoded(category c) = Count(c) / Total number of rows

or simply Count(c)

---

## Use Cases

* High-cardinality features
* Tree-based models

---

# 5️⃣ Target Encoding (Mean Encoding)

## Explanation

Replace each category with the mean of the target variable for that category.

---

## Example (House Price Prediction)

Area | Price
A    | 50
A    | 60
B    | 80

Encoding:

A → (50 + 60) / 2 = 55
B → 80

---

## Mathematical Formula

For category c:

Encoded(c) = (Sum of target values where category = c) / (Number of samples in c)

Formula:

Encoded(c) = Sum(y_i where x_i = c) / N_c

where:

* y_i = target value
* N_c = number of samples in category c

---

## Risk: Data Leakage

If we compute mean using full dataset:

Model indirectly sees target distribution.

Solution:
Use cross-validation based encoding.

---

## Use Cases

* High-cardinality features
* Boosting models (XGBoost, LightGBM)

---

# 6️⃣ Hash Encoding (Feature Hashing)

## Explanation

Maps categories into fixed number of buckets using hash function.

Formula:

Encoded index = hash(category) % N

where:
N = number of buckets

---

## Example

If N = 5 buckets:

hash("Mumbai") % 5 = 3

---

## Use Cases

* Very large datasets
* NLP problems
* Memory efficiency required

---

# 7️⃣ Embedding Encoding

## Explanation

Neural networks learn dense vector representations for each category.

Each category is mapped to a vector of size d.

---

## Mathematical Representation

Embedding matrix:

E has shape (k × d)

where:

* k = number of categories
* d = embedding dimension

Category_i → vector v_i of size d

Example:

City → [0.23, -0.45, 1.2]

---

## Use Cases

* Deep Learning
* Recommendation Systems
* NLP

---

# 📊 Practical Selection Guide

Condition → Encoding

Ordered categories → Label Encoding
Small nominal categories → One-Hot Encoding
Medium cardinality → Binary Encoding
High cardinality → Target / Frequency Encoding
Very large-scale data → Hash Encoding
Deep learning models → Embeddings

---


