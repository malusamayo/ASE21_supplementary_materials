# Validation Rubrics

### What to look at?

You only need to look at **summary of the variable** written in the link! NO NEED to evaluate whether other variable's docs are correct or not.

E.g., for **[fifa-19-visualization.html#019[impute_by_median]](http://localhost:8889/fifa-19-visualization.html#019)**, you should check the docs of  'impute_by_median', not other variables!

When you click the page, the summary **at the top** is the one you should look at, not the one in the center.

### What might you encounter?

##### No documentation for the variable:

1. Check whether there is any input. If not, **no documentation** should be generated. It is likely using external sources (e.g., csv files) as inputs.
2. Check whether the variable is in the output. If not, it is likely that it is not used later. we **intentionally ignore** such dataframes by def-use analysis.
   1. You still need to check the code to see whether it is true (i.e., the variable is indeed not used). 

##### Multiple source columns for new columns:

+ A pattern like: `Size = float(str_transform(Cabin, Name))` DOES NOT imply that both columns are sources. Instead, it simply means that some subset of the two columns could be sources.
+ Therefore, as long as one src column is correct, the pattern should be marked as **correct**.
+ Also, one-hot-encoding columns need not necessarily be grouped together.
  + e.g., `col1 = one-hot-encoding(col); col2, cols3 = one-hot-encoding(col)` **and** `col1, col2, cols3 = one-hot-encoding(col)` are both correct.

##### Pattern semantics:

+ int/float/str/bool/category/datetime64: convert types
+ str_transform/num_transform: **unspecified** transformation applied to strings/numbers
+ rearrange_row/rearrange_cols: rows/columns are shuffled, resulting in a different order 
+ merge: cardinality is **reduced** (e.g., 100 different values -> 5 different values)
+ one_hot_encoding: resulting columns are of **0/1 values**
+ encode: resulting columns are of **contiguous** integer values (e.g., [0, N])

### Final Guideline

Refer to the code/table to evaluate the patterns!

