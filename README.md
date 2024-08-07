# Uncommon-R-Data-Wrangling-Tips
List of uncommon R data wrangling tips

## Contents
- [1 Filter nested list](#1-Filter-nested-list)


### 1 Filter nested list
To filter a nested "list" object by maintaining a list of selected characters, create a custom function script as below. Important note: this custom function mantains rows with empty element

```
filter_nested_list <- function(nested_list, chars_to_filter) {
  lapply(nested_list, function(sublist) {
    intersect(sublist, chars_to_filter)
  })
}
```

If you intend to remove rows with empty element in the output filtered nested list, you may include the following script:
```
filtered_list <- filtered_list[lengths(filtered_list) > 0]
```

### 2 Replicate dataframe rows based on a single column
This is to replicate rows in a data frame based on a specified frequency. 
You may add an identifier column to the replicated data if needed.

```
# Sample data
df <- data.frame(
  ID = 1:5,
  Name = c("A", "B", "C", "D", "E"),
  Value = c(10, 20, 30, 40, 50),
  Frequency = c(1, 3, 2, 4, 1)
)

# Print the original dataframe
print("Original Dataframe:")
print(df)

# Replicate rows based on the Frequency column
df_replicated <- df[rep(seq_len(nrow(df)), df$Frequency), ]

# Reset row names to maintain consistency
rownames(df_replicated) <- NULL

# Add Id column
df_replicated$Id <- seq_len(nrow(df_replicated))

# Print the replicated dataframe with Id column
print(df_replicated)
```

