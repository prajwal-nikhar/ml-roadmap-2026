# AI & ML 8-Week Roadmap

## Day 1: Python Foundations & NumPy

### Topics Covered
- Python basics refresher: variables, loops, functions, comprehensions
- NumPy fundamentals: array creation, indexing, slicing, reshaping, broadcasting
- Manual implementation of statistical measures (mean, median, std dev) verified against NumPy

### Files
- `day1_python_numpy_basics.ipynb` — NumPy array exercises, custom stats function, and Python practice problems

### What I Learned
- How NumPy arrays differ from Python lists in memory layout and performance
- Broadcasting rules for operations between arrays of different shapes
- How to manually compute statistical measures and validate them against library functions
- Python fundamentals: comprehensions, dictionary operations, nested data handling

### Key Takeaways
- Vectorized NumPy operations are significantly faster than Python loops for numerical work
- `np.std()` uses population standard deviation (ddof=0) by default, not sample std dev
- Broadcasting lets you operate on arrays of different shapes without explicit loops

## Day 2: NumPy Deep Dive & Practice Problems

### Topics Covered
- NumPy aggregations along axes (sum, max, cumulative operations)
- Vectorization vs loops: measuring real performance difference
- Matrix operations: dot product, matrix multiplication, transpose, inverse, determinant

### Files
- `day2_numpy_advanced.ipynb` — Axis-wise aggregations, vectorization speed test, matrix operation exercises

### What I Learned
- `axis=0` operates column-wise, `axis=1` operates row-wise (a common source of confusion)
- Vectorized NumPy operations were ~[X]x faster than equivalent Python loops on 1M elements
- NumPy operations run in compiled C under the hood, avoiding Python's per-element interpreter overhead — this is the core reason for the speedup
- Matrix multiplication (`@` or `np.dot`) differs from element-wise multiplication (`*`)
- Not all matrices are invertible — `np.linalg.inv()` requires a square, non-singular matrix

### Key Takeaways
- Always prefer vectorized NumPy operations over explicit Python loops when working with numerical arrays
- `np.linalg` module handles core linear algebra operations needed for ML (inverse, determinant, eigenvalues later in Week 6)

## Day 3: Pandas Basics

### Topics Covered
- Series: creation from lists, dicts, custom indexes; vectorized operations on Series
- DataFrame: creation, all core exploration methods (shape, info, describe, dtypes, value_counts)
- loc vs iloc: label-based vs position-based indexing — including the custom index gotcha
- Filtering: single condition, multiple conditions (&, |, ~), isin(), between(), str methods, query()
- Loaded Netflix dataset: applied real filters (type, release year, country)

### Files
- `day3_pandas_basics.ipynb` — Series deep dive, DataFrame exploration, loc/iloc comparison, boolean indexing, Netflix CSV filters

### What I Learned
- A DataFrame is a collection of Series sharing the same index — each column is a Series
- `loc` is label-based and inclusive on both ends of a slice; `iloc` is position-based and exclusive on the right (like Python slicing)
- With a custom index (e.g. 10, 20, 30), `loc[10]` and `iloc[0]` both return the first row but for entirely different reasons — easy bug to miss
- Boolean filtering uses `&`, `|`, `~` not Python's `and`/`or`/`not` — parentheses around each condition are mandatory
- `query()` offers cleaner readable syntax for multi-condition filters
- `.isnull().sum()` is the first thing to run on any new dataset to understand data quality

### Key Takeaways
- Always run `.shape`, `.info()`, `.describe()`, `.isnull().sum()` the moment you load any new dataset
- `loc` for when you know column/index names; `iloc` for when you need positional slicing
- Netflix dataset has significant null values in `country`, `cast`, `director` — will need handling in Week 2

## Day 4: Pandas Data Manipulation

### Topics Covered
- groupby: split-apply-combine pattern, agg with multiple functions, transform (adding group stats back to DataFrame), filter by group condition
- merge / join: inner, left, right, outer joins; chaining multiple merges; joining on different column names
- apply / map: element-wise map on Series, row-wise and column-wise apply on DataFrame, lambda functions
- Sorting: single column, multiple columns with mixed ascending/descending order, sort by index
- Duplicates: detecting exact and subset duplicates, drop_duplicates with keep='first'/'last'

### Files
- `day4_pandas_manipulation.ipynb` — groupby aggregations, merge join types, apply/map operations, sorting and duplicate handling on sample + Netflix dataset

### What I Learned
- groupby follows split → apply → combine: split data into groups, apply a function, combine results back
- `transform` returns a same-length Series so you can add group-level stats (e.g. course average) back as a new column — unlike `agg` which collapses rows
- merge `how` parameter mirrors SQL joins exactly: inner keeps only matches, left keeps all left rows, outer keeps everything
- `apply(func, axis=1)` runs the function row-wise; `axis=0` runs column-wise — easy to mix up
- `map` is for element-wise transformation on a single Series; `apply` is for more complex row/column logic on a DataFrame
- `drop_duplicates(subset=['col'], keep='last')` lets you control which duplicate to retain

### Key Takeaways
- `transform` is underused but powerful — lets you enrich a DataFrame with group-level context without losing rows
- Always check for duplicates early in any EDA — `df.duplicated().sum()` before any analysis
- Chained merges are the Pandas equivalent of multi-table SQL joins

## Day 5: Matplotlib & Data Visualization

### Topics Covered
- Line plots: trends over time, multiple lines, markers, grid styling
- Bar plots: vertical and horizontal, value labels on bars, sorting by data
- Scatter plots: correlation visualization, color by category, annotation
- Histograms: distribution comparison, mean lines, overlapping distributions
- Subplots: multi-plot figures using plt.subplots(), shared layout with suptitle
- Applied EDA visualizations on Netflix dataset (content type, yearly trends, ratings)

### Files
- `day5_matplotlib_visualization.ipynb` — all plot types with customization, subplot grid, Netflix EDA plots
- `line_plot.png` — streaming platform growth comparison
- `bar_plots.png` — students per course (vertical) + avg marks per course (horizontal)
- `scatter_plot.png` — study hours vs marks with correlation annotation
- `histogram.png` — marks distribution comparison between two classes
- `day5_all_plots.png` — 2x2 subplot grid combining all four chart types
- `netflix_eda_plots.png` — Movies vs TV Shows, content per year, top ratings

### What I Learned
- `plt.subplots(rows, cols)` returns a fig and axes array — use `axes[i]` or `axes[i,j]` to target each subplot
- `figsize` controls the overall figure size; increase width when plotting side-by-side charts to avoid clipping
- `bbox_inches='tight'` in `savefig` prevents labels and titles from getting cut off
- Sort each chart independently using its own metric — sorting by avg_marks and then plotting students gives wrong order
- `xlim` on horizontal bar charts prevents value labels from being clipped at the edge
- `np.corrcoef(x, y)[0,1]` gives the Pearson correlation coefficient — useful to annotate scatter plots
- Overlapping histograms need `alpha < 1` to stay readable; adding mean lines with `axvline` makes distributions easier to compare

### Key Takeaways
- Always use `tight_layout()` before `savefig` to prevent subplot overlap
- Color consistency across related charts improves readability
- Scatter plots should always show a reference line (threshold, mean) to give context to the distribution
- For horizontal bar charts, sort ascending so the longest bar is at the top — matches natural reading direction

## Day 6: Linear Algebra & Statistics Basics

### Topics Covered
- Vectors: addition, subtraction, scalar multiplication, dot product, magnitude, unit vector, cosine similarity
- Matrices: element-wise vs matrix multiplication, transpose, identity, determinant, inverse, eigenvalues/eigenvectors
- Solving linear equations using numpy (Ax = b)
- Statistics: mean, median, mode, variance, std dev (population vs sample), IQR, skewness, kurtosis
- Probability distributions: Normal, Binomial, Uniform — PDF, CDF, 68-95-99.7 rule
- Z-scores: standardization, interpretation, outlier detection

### Files
- `day6_linear_algebra_statistics.ipynb` — vectors, matrix ops, statistics fundamentals, distributions, z-scores
- `vectors.png` — vector addition visualization using quiver plot
- `statistics.png` — histogram with mean/median lines + box plot
- `distributions.png` — Normal, Binomial, Uniform distributions side by side

### What I Learned
- Dot product measures alignment between vectors — foundation of neural network weight calculations
- Cosine similarity = dot product / (magnitude of v1 × magnitude of v2) — used in NLP and recommendation systems
- `np.var(data, ddof=1)` for sample variance, `ddof=0` (default) for population variance — wrong ddof gives wrong results
- Eigenvalues and eigenvectors of a matrix are the foundation of PCA (coming in Week 6)
- Z-score = (value - mean) / std — standardized scores always have mean=0, std=1
- 68-95-99.7 rule: 68% of data falls within ±1σ, 95% within ±2σ, 99.7% within ±3σ of the mean
- `quiver` in Matplotlib draws arrows — it does not support linestyle parameter unlike line plots

### Key Takeaways
- Linear algebra is the backbone of ML — matrix multiplication is what happens inside every neural network forward pass
- Population std vs sample std matters: use ddof=1 when working with a sample of a larger dataset
- Z-scores above |2| are typically flagged as outliers — same principle used in Week 2's outlier detection
- Normal distribution CDF via `stats.norm.cdf()` gives exact probabilities — more precise than the 68-95-99.7 rule

## Day 7: Netflix Data Analysis Project (Week 1 Capstone)

### Topics Covered
- End-to-end EDA pipeline: load → clean → analyze → visualize
- Data cleaning: duplicate removal, missing value imputation, datetime parsing, feature extraction
- GroupBy aggregations on real dataset
- Multi-plot visualization dashboard across 4 figures
- NumPy statistical summary on project data

### Files
- `day7_netflix_analysis.ipynb` — full EDA pipeline across 7 cells
- `netflix_overview.png` — Movies vs TV Shows count + content added per year trend
- `netflix_genre_rating.png` — Top 10 genres + rating distribution
- `netflix_country_year.png` — Top 10 producing countries + release year histogram
- `netflix_duration.png` — Movie duration distribution + TV show seasons breakdown

### What I Learned
- `df['col'] = df['col'].fillna(...)` is the correct Pandas 3.0 syntax — `inplace=True` on chained assignments is deprecated and will break in future versions
- Always check column dtype before calling `.str` accessor — if `date_added` is already datetime, `.str.strip()` throws AttributeError
- `df['listed_in'].str.split(', ').explode()` unpacks multi-value columns into individual rows for proper genre frequency analysis
- `str.extract(r'(\d+)')` pulls the first numeric value from a string column — clean way to separate duration from unit label
- `dt.year` and `dt.month` on datetime columns create useful temporal features for trend analysis

### Key Insights from Netflix Dataset
- Movies make up ~70% of Netflix content, TV Shows ~30%
- Content additions peaked around 2019–2020, slowed post-pandemic
- United States is the largest content producer by a significant margin
- TV-MA and TV-14 are the most common ratings — platform skews toward mature audiences
- Average movie duration is ~99 minutes; majority of TV shows have only 1 season

### Key Takeaways
- Real datasets always

## Day 8: Missing Value Handling

### Topics Covered
- Detecting missing values: isnull(), null percentage, missing value heatmap with Seaborn
- Dropping strategies: dropna(), subset drops, dropping high-null columns by threshold
- Mean / median / mode imputation for numerical and categorical columns
- Forward fill (ffill) and backward fill (bfill) for time-series ordered data
- KNN Imputation using Scikit-Learn for context-aware numerical imputation

### Files
- `day8_missing_values.ipynb` — full missing value handling pipeline across 5 cells
- `missing_heatmap.png` — heatmap showing missing value pattern across dataset
- `imputation_distribution.png` — distribution comparison before/after mean & median imputation
- `ffill_bfill.png` — forward fill vs backward fill on time-series Sales and Temperature data
- `knn_imputation.png` — distribution comparison before/after KNN imputation

### What I Learned
- `np.nan` is float-only — using it in `np.where` with string columns throws DTypePromotionError; use `None` instead for categorical columns
- `df.isnull().sum() / len(df) * 100` gives null percentage per column — essential first step before choosing imputation strategy
- Mean imputation distorts distribution by creating a spike at the mean — median is safer for skewed data
- ffill/bfill only make sense for time-ordered data — using them on random tabular data gives misleading results
- KNN imputation uses the K nearest neighbors (based on other features) to estimate missing values — more accurate than simple mean/median but computationally heavier
- `KNNImputer` only works on numerical columns — categorical columns must be encoded first or handled separately

### Imputation Strategy Decision Rule
| Missing % | Strategy |
|-----------|----------|
| < 5%      | Drop rows |
| 5–30%     | Mean / Median / Mode imputation |
| Time-series | ffill / bfill |
| Numerical with correlations | KNN imputation |
| > 30%     | Drop column or flag as separate binary feature |

### Key Takeaways
- Never impute blindly — always check distribution before and after to ensure imputation doesn't distort the data
- Mode imputation for categorical columns can introduce bias if one category is already dominant
- KNN imputation preserves relationships between features better than mean/median — preferred when features are correlated
- Always visualize missing patterns with a heatmap before deciding on a strategy

## Day 9: Outlier Detection

### Topics Covered
- Box plot visualization for outlier identification
- IQR (Interquartile Range) method: Q1, Q3, Tukey's 1.5×IQR rule
- Z-score method: standardized distance from mean, threshold-based detection
- Outlier handling strategies: removal, capping (Winsorization), log transformation
- Applied outlier analysis on Netflix movie duration data

### Files
- `day9_outlier_detection.ipynb` — full outlier detection pipeline across 6 cells
- `boxplots_outliers.png` — box plots for all 4 columns showing outlier points in red
- `outlier_strategies.png` — distribution comparison across 4 handling strategies for Salary
- `netflix_duration_outliers.png` — Netflix movie duration box plot + before/after cleanup

### What I Learned
- IQR = Q3 - Q1; outlier bounds are Q1 - 1.5×IQR (lower) and Q3 + 1.5×IQR (upper) — Tukey's method
- Z-score method is sensitive to extreme outliers because they inflate the std dev — IQR is more robust
- Z-score assumes normality; IQR works on any distribution — prefer IQR for skewed data
- Winsorization (clip to bounds) retains all rows while neutralizing outlier impact — better than removal when data is scarce
- `np.log1p()` compresses right-skewed distributions and large value ranges — always use log1p over log to safely handle zeros
- Red dots on box plots (flierprops) are data points beyond 1.5×IQR — visually identifies outliers instantly

### Outlier Handling Decision Rule
| Situation | Strategy |
|-----------|----------|
| Small dataset, can't afford to lose rows | Cap (Winsorize) |
| Large dataset, outliers are errors | Remove |
| Right-skewed distribution | Log transform |
| Time-series data | Flag as binary feature |
| Domain-specific valid extremes | Keep as-is |

### Key Takeaways
- Always visualize outliers with a box plot before deciding on a strategy
- Not all outliers are errors — a Netflix movie with 300 min duration is unusual but valid
- IQR is the default go-to; use Z-score only when data is confirmed to be normally distributed
- Log transformation is preferred when outliers are valid but distort model training

## Day 10: Feature Encoding

### Topics Covered
- Label Encoding: integer assignment per category, use cases and pitfalls
- One-Hot Encoding: binary column per category, dummy variable trap, drop='first'
- Ordinal Encoding: order-preserving integer mapping for ranked categories
- Encoding comparison: impact of encoding choice on model accuracy
- When to use each encoding type across different model families

### Files
- `day10_feature_encoding.ipynb` — full encoding pipeline across 5 cells with comparison experiment

### What I Learned
- Label Encoding on nominal features implies a false ordinal relationship — models learn HR < Finance < Sales < Tech which has no real meaning
- `drop='first'` in OneHotEncoder avoids the dummy variable trap — with N categories only N-1 columns are needed; the last is implied when all others are 0
- Ordinal Encoding requires explicitly defining category order — letting sklearn infer it alphabetically gives wrong rankings
- `pd.get_dummies()` is fastest for quick EDA; `sklearn OneHotEncoder` is better inside ML pipelines because it handles unseen categories at inference time
- `OrdinalEncoder` should only be used when the order is domain-meaningful (e.g. High School < Bachelor < Master < PhD) — never on arbitrary categories

### Encoding Decision Rule
| Encoding | Use When | Avoid When |
|----------|----------|------------|
| Label Encoding | Target variable, tree-based models | Nominal features in linear/logistic regression |
| One-Hot Encoding | Nominal categories, linear models | High cardinality columns (100+ unique values) |
| Ordinal Encoding | Categories with a clear meaningful order | Nominal categories with no natural ranking |

### Key Takeaways
- Encoding choice directly affects model performance — wrong encoding on linear models introduces false relationships
- High cardinality OHE (100+ dummies) causes dimensionality explosion — use target encoding or embeddings instead
- Tree-based models (Decision Tree, Random Forest, XGBoost) are largely insensitive to encoding choice — they split on values, not magnitudes
- Always define ordinal category order explicitly — never rely on alphabetical default

## Day 11: Feature Scaling

### Topics Covered
- Min-Max Scaling: rescaling to fixed range [0,1], custom ranges
- Standardization (Z-score): rescaling to mean=0, std=1
- RobustScaler: outlier-resistant scaling using median and IQR
- Train/test scaling discipline to prevent data leakage
- Impact of scaling on distance-based models (KNN)

### Files
- `day11_feature_scaling.ipynb` — full scaling pipeline across 5 cells
- `scaler_comparison.png` — box plot comparison of MinMax, Standard, and Robust scalers on outlier-contaminated data

### What I Learned
- Min-Max formula: `(X - X_min) / (X_max - X_min)` — bounded to [0,1] but highly sensitive to outliers since a single extreme value compresses the rest of the range
- Standardization formula: `(X - mean) / std` — not bounded to a fixed range, less sensitive to outliers than Min-Max but still affected since mean/std both shift with extreme values
- RobustScaler formula: `(X - median) / IQR` — median and IQR are not affected by extreme values, making this the most reliable choice when outliers are present
- KNN, SVM, and gradient-descent-based models (Linear/Logistic Regression) are scale-sensitive — tree-based models are not
- Critical rule: fit the scaler only on training data, then use `.transform()` (not `.fit_transform()`) on test data — fitting on test data causes data leakage and inflates performance metrics

### Scaler Decision Rule
| Scaler | Use When | Avoid When |
|--------|----------|------------|
| MinMaxScaler | Bounded range needed (neural nets, image pixels) | Outliers present |
| StandardScaler | Linear/Logistic Regression, SVM, PCA — default choice | Heavy outliers, non-normal data |
| RobustScaler | Data has known/confirmed outliers | Clean, outlier-free data |

### Key Takeaways
- Demonstrated with an injected outlier that MinMax and Standard scalers get visibly distorted while RobustScaler stays stable
- KNN accuracy changed measurably between unscaled and scaled versions of the same data — proof that scaling is not optional for distance-based models
- Always scale numerical features after train/test split, never before — fitting the scaler on the full dataset leaks test set information into training

## Day 12: Data Visualization with Seaborn

### Topics Covered
- histplot / kdeplot: distribution visualization, KDE curves, grouped distributions by hue
- boxplot: category-wise distribution comparison, hue-based grouping
- violinplot: distribution shape + summary statistics, split violin by gender
- pairplot: pairwise relationships across all numerical features, colored by category
- heatmap: full and masked (upper triangle) correlation matrices, interpretation guide
- Applied Seaborn EDA on Netflix dataset

### Files
- `day12_seaborn_visualization.ipynb` — full Seaborn pipeline across 6 cells
- `seaborn_distributions.png` — histogram, histogram+KDE, grouped KDE, stacked histplot
- `seaborn_boxplots.png` — boxplot by department, boxplot with hue, violin, split violin
- `seaborn_pairplot.png` — pairplot colored by promotion status
- `seaborn_pairplot_dept.png` — pairplot colored by department
- `seaborn_heatmap.png` — full and masked correlation heatmaps
- `netflix_seaborn_eda.png` — duration distribution, duration by type, ratings by content type

### What I Learned
- `distplot` is deprecated in newer Seaborn — use `histplot(kde=True)` for histogram + KDE and `kdeplot()` for KDE-only plots
- `hue` parameter in Seaborn plots splits data by a categorical column automatically — no need to manually filter and plot separately
- `multiple='stack'` in histplot stacks grouped bars instead of overlapping them — cleaner for multi-category comparisons
- Violin plots show the full distribution shape (KDE) wrapped around a box plot — more informative than a box plot alone
- `split=True` in violinplot shows male/female (or any binary category) distributions mirrored on each side — very efficient use of space
- `np.triu()` mask removes the upper triangle from the heatmap — avoids redundant mirror values since correlation matrix is symmetric
- Pairplot diagonal shows each feature's own distribution; off-diagonal shows scatter between every feature pair

### Key Takeaways
- Always use `sns.set_theme()` at the top of visualization notebooks — consistent styling across all plots
- Heatmap `center=0` ensures the colormap is centered at zero — critical for correlation maps where negative values matter
- Pairplot is slow on large datasets (>10k rows) — sample first with `df.sample(1000)` before calling pairplot
- Violin + split is the most space-efficient way to compare two groups across multiple categories simultaneously