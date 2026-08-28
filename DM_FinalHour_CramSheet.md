# FINAL HOUR CRAM SHEET — Data Mining Module I

*Read top to bottom. This covers everything with zero fluff.*

---

## ⏱️ TIME BUDGET (60 min)
- 0–15 min: Formulas + definitions (Section 1–2)
- 15–35 min: Practice 1 Apriori + 1 FP-Growth by hand (Section 3)
- 35–50 min: Schemas + OLAP + preprocessing steps (Section 4–5)
- 50–60 min: Skim 2-mark definitions once more (Section 6)

---

## 1. ALL FORMULAS (memorize these first)

| Concept | Formula |
|---|---|
| Min-Max Normalization | `v' = (v−min)/(max−min) × (new_max−new_min) + new_min` |
| Z-score Normalization | `z = (v − mean)/std_dev` |
| Decimal Scaling | `v' = v/10^j` (j = smallest int so max\|v'\|<1) |
| Euclidean Distance | `√[Σ(xᵢ−yᵢ)²]` |
| Manhattan Distance | `Σ\|xᵢ−yᵢ\|` |
| Jaccard Similarity (binary) | `M11/(M01+M10+M11)` |
| Jaccard Distance | `1 − Jaccard Similarity` |
| Support(A) | `count(A) / total transactions` |
| Support(A,B) | `count(A∪B) / total transactions` |
| Confidence(A→B) | `Support(A,B) / Support(A)` |
| Lift(A→B) | `Confidence(A→B) / Support(B)` = `Support(A,B)/[Support(A)×Support(B)]` |
| Lift interpretation | >1 positive correlation, =1 independent, <1 negative correlation |
| Mean (bin smoothing) | `Σvalues / n` |

**Five-number summary** = {Min, Q1, Median, Q3, Max}
- Median = middle value (avg of two middles if even count)
- Q1 = median of lower half, Q3 = median of upper half

---

## 2. ONE-LINE DEFINITIONS (2-markers — fire these off fast)

- **Data Mining**: discovering hidden patterns/knowledge from large data repositories.
- **KDD**: full pipeline — Clean → Integrate → Select → Transform → Mine → Evaluate → Present.
- **Data Quality dims**: Accuracy, Completeness, Consistency, Timeliness.
- **Data Warehouse**: subject-oriented, integrated, time-variant, non-volatile data store for decision-making.
- **OLTP vs OLAP**: OLTP = current data, simple fast transactions; OLAP = historical data, complex analytical queries.
- **Data Cube**: multidimensional structure for fast multi-angle aggregation.
- **Dimensionality Reduction**: reduce attribute count while keeping key info — cuts noise/cost/curse of dimensionality.
- **Frequent Itemset**: item set meeting minimum support.
- **Apriori property**: all subsets of a frequent itemset are frequent (downward closure); used to prune candidates.
- **Data Lake vs Warehouse**: Lake = raw/all formats, schema-on-read; Warehouse = processed/structured, schema-on-write.
- **Handling missing data**: ignore tuple, fill manually, global constant, mean/median, most probable value.
- **Correlation measurement**: Chi-square (nominal), Pearson correlation coefficient (numeric).
- **FP-Growth**: finds frequent itemsets without candidate generation, using a compressed FP-tree, only 2 DB scans.
- **Why FP-Growth is fast**: no candidate generation, compact tree, divide-and-conquer mining.
- **Redundancy in integration**: fixed via correlation analysis (χ² test / correlation coefficient).

---

## 3. THE TWO ALGORITHMS — STEP-BY-STEP RECIPE

### APRIORI (candidate generation + pruning)
1. Scan DB → count each single item → keep those ≥ min support → **L1**
2. Join L1 with itself → candidate pairs → count → keep ≥ min support → **L2**
3. Join L2 → candidate triples → **prune any candidate whose subset isn't in L2** (Apriori property) → count → **L3**
4. Repeat until no candidates remain.
5. From final frequent itemsets, generate rules: for itemset X, for every non-empty subset S, rule `S → (X−S)`, confidence = Support(X)/Support(S). Keep if confidence ≥ min confidence.

**Mini worked pattern** (4 transactions, min support=2):
- Count singles → L1
- Count all pairs → L2 (often ALL pairs survive if data is small/dense)
- Join pairs sharing prefix → triples → check via Apriori property → L3
- Try to extend to 4-itemset → usually pruned/fails count → STOP
- Generate rules from largest frequent itemsets first (best marks)

### FP-GROWTH (tree-based, no candidates)
1. Scan DB once → count items → drop below min support → sort remaining by **descending frequency**.
2. Scan DB again → reorder each transaction's items by that frequency order → insert into **FP-tree**, sharing common prefixes, incrementing counts.
3. For each item (starting from **least frequent**), build its **conditional pattern base** = all prefix paths leading to it.
4. Build a **conditional FP-tree** from that base; recursively mine it.
5. Combine to get all frequent itemsets — result set is IDENTICAL to what Apriori would find, just reached differently.

**Golden rule to write in your answer**: "FP-Growth avoids the costly candidate generation and multiple database scans of Apriori by compressing the database into an FP-tree and mining it recursively via conditional pattern bases."

---

## 4. SCHEMAS & OLAP — QUICK RECALL

### Star Schema
One **fact table** (numeric measures + foreign keys) in the center, connected directly to **denormalized** dimension tables. Fast queries, simple joins.

### Snowflake Schema
Like star, but dimension tables are **normalized** into sub-tables (e.g., Product → Product + Category). Less redundancy, more joins, slower.

### Fact Constellation (Galaxy)
**Multiple fact tables** sharing common dimension tables. Used for multiple business processes together.

### OLAP Operations (memorize with one example each)
| Operation | What it does | Example |
|---|---|---|
| Roll-up | Aggregate up a hierarchy | City → State → Country sales |
| Drill-down | Go to finer detail | Year → Quarter → Month |
| Slice | Fix one dimension | Sales for only "2024" |
| Dice | Fix multiple dimensions | Sales where Year=2024 AND Region=South |
| Pivot | Rotate axes for a new view | Swap rows/columns in the report |

---

## 5. DATA PREPROCESSING — 4-STEP RECALL

1. **Data Cleaning** → missing values (fill/ignore), noisy data (binning/regression/clustering), outliers, inconsistencies.
2. **Data Integration** → combine sources; issues: entity identification problem, redundancy (χ² test), value conflicts (units).
3. **Data Transformation** → smoothing, normalization (min-max/z-score/decimal), aggregation, generalization.
4. **Data Reduction** → attribute subset selection, PCA, sampling, histograms — keeps analysis fast without losing key info.

**Binning quick method**: sort data → split into equal-frequency bins → smooth by **mean** (replace all with bin average) or **boundaries** (replace with nearest min/max of bin).

---

## 6. LAST-MINUTE DEFINITION SPRINT (say these out loud once)

Data mining → KDD → data types (nominal/ordinal/interval/ratio) → data quality → data warehouse → OLTP vs OLAP → data cube → dimensionality reduction → frequent itemset/support/confidence → Apriori property → lift → data lake vs warehouse → missing data handling → correlation measurement → FP-Growth → why FP-Growth is fast.

If you can define all 16 of those in one line each, Section A is done.

---

## ✅ EXAM-HALL CHECKLIST
- [ ] Support/Confidence/Lift formulas written from memory
- [ ] Can build an FP-tree for a fresh 5-6 transaction dataset
- [ ] Can run Apriori through L1→L2→L3 and generate rules
- [ ] Can draw Star and Snowflake schema in under 1 minute
- [ ] Know all 5 OLAP operations with an example each
- [ ] Know the 4 preprocessing steps and 2 techniques under each

**You've got this — go crush it.**
