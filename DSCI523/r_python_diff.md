**Spot the difference between R and Python**

This is a collaborative study sheet for UBC MDS students learning both R and Python at the same time 🫠

All are welcome to contribute, and all contributions will be attributed. If you contribute, please add your name to the Contributors section at the end of the document.

| R | Python | Description of difference |
| :---- | :---- | :---- |
| `1` | `0` | The number in which the programming language starts counting from (in particular for things like numerical indexing or iteration) |
| `length()` | `len()` | Function to get the length of an object (most useful for objects that can contain \> 1 elements). |
| `delim` | `sep or delimiter` | Function argument name used to set delimiter when reading in data with atypical delimiter. |
| `my_list[-1]` | `my_list[-1]` | R removes the first element of the list or vector and returns the rest of the elements while Python returns the last element. |
| `arrange() df$colname <- sort(df$colname)` | `.sort_values()` | Functions used to sort dataframe/tibble according to column values. |
| `[[` | `[` | Used for subsetting and returns an object with a layer of structure removed (R this is in general, Python this is mostly for data frames, or if you subset one item from a list or tuple). If applied to a data frame, you get back the column as a vector (in R) or a series (in Python) |
| `[` | `[[` | Used for subsetting and returns an object of the same type. However in Python this is only true for data frames. |
| `typeof()` | `type()` | Function to determine the type of an object. |
|  |  |  |

**Contributors**

Tiffany Timbers, Paramveer Singh, Muhammad Mujtaba Khan, Tianhao Cao