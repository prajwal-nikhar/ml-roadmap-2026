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

### Next Steps
Day 3: Pandas Basics — Series, DataFrames, indexing with loc/iloc, filtering
