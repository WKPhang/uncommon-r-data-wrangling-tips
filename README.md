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
