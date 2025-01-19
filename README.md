# Uncommon R Data Wrangling Tips
List of uncommon R data wrangling tips

## Contents
- [1 Filter nested list](#1-Filter-nested-list)
- [2 Replicate dataframe rows based on frequency](#2-Replicate-dataframe-rows-based-on-frequency)


## 1 Filter nested list
To filter a nested "list" object by maintaining a list of selected characters, create a custom function script as below. Important note: this custom function mantains rows with empty element

```
# Define the custom function
filter_nested_list <- function(nested_list, chars_to_filter) {
  lapply(nested_list, function(sublist) {
    intersect(sublist, chars_to_filter)
  })
}

# Sample data
nested_data <- list(
  c("a", "b", "c"),
  c("d", "e", "f"),
  c("g", "h", "i"),
  c("j", "k", "l"),
  c()
)

# List of characters to filter
selected_characters <- c("a", "e", "i", "k")

filtered_data <- filter_nested_list(nested_data, selected_characters)

# Print the original and filtered nested data
print("Original nested list:")
print(nested_data)
print("Filtered nested list:")
print(filtered_data)

```

If you intend to remove rows with empty element in the output filtered nested list, you may include the following script:
```
filtered_data2 <- filtered_data[lengths(filtered_data) > 0]
print("Filtered nested list without empty element:")
print(filtered_data2)
```

## 2 Replicate dataframe rows based on frequency
This is to replicate rows in a data frame based on a specified frequency. 
You may add an identifier column to the replicated data if needed.

```
# Sample data
df <- data.frame(
  Initial_id = 1:5,
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

# Reorder columns to place Id as the first column
df_replicated <- df_replicated[, c("Id", setdiff(colnames(df_replicated), "Id"))]

# Print the replicated dataframe with Id column
print(df_replicated)
```

