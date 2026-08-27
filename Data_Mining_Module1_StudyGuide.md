# Data Mining — Module I Study Guide
### (Data Mining Basics, OLAP, Pattern Mining)

---

## HOW TO USE THIS GUIDE
- **2-mark questions**: short, crisp answers — memorize the definition + one line of explanation.
- **8-mark questions**: come in either/or pairs — write ~1 page, use diagrams/tables wherever possible.
- **16-mark questions**: come in either/or pairs — these need full explanations WITH a solved numerical example. Practice writing these out by hand at least once.

---

## SECTION A — 2 MARK QUESTIONS (Pick any 6)

### 1. What is Data Mining?
Data Mining is the process of discovering interesting patterns, correlations, and useful knowledge from large amounts of data stored in databases, data warehouses, or other repositories. It is often called "Knowledge Discovery from Data" (KDD).

### 2. What is Knowledge Discovery in Databases (KDD)?
KDD is the overall process of finding useful knowledge from data. Data mining is just one step in this process. The KDD process includes: Data Cleaning → Data Integration → Data Selection → Data Transformation → Data Mining → Pattern Evaluation → Knowledge Presentation.

### 3. What do you mean by "confluence of multiple disciplines" in data mining?
Data mining draws techniques from many fields such as statistics, machine learning, pattern recognition, database systems, information retrieval, visualization, and algorithms. It is not a single technique but a mixture ("confluence") of ideas from all these areas.

### 4. What are the different types of data attributes?
- **Nominal**: categories with no order (e.g., color: red, blue, green)
- **Ordinal**: categories with meaningful order (e.g., grade: low, medium, high)
- **Interval**: numeric, equal intervals, no true zero (e.g., temperature in °C)
- **Ratio**: numeric, has a true zero (e.g., height, weight, age)

### 5. What is Data Quality? Name two dimensions of data quality.
Data quality refers to how accurate, complete, and reliable data is for analysis. Key dimensions include: **Accuracy** (data is correct), **Completeness** (no missing values), **Consistency** (no contradictions), and **Timeliness** (data is up to date).

### 6. What is a Data Warehouse?
A Data Warehouse is a subject-oriented, integrated, time-variant, and non-volatile collection of data used to support management decision-making. It stores historical data gathered from multiple sources for analysis and reporting.

### 7. Differentiate between OLTP and OLAP.
| OLTP | OLAP |
|---|---|
| Handles day-to-day transactions | Handles analytical queries |
| Current data | Historical data |
| Simple queries, fast updates | Complex queries, read-mostly |
| Normalized schema | Denormalized (star/snowflake) schema |

### 8. What is a Data Cube?
A data cube is a multidimensional structure that allows data to be modeled and viewed in multiple dimensions (e.g., sales data viewed by product, region, and time simultaneously). It supports fast aggregation and analysis.

### 9. What is Dimensionality Reduction? Why is it needed?
It is the process of reducing the number of attributes (dimensions) under consideration, while preserving the important information. It is needed to reduce noise, storage cost, and computation time, and to avoid the "curse of dimensionality."

### 10. Define Frequent Itemset, Support, and Confidence.
- **Frequent Itemset**: a set of items that appears together in transactions at least as often as a minimum support threshold.
- **Support**: the percentage/fraction of transactions that contain a particular itemset.
- **Confidence**: the likelihood that item B is purchased when item A is purchased, i.e., Confidence(A→B) = Support(A∪B) / Support(A).

### 11. What is the Apriori property (downward closure property)?
It states that **all non-empty subsets of a frequent itemset must also be frequent**. Conversely, if an itemset is infrequent, all its supersets will also be infrequent. This property is used to prune the search space in the Apriori algorithm.

### 12. Define Lift as a pattern evaluation measure.
Lift measures how much more often items A and B occur together than expected if they were statistically independent.
Lift(A→B) = Confidence(A→B) / Support(B)
- Lift = 1 → A and B are independent
- Lift > 1 → positively correlated
- Lift < 1 → negatively correlated

---

## SECTION B — 8 MARK QUESTIONS (Either/Or Pairs)

## PAIR 1

### Q. Explain the different types of Data Warehouse Schemas with diagrams.

A data warehouse uses a **multidimensional data model**, typically implemented using one of the following schemas:

**1. Star Schema**
- Consists of one central **fact table** connected directly to multiple **dimension tables**.
- The fact table contains numeric measures (e.g., sales amount, quantity) and foreign keys to dimension tables.
- Dimension tables are **denormalized** (not further split), making queries fast and simple.
- Example: A `Sales_Fact` table connected to `Time`, `Product`, `Customer`, and `Store` dimension tables.

```
        Time
          |
Product — Sales_Fact — Store
          |
       Customer
```

**2. Snowflake Schema**
- An extension of the star schema where dimension tables are **normalized** into multiple related tables to reduce redundancy.
- Example: `Product` dimension is split into `Product` and `Product_Category`.
- Saves storage space but queries become slightly slower due to more joins.

**3. Fact Constellation Schema (Galaxy Schema)**
- Contains **multiple fact tables** that share common dimension tables.
- Used for complex data warehouses that need to model several business processes together (e.g., Sales and Shipping sharing the same Time and Product dimensions).

**Comparison Table:**
| Schema | Dimension Tables | Redundancy | Query Speed |
|---|---|---|---|
| Star | Denormalized | High | Fast |
| Snowflake | Normalized | Low | Slower (more joins) |
| Fact Constellation | Shared across facts | Medium | Moderate |

---

### Q. (OR) Explain the various OLAP operations with examples.

OLAP (Online Analytical Processing) allows users to interactively analyze multidimensional data from multiple perspectives. The main operations are:

1. **Roll-up (drill-up)**: Aggregates data by climbing up a concept hierarchy or reducing dimensions.
   *Example: Sales by city → Sales by state → Sales by country.*

2. **Drill-down**: The reverse of roll-up; navigates from summarized data to more detailed data.
   *Example: Sales by year → Sales by quarter → Sales by month.*

3. **Slice**: Selects a single dimension from a cube, producing a sub-cube.
   *Example: Selecting sales data for only "2024" from a Time-Product-Region cube.*

4. **Dice**: Selects two or more dimensions from a cube, creating a sub-cube based on multiple criteria.
   *Example: Sales where Time = "2024" AND Region = "South" AND Product = "Electronics".*

5. **Pivot (rotate)**: Rotates the data axes to provide an alternate presentation of data.
   *Example: Swapping rows and columns so that Product becomes rows and Time becomes columns.*

---

## PAIR 2

### Q. Explain the steps involved in Data Preprocessing.

Real-world data is often incomplete, noisy, and inconsistent. Data preprocessing improves data quality before mining. The major steps are:

**1. Data Cleaning**
- Fills in missing values (using mean/median, or prediction methods).
- Removes noise (using binning, regression, or clustering) — smooths out random errors.
- Detects and removes outliers and resolves inconsistencies in recorded data.

**2. Data Integration**
- Combines data from multiple sources (databases, files, etc.) into a coherent store.
- Key issues:
  - **Entity identification problem**: matching entities from different sources (e.g., "cust_id" in one DB = "customer_number" in another).
  - **Redundancy**: same attribute may have different names in different sources; solved using correlation analysis.
  - **Detection and resolution of data value conflicts** (e.g., different units like kg vs pounds).

**3. Data Transformation**
- Converts data into forms suitable for mining. Techniques include:
  - **Smoothing**: removes noise.
  - **Normalization**: scales attribute data into a small range (e.g., 0 to 1).
  - **Aggregation**: summary/aggregation operations applied to data.
  - **Generalization**: low-level data replaced by higher-level concepts (e.g., age → "youth/adult/senior").

**4. Data Reduction / Dimensionality Reduction**
- Reduces data volume while producing the same (or similar) analytical results.
- Techniques: attribute subset selection, wavelet transforms, PCA (Principal Component Analysis), histograms, sampling.

---

### Q. (OR) Explain Similarity and Distance measures with examples.

Measuring similarity/dissimilarity is essential for clustering, classification, and pattern mining.

**1. Euclidean Distance**
Straight-line distance between two points.
`d(x,y) = √[Σ(xᵢ − yᵢ)²]`
*Example: Distance between points (2,3) and (5,7) = √[(5−2)² + (7−3)²] = √(9+16) = 5*

**2. Manhattan Distance (City Block Distance)**
Sum of absolute differences between coordinates.
`d(x,y) = Σ|xᵢ − yᵢ|`
*Example: For (2,3) and (5,7): |5−2| + |7−3| = 3+4 = 7*

**3. Cosine Similarity**
Measures the angle between two vectors, often used in text mining/document similarity.
`cos(θ) = (A·B) / (‖A‖‖B‖)`
Value ranges from -1 to 1 (1 = identical direction).

**4. Jaccard Coefficient**
Used for binary/categorical data — measures similarity between finite sets.
`J(A,B) = |A∩B| / |A∪B|`
*Example: If A={1,2,3} and B={2,3,4}, then J = |{2,3}| / |{1,2,3,4}| = 2/4 = 0.5*

---

## SECTION C — 16 MARK QUESTIONS (Either/Or Pairs — Practice These Numericals!)

## PAIR 1

### Q. Explain the Apriori Algorithm in detail with a solved example.

**Concept:**
Apriori is a classic algorithm for mining frequent itemsets and generating association rules. It uses the **downward closure (Apriori) property**: any subset of a frequent itemset must also be frequent.

**Steps of the Algorithm:**
1. Scan the database and count support for each individual item (1-itemsets). Keep those meeting minimum support → this forms **L1**.
2. Generate candidate 2-itemsets (**C2**) by joining L1 with itself. Scan database, calculate support, prune those below minimum support → **L2**.
3. Generate candidate 3-itemsets (**C3**) from L2 using the join step, then prune using the Apriori property (remove candidates whose subsets are not frequent).
4. Repeat until no more frequent itemsets can be generated.
5. Generate **association rules** from the final frequent itemsets using minimum confidence.

**Solved Example:**

Given transactions (min support = 2, i.e., 50% for 4 transactions; min confidence = 70%):

| TID | Items |
|---|---|
| T1 | {Bread, Milk} |
| T2 | {Bread, Diaper, Beer, Eggs} |
| T3 | {Milk, Diaper, Beer, Coke} |
| T4 | {Bread, Milk, Diaper, Beer} |

**Step 1 — Candidate 1-itemsets (C1) and support count:**
| Item | Count |
|---|---|
| Bread | 3 |
| Milk | 3 |
| Diaper | 3 |
| Beer | 3 |
| Eggs | 1 |
| Coke | 1 |

Min support count = 2 → **L1** = {Bread, Milk, Diaper, Beer} (Eggs and Coke removed)

**Step 2 — Candidate 2-itemsets (C2):**
| Itemset | Count |
|---|---|
| {Bread, Milk} | 2 |
| {Bread, Diaper} | 2 |
| {Bread, Beer} | 2 |
| {Milk, Diaper} | 2 |
| {Milk, Beer} | 2 |
| {Diaper, Beer} | 3 |

All satisfy min support ≥ 2 → **L2** = all six pairs above.

**Step 3 — Candidate 3-itemsets (C3):**
Join L2 → possible candidates: {Bread, Milk, Diaper}, {Bread, Diaper, Beer}, {Milk, Diaper, Beer}

Counting from transactions:
| Itemset | Count |
|---|---|
| {Bread, Milk, Diaper} | 1 |
| {Bread, Diaper, Beer} | 2 |
| {Milk, Diaper, Beer} | 2 |

**L3** = {Bread, Diaper, Beer}, {Milk, Diaper, Beer} (support ≥ 2)

No further 4-itemsets can be formed → Algorithm stops.

**Step 4 — Generate Association Rules (from {Diaper, Beer, Milk}, support=2):**
- Rule: Diaper, Beer → Milk
  Confidence = Support({Diaper,Beer,Milk}) / Support({Diaper,Beer}) = 2/3 = 66.7% → **rejected** (below 70%)
- Rule: Milk, Beer → Diaper
  Confidence = 2/2 = 100% → **accepted** ✅
- Rule: Diaper, Milk → Beer
  Confidence = 2/2 = 100% → **accepted** ✅

**Conclusion:** The frequent itemsets and strong rules generated help identify patterns such as "customers who buy Milk and Beer also buy Diapers."

---

### Q. (OR) Explain Data Warehouse and Data Warehouse Modelling in detail.

*(Combine your answers from: Data Warehouse definition (Section A, Q6) + Schema types (Section B, Pair 1) + OLAP vs OLTP (Section A, Q7) + OLAP operations (Section B, Pair 1) + Data Cube Computation below for the full 16-mark answer.)*

**Data Cube Computation:**
- A data cube stores pre-computed aggregated values across multiple dimensions to speed up OLAP queries.
- **Full cube computation**: pre-compute all possible aggregations across every combination of dimensions (fast query, but very high storage cost).
- **Partial/iceberg cube computation**: only compute cells whose aggregate value satisfies a threshold condition (saves space).
- Efficient computation uses **multiway array aggregation**, **BUC algorithm**, or **Star-Cubing** to avoid recomputation and redundant scans.

---

## PAIR 2

### Q. Explain the FP-Growth Algorithm in detail with a solved example.

**Concept:**
FP-Growth (Frequent Pattern Growth) mines frequent itemsets **without generating candidate itemsets** (unlike Apriori), making it faster on large datasets. It compresses the database into a compact structure called the **FP-tree** and mines patterns directly from it.

**Steps:**
1. Scan the database once, find frequent 1-itemsets, and sort them in descending order of support (frequency descending list).
2. Scan the database again; for each transaction, keep only frequent items, sorted by the same order, and insert into the FP-tree (shared prefixes are merged, with counters incremented).
3. Once the FP-tree is built, mine it recursively:
   - For each item (starting from the least frequent), construct its **conditional pattern base** (prefix paths).
   - Build a **conditional FP-tree** from this base.
   - Recursively mine the conditional FP-tree to extract frequent patterns.

**Solved Example:**

Using the same transactions (min support count = 2):

| TID | Items |
|---|---|
| T1 | {Bread, Milk} |
| T2 | {Bread, Diaper, Beer, Eggs} |
| T3 | {Milk, Diaper, Beer, Coke} |
| T4 | {Bread, Milk, Diaper, Beer} |

**Step 1 — Frequency of items (descending order):**
Bread=3, Milk=3, Diaper=3, Beer=3 (Eggs=1, Coke=1 dropped, below min support)

Order used: Bread, Milk, Diaper, Beer (ties broken alphabetically/by convenience)

**Step 2 — Reorder each transaction by this frequency order:**
| TID | Ordered Items |
|---|---|
| T1 | Bread, Milk |
| T2 | Bread, Diaper, Beer |
| T3 | Milk, Diaper, Beer |
| T4 | Bread, Milk, Diaper, Beer |

**Step 3 — Build the FP-tree:**
- Root
  - Bread:3
    - Milk:1 (from T1)
    - Diaper:1 (from T2) → Beer:1
    - Milk:1 (from T4) → Diaper:1 → Beer:1
  - Milk:1 (from T3, since T3 doesn't start with Bread)
    - Diaper:1 → Beer:1

(Shared prefixes like "Bread" are merged into one branch with a count, rather than repeated.)

**Step 4 — Mine conditional pattern bases (example for "Beer"):**
Beer appears in paths: {Bread, Diaper}, {Bread, Milk, Diaper}, {Milk, Diaper}
→ Conditional pattern base of Beer = {(Bread, Diaper):1, (Bread, Milk, Diaper):1, (Milk, Diaper):1}

Building the conditional FP-tree for Beer, Diaper appears in all 3 paths → {Diaper, Beer} is frequent with support 3.

Continuing this recursively for each item produces all frequent itemsets — matching what Apriori found, but **without generating any candidate sets**, making FP-Growth more efficient on large/dense datasets.

**Advantage over Apriori:** No candidate generation, only 2 database scans needed (vs. multiple scans in Apriori), so it's much faster for large datasets with many frequent items.

---

### Q. (OR) Explain Data Cleaning and Data Integration in detail, along with the issues faced.

*(Use the detailed content from Section B, Pair 2, Q1 — expand each point with 2-3 lines and include real-world examples: e.g., a missing "age" field filled using the mean age; a customer record duplicated across two merged databases due to different ID formats.)*

**Additional issues to mention for full marks:**
- **Handling noisy data**: Binning (sort data into bins, smooth by bin means/boundaries), Regression (fit data to a function), Clustering (detect and remove outliers).
- **Handling missing data**: Ignore the tuple, fill manually, use a global constant, use attribute mean/median, or use the most probable value (via regression/decision tree/Bayesian inference).
- **Data integration challenges**: schema integration, entity identification, redundancy detection via correlation analysis (chi-square test for categorical data, correlation coefficient for numeric data), and detecting/resolving data value conflicts across sources.

---

## QUICK REVISION CHECKLIST (Night Before)

- [ ] Write out the Apriori algorithm steps + solve one numerical from scratch
- [ ] Write out the FP-Growth algorithm steps + build one FP-tree from scratch
- [ ] Draw Star schema and Snowflake schema diagrams from memory
- [ ] List all 5 OLAP operations with one example each
- [ ] List all 4 preprocessing steps (Cleaning, Integration, Transformation, Reduction) with 2 techniques each
- [ ] Memorize the 4 distance/similarity formulas (Euclidean, Manhattan, Cosine, Jaccard)
- [ ] Revise all 12 definitions in Section A

**Good luck for your exam tomorrow!**
