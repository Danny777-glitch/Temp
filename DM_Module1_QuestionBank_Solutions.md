# Data Mining — Question Bank Solutions (Module I: CO1 & CO2)

---

# PART A — Short Answer Questions (All 26, with Answers)

### Q1. Classify: a) Job title b) Age c) Grade d) Gender
- **Job title** → Nominal
- **Age** → Numeric (Ratio)
- **Grade** → Ordinal
- **Gender** → Binary (Nominal, symmetric)

### Q2. Min-max normalize 73000 (income), min=25000, max=70000, range [0,1]
Formula: `v' = (v - min)/(max - min) × (new_max - new_min) + new_min`
v' = (73000 − 25000)/(70000 − 25000) = 48000/45000 = **1.067**
*(Note: since 73000 exceeds the stated max of 70000, the normalized value exceeds 1 — this is expected/acceptable and worth mentioning in your answer.)*

### Q3. Equal-frequency partitioning + smoothing by bin boundaries
Data: 5,10,11,13,15,35,50,55,72,92,204,215 (12 values → 3 bins of 4)

| Bin | Values | Boundaries |
|---|---|---|
| Bin 1 | 5, 10, 11, 13 | 5, 13 |
| Bin 2 | 15, 35, 50, 55 | 15, 55 |
| Bin 3 | 72, 92, 204, 215 | 72, 215 |

**Smoothing by bin boundaries** (each value replaced by nearest boundary):
- Bin 1: 5→**5**, 10→**13** (closer to 13), 11→**13**, 13→**13**
- Bin 2: 15→**15**, 35→tie (20 from each side, take **15**), 50→**55**, 55→**55**
- Bin 3: 72→**72**, 92→**72** (closer to 72), 204→**215**, 215→**215**

### Q4. Five-number summary of rank data
Data (17 values): 23,25,26,29,30,31,32,32,35,40,43,45,46,50,55,56,60
- **Min = 23, Max = 60**
- **Median (Q2)** = 9th value = **35**
- **Q1** = median of first 8 values (23,25,26,29,30,31,32,32) = avg(29,30) = **29.5**
- **Q3** = median of last 8 values (35,40,43,45,46,50,55,56) = avg(45,46) = **45.5**

**Five-number summary: {23, 29.5, 35, 45.5, 60}**

### Q5. Min-max normalize 23000, min=10000, max=65000, range [0,1]
v' = (23000 − 10000)/(65000 − 10000) = 13000/55000 = **0.236**

### Q6. Handling redundancy in data integration
- Use **correlation analysis**: Chi-square test for nominal attributes, correlation coefficient (Pearson's r) and covariance for numeric attributes.
- Careful integration of metadata (schema) from different sources to detect same real-world entity stored under different attribute names.
- Remove duplicate attributes/tuples once redundancy is confirmed.

### Q7. Identify attribute types
- **Employee Designation** → Nominal
- **Pizza_Taste** → Ordinal
- **Pin_Code** → Nominal (numeric-looking but an identifier, no meaningful arithmetic)
- **Calendar_Dates** → Interval

### Q8. Data Lake vs Data Warehouse
| Data Lake | Data Warehouse |
|---|---|
| Stores raw data (structured + unstructured + semi-structured) | Stores processed, structured data |
| Schema-on-read | Schema-on-write |
| Used by data scientists for exploration/ML | Used by business analysts for reporting |
| Huge, flexible, low-cost storage | Optimized, curated, higher cost per GB |

### Q9. Five-number summary of age data
Data (24 values, sorted): 12,15,16,16,19,20,20,21,22,22,22,25,25,25,25,30,33,35,35,35,45,52,63,76
- **Min = 12, Max = 76**
- **Median** = avg(12th,13th) = avg(25,25) = **25**
- **Q1** = median of first 12 = avg(6th,7th) = avg(20,20) = **20**
- **Q3** = median of last 12 = avg(6th,7th of upper half) = avg(35,35) = **35**

**Five-number summary: {12, 20, 25, 35, 76}**

### Q10. distance(C2, C3) — binary attribute data
| | A | B | C | D |
|---|---|---|---|---|
| C2 | 1 | 1 | 0 | 0 |
| C3 | 0 | 1 | 1 | 1 |

Since "purchase = 1" is the meaningful match (asymmetric binary), use **Jaccard distance**:
- M11 (both 1) = 1 (attribute B)
- M10 (C2=1,C3=0) = 1 (attribute A)
- M01 (C2=0,C3=1) = 2 (attributes C, D)

Jaccard similarity = M11/(M01+M10+M11) = 1/(2+1+1) = **0.25**
**Jaccard distance = 1 − 0.25 = 0.75**

### Q11. Equal-frequency binning + smoothing by bin mean
Same bins as Q3:
- Bin 1 (5,10,11,13): mean = 39/4 = **9.75** → all values become 9.75
- Bin 2 (15,35,50,55): mean = 155/4 = **38.75** → all values become 38.75
- Bin 3 (72,92,204,215): mean = 583/4 = **145.75** → all values become 145.75

### Q12. Star schema for education data warehouse
**Fact table**: `Fact_Enrollment` (StudentID, CourseID, FacultyID, TimeID, Marks, Attendance_%, Credits_Earned)
**Dimension tables**:
- `Dim_Student` (StudentID, Name, Gender, DOB, Program)
- `Dim_Course` (CourseID, CourseName, Department, Credits)
- `Dim_Faculty` (FacultyID, Name, Department, Designation)
- `Dim_Time` (TimeID, Semester, AcademicYear)

### Q13. Distance between (22,1,42,10) and (20,0,36,8)
Euclidean distance:
d = √[(22−20)² + (1−0)² + (42−36)² + (10−8)²]
d = √[4 + 1 + 36 + 4] = √45 = **6.708**

### Q14. Equal-frequency partitioning + smoothing by mean
Data: 12,17,19,22,26,29,33,35,36,44,47,55 (12 values → 3 bins of 4)
- Bin 1 (12,17,19,22): mean = 70/4 = **17.5**
- Bin 2 (26,29,33,35): mean = 123/4 = **30.75**
- Bin 3 (36,44,47,55): mean = 182/4 = **45.5**

### Q15. Methods for handling missing data
1. Ignore the tuple (not good if many attributes missing)
2. Fill in manually
3. Use a global constant (e.g., "Unknown")
4. Use the attribute mean/median
5. Use the mean/median of the same class
6. Use the most probable value (via regression, decision tree, or Bayesian inference)

### Q16. How is correlation between two attributes measured?
- **Nominal attributes**: Chi-square (χ²) test
- **Numeric attributes**: Correlation coefficient (Pearson's r) and Covariance

### Q17 / Q25. Method for finding frequent itemsets without candidate generation
**FP-Growth (Frequent Pattern Growth)**
Steps in FP-tree construction:
1. Scan DB once → find frequent 1-itemsets, sort by descending support.
2. Scan DB again → for each transaction, keep only frequent items sorted by that order, and insert into the FP-tree, incrementing shared-prefix node counts.
3. Mine the FP-tree recursively via conditional pattern bases and conditional FP-trees for each item (starting from the least frequent).

### Q18. Support of Bread and Jam
T = 500000, Bread = 20000, Jam = 30000, Both = 10000
- Support(Bread) = 20000/500000 = **4%**
- Support(Jam) = 30000/500000 = **6%**
- Support(Bread, Jam) = 10000/500000 = **2%**

### Q19. Major(science) → status(undergraduate)
5000 students, 70% science = 3500, 64% undergrad = 3200, 56% of undergrads major in science
- Undergrads majoring in science = 56% × 3200 = 1792
- **Support** = 1792/5000 = **35.84%**
- **Confidence** = 1792/3500 (science majors) = **51.2%**

### Q20. Lift for Bread(yes) → Butter(No)
| | Butter(Yes) | Butter(No) | Total |
|---|---|---|---|
| Bread(Yes) | 10 | 20 | 30 |
| Bread(No) | 10 | 60 | 70 |
| Total | 20 | 80 | 100 |

- Support(Bread=yes, Butter=No) = 20/100 = 0.20
- Confidence = 20/30 = 0.667
- Support(Butter=No) = 80/100 = 0.80
- **Lift = 0.667/0.80 = 0.833** → Lift < 1, so Bread(yes) and Butter(No) are **negatively correlated**.

### Q21. Lift for {Laptop}→{Mouse}
Support(Laptop)=0.4, Support(Mouse)=0.5, Support(Laptop,Mouse)=0.3
**Lift = 0.3/(0.4×0.5) = 0.3/0.2 = 1.5**
Interpretation: Lift > 1 → Laptop and Mouse are **positively correlated**; buying a laptop increases the likelihood of buying a mouse.

### Q22. Lift for hamburgers→hotdogs
| | hotdogs | ¬hotdogs | Total |
|---|---|---|---|
| hamburgers | 2000 | 500 | 2500 |
| ¬hamburgers | 1000 | 1500 | 2500 |
| Total | 3000 | 2000 | 5000 |

- Support(hamburgers,hotdogs) = 2000/5000 = 0.4
- Confidence = 2000/2500 = 0.8
- Support(hotdogs) = 3000/5000 = 0.6
- **Lift = 0.8/0.6 = 1.33** → positively correlated

### Q23. How is Apriori's efficiency improved?
- **Hash-based technique**: hash itemsets into buckets to filter candidates early
- **Transaction reduction**: remove transactions that don't contain any frequent itemset
- **Partitioning**: divide DB into partitions, mine each separately
- **Sampling**: mine a random sample instead of the whole DB
- **Dynamic itemset counting**: add new candidates dynamically during scan

### Q24. Steps in association rule mining + measures used
1. **Find all frequent itemsets** — using the **support** measure (≥ min support threshold)
2. **Generate strong association rules** from frequent itemsets — using the **confidence** measure (≥ min confidence threshold)
(Additional measures used to judge rule interestingness: **lift**, **correlation**)

### Q26. Why is FP-Growth fast?
- No candidate generation step (unlike Apriori, which generates and tests many candidates)
- Compresses the whole database into a compact **FP-tree**
- Requires only **2 scans** of the database
- Uses a **divide-and-conquer** strategy — mines smaller, focused conditional pattern bases recursively instead of repeatedly scanning the full database

---
---

# PART B — Important Descriptive Questions (Selected, with Full Answers)

*(All Part B questions in this bank are CO1/CO2 = Module I topics, so any could appear. Below are the ones most likely to be asked and most valuable to prepare — especially the numericals, since these carry the most marks.)*

## Q1. Explain data cleaning and data integration with real-time examples.

**Data Cleaning** — fixes missing, noisy, or inconsistent data:
- *Missing values*: e.g., a "PurchaseDate" field left blank → fill using the most frequent value, or predict using regression.
- *Noisy data*: e.g., a sensor recording temperature as "5000°C" by error → detected via binning/regression/clustering and corrected or removed.
- *Inconsistent data*: e.g., "Male"/"M"/"male" all meaning the same thing → standardized to one format.

**Data Integration** — combines data from multiple sources:
- *Entity identification problem*: e.g., "Cust_ID" in System A = "Customer_Number" in System B — must be matched before merging.
- *Redundancy*: e.g., "Revenue" column present in both merged sources — detected using correlation/Chi-square analysis and removed.
- *Data value conflicts*: e.g., one source stores weight in kg, another in pounds — must be converted to a common unit before integration.

---

## Q4. Explain normalization in detail. Normalize: 200, 300, 400, 600, 1000

**a) Min-Max Normalization** [new_min=0, new_max=1]
Formula: `v' = (v−min)/(max−min)`, min=200, max=1000

| v | v' |
|---|---|
| 200 | 0 |
| 300 | 0.125 |
| 400 | 0.25 |
| 600 | 0.5 |
| 1000 | 1 |

**b) Z-score Normalization**
Mean = (200+300+400+600+1000)/5 = **500**
Variance = Σ(v−mean)²/5 = (90000+40000+10000+10000+250000)/5 = 400000/5 = 80000
Std. dev = √80000 ≈ **282.84**

| v | z = (v−500)/282.84 |
|---|---|
| 200 | −1.061 |
| 300 | −0.707 |
| 400 | −0.354 |
| 600 | 0.354 |
| 1000 | 1.768 |

**c) Decimal Scaling Normalization**
`v' = v/10^j` where j is smallest integer so that max|v'| < 1. Max value = 1000 → j = 4

| v | v' |
|---|---|
| 200 | 0.02 |
| 300 | 0.03 |
| 400 | 0.04 |
| 600 | 0.06 |
| 1000 | 0.10 |

**Why normalize?** Prevents attributes with large ranges (e.g., income in lakhs) from dominating attributes with small ranges (e.g., age) during distance calculations — essential for clustering, kNN, and neural network based methods.

---

## Q9. KDD process diagram + need for data mining

**Steps in KDD (Knowledge Discovery in Databases):**
```
Raw Data → Data Cleaning → Data Integration → Data Selection
        → Data Transformation → Data Mining → Pattern Evaluation
        → Knowledge Presentation
```
- **Data Cleaning**: remove noise/inconsistent data
- **Data Integration**: combine multiple sources
- **Data Selection**: retrieve relevant data for the task
- **Data Transformation**: consolidate data into forms suitable for mining
- **Data Mining**: apply algorithms to extract patterns
- **Pattern Evaluation**: identify truly interesting patterns
- **Knowledge Presentation**: visualize/report results to the user

**Need for Data Mining**: With huge volumes of data generated daily, manual analysis is impossible. Data mining automatically discovers hidden patterns, trends, and relationships to support decision-making, forecasting, and strategy formulation — turning raw data into actionable knowledge.

---

## Q14. Star schema (date, spectator, location, game / measures: count, charge) + OLAP operations

**a) Star Schema:**
```
                Dim_Date
                   |
Dim_Spectator — Fact_Game(charge, count) — Dim_Location
                   |
                Dim_Game
```
Fact table: `Fact_Game` (DateID, SpectatorID, LocationID, GameID, count, charge)

**b) OLAP operations to find total charge paid by student spectators at GM_Place in 2010:**
1. **Roll-up** the date dimension from day-level to year-level (2010).
2. **Slice** on Location = "GM_Place".
3. **Dice** (or further slice) on Spectator_Category = "Student".
4. **Aggregate** (sum) the `charge` measure over the remaining cells.

So the sequence is: Roll-up (date→year) → Slice (location) → Dice (spectator=student) → sum(charge).

---

## Q19. Star, snowflake, and fact constellation schema for an online store

Tables: Customer, Product, Shipment, Date

**Star Schema**: One fact table `Fact_Orders`(OrderID, CustomerID, ProductID, ShipmentID, DateID, Quantity, SalesAmount) directly linked to denormalized `Customer`, `Product`, `Shipment`, `Date` dimension tables.

**Snowflake Schema**: Dimension tables normalized further — e.g., `Product` → `Product` + `Category`; `Customer` → `Customer` + `Location`. Reduces redundancy, saves storage, but needs more joins.

**Fact Constellation (Galaxy) Schema**: Multiple fact tables — e.g., `Fact_Orders` and `Fact_Shipment` — sharing common dimensions like `Date` and `Customer`. Supports analyzing multiple business processes together.

**Business value**: Star schema → fast sales-trend queries for marketing dashboards. Snowflake → cleaner category-level analysis with less redundancy. Fact constellation → combined analysis of orders + shipment/delivery performance for strategy decisions.

---

## Q21. Apriori Algorithm — 5 transactions, min support = 60%, min confidence = 70%

| TID | Items |
|---|---|
| T1 | A,B,C,D,E,F |
| T2 | B,C,D,E,F,G |
| T3 | A,D,E,H |
| T4 | A,D,F,I,J |
| T5 | B,D,E,K |

Min support count = 60% × 5 = **3**

**C1 → L1** (item : count): A=3, B=3, C=2(✗), D=5, E=4, F=3, others=1(✗)
**L1 = {A, B, D, E, F}**

**C2 → L2** (pairs from L1, count ≥3):
AD=3 ✓, BD=3 ✓, BE=3 ✓, DE=4 ✓, DF=3 ✓
(AB=1✗, AE=2✗, AF=2✗, BF=2✗, EF=2✗ — all dropped)
**L2 = {AD, BD, BE, DE, DF}**

**C3 → L3** (joined from L2, pruned via Apriori property):
- BDE (from BD+BE+DE, all in L2 ✓) → count = 3 (T1,T2,T5) → **frequent**
- DEF (from DE+DF, but EF not in L2 ✗) → pruned
**L3 = {BDE : 3}**

No further candidates possible → **stop**.

**Frequent itemsets**: {A,B,D,E,F}, {AD,BD,BE,DE,DF}, {BDE}

**Strong association rules (confidence ≥ 70%)** — from BDE (support 3/5=60%):
- B,D → E : 3/3 = **100%** ✓
- B,E → D : 3/3 = **100%** ✓
- E,D → B : 3/4 = **75%** ✓
- B → D,E : 3/3 = **100%** ✓
- E → B,D : 3/4 = **75%** ✓
- D → B,E : 3/5 = 60% ✗ (rejected)

Also from pairs: A→D (3/3=100% ✓), B→D (3/3=100% ✓), B→E (3/3=100% ✓), D→E (4/5=80% ✓), E→D (4/4=100% ✓), F→D (3/3=100% ✓)

---

## Q22. FP-Growth — 6 transactions, min support = 20%

| TID | Items |
|---|---|
| T1 | A,B,E |
| T2 | B,C,D |
| T3 | B,D,E |
| T4 | C,D,E |
| T5 | B,C,D,E |
| T6 | B,C,E |

Min support count = 20% × 6 = 1.2 → **round up to 2**

**Item counts**: A=1(✗), B=5, C=4, D=4, E=5
**L1 (frequency order)**: B(5), E(5), C(4), D(4)

**Reorder each transaction** (drop A, order B-E-C-D):
T1: B,E | T2: B,C,D | T3: B,E,D | T4: E,C,D | T5: B,E,C,D | T6: B,E,C

**FP-tree:**
```
Root
├── B:5
│    ├── E:4
│    │    ├── D:1        (from T3)
│    │    └── C:2
│    │         └── D:1   (from T5)
│    └── C:1              (from T2)
│         └── D:1
└── E:1                    (from T4, no B)
     └── C:1
          └── D:1
```

**Mining conditional pattern bases (sample workings):**
- For **D**: pattern base = {(B,E,C):1, (B,E):1, (B,C):1, (E,C):1} → total count 4 ✓
- For **C**: pattern base = {(B,E):2, (B):1, (E):1} → total count 4 ✓
- For **E**: pattern base = {(B):4} + direct → total count 5 ✓

**Final frequent itemsets (matches Apriori on the same data):**

| Size | Itemsets (count) |
|---|---|
| 1 | B(5), E(5), C(4), D(4) |
| 2 | BE(4), BC(3), BD(3), EC(3), ED(3), CD(3) |
| 3 | BEC(2), BED(2), BCD(2), ECD(2) |

(4-itemset BECD = only 1 → not frequent)

**Advantage shown here**: FP-Growth found the same frequent itemsets as Apriori would, but without ever generating and testing candidate sets — it only needed 2 database scans total.

---

## Q23. Apriori — 4 transactions, min support count = 2, min confidence = 50%

| TID | Items |
|---|---|
| 1 | A,B,C |
| 2 | B,C,D |
| 3 | A,C,D |
| 4 | A,B,C,D |

**L1**: A=3, B=3, C=4, D=3 (all ≥2) → **L1 = {A,B,C,D}**

**L2** (all pairs, count≥2): AB=2, AC=3, AD=2, BC=3, BD=2, CD=3 → **all 6 pairs frequent**

**L3**: ABC=2 ✓, ABD=1 ✗(dropped), ACD=2 ✓, BCD=2 ✓
**L3 = {ABC, ACD, BCD}**

**L4**: ABCD — subset ABD not frequent → pruned. **L4 = ∅**

**Strong rules (confidence ≥ 50%)** — sample from ABC(2):
- A,B→C: 2/2=100% ✓ | A,C→B: 2/3=67% ✓ | B,C→A: 2/3=67% ✓
- C→A,B: 2/4=50% ✓ | A→B,C: 2/3=67% ✓ | B→A,C: 2/3=67% ✓

From ACD(2): A,D→C=100% ✓ | A,C→D=67% ✓ | C,D→A=67% ✓ | C→A,D=50% ✓
From BCD(2): B,D→C=100% ✓ | B,C→D=67% ✓ | C,D→B=67% ✓ | C→B,D=50% ✓

*(At only 50% minimum confidence, nearly every rule generated turns out to be "strong" — a useful thing to point out in your answer.)*

---

## Q27. Market Basket Analysis — Supermarket (min support count=2, min confidence=60%)

| TID | Items |
|---|---|
| 1 | Milk, Bread, Butter |
| 2 | Bread, Eggs, Butter |
| 3 | Milk, Bread, Eggs |
| 4 | Milk, Eggs, Butter, Cheese |
| 5 | Bread, Cheese |
| 6 | Milk, Bread, Cheese, Butter |

**L1**: Milk=4, Bread=5, Butter=4, Eggs=3, Cheese=3 (all ≥2)

**L2**: Milk-Bread=3, Milk-Butter=3, Milk-Eggs=2, Milk-Cheese=2, Bread-Butter=3, Bread-Eggs=2, Bread-Cheese=2, Butter-Eggs=2, Butter-Cheese=2
(Eggs-Cheese=1 ✗ dropped)

**L3**: Milk-Bread-Butter=2 ✓, Milk-Butter-Cheese=2 ✓ (others fail support≥2)

**Strong rules (≥60%):**
- Milk,Bread→Butter: 2/3=67% ✓
- Milk,Butter→Bread: 2/3=67% ✓
- Bread,Butter→Milk: 2/3=67% ✓
- Milk,Cheese→Butter: 2/2=100% ✓
- Butter,Cheese→Milk: 2/2=100% ✓
- Milk,Butter→Cheese: 2/3=67% ✓

**Recommendation for store manager**: Since {Milk, Butter, Cheese} and {Milk, Bread, Butter} show strong bidirectional rules, place **dairy items (Milk, Butter, Cheese) together** as a cross-sell zone, and consider a **combo discount on Milk+Bread+Butter**, a common breakfast basket.

---

## QUICK PRIORITY LIST FOR TOMORROW (given limited time)
1. **Apriori numerical** (Q21 or Q23 style) — practice by hand once more
2. **FP-Growth numerical** (Q22 style) — practice building one FP-tree
3. **Normalization** (min-max, z-score, decimal scaling) — Q4/Q3/Q5 style, very likely to appear
4. **Five-number summary** — Q4/Q9 style, quick and easy marks
5. **Lift calculation** — Q20/Q21/Q22 style from a contingency table, quick and formulaic
6. **Star/Snowflake/Fact Constellation schema** — draw once from memory
7. **OLAP operations** with one example each

**All the best for your exam!**
