```R
fixed <- fix_me |> mutate(province = case_when(province == 'Alberta' ~ 'AB', province == 'British Columbia' ~ 'BC', TRUE ~ province))
penguins_less_nas <- penguins |> drop_na(body_mass_g)
engine_summary <- planes |> group_by(engine) |> summarise(avg_seats = mean(seats, na.rm = TRUE),planes = n())

```



```R
avg_flights <- flights |> 
  filter(carrier %in% c('AA',...)) |> 
  mutate(speed = (distance * 1.609) / (air_time / 60)) |> 
  group_by(carrier) |> 
  summarize(
    avg_speed = round(mean(speed, na.rm = TRUE), 0),
    avg_distance_km = round(mean(distance * 1.609, na.rm = TRUE), 0)
  ) |> 
  mutate(carrier = case_when(carrier == 'AA' ~ 'American Airlines', ...)) |> arrange(avg_speed)
```

```R
#' @param df A dataframe
#' @param col Name of the column to search in
#' @return A tibble with syntactic column names
#' @examples
#' read_clean_from_vanopenportal("parks-washrooms")
variance_calculation <- function(x) {
  if (!is.numeric(x)) {stop("Input must be a numeric vector!")}
  x <- x[!is.na(x) & !is.nan(x)]
  if (length(x) < 2) {stop("Input must have at least two non-NA and non-NaN elements!")}
  variance <- sum((x - mean(x))^2) / (length(x) - 1)
  return(variance)
}

filter_str <- function(df, col, pattern) {
  if (!is.data.frame(df)) {stop('Input must be a dataframe')}
  col_name <- deparse(substitute(col))
  if (!col_name %in% names(df)) {stop('Invalid column name: ', col_name)}
  if (!is.character(pattern)) {stop('Pattern must be a string')}
  df |> filter(str_detect({{col}}, pattern))
}

replace_str <- function(df, col, pattern, replacement) {
  if (!is.data.frame(df)) {stop('Input must be a dataframe')}
  col_name <- deparse(substitute(col))
  if (!col_name %in% names(df)) {stop('Invalid column name: ', col_name)}
  if (!is.character(df[[col_name]])) {stop('Specified column must be a character vector')}
  if (!is.character(pattern) || !is.character(replacement)) {stop('pattern and replacement must be strings')}
  df |> mutate({{col}} := str_replace({{col}}, pattern, replacement))
}
```

```R
dogs <- data.frame(
  name = c('Teemo', 'Luna', 'Cooper', 'Atlas'),
  breed = c('Toy Poodle', 'Golden Retriever', 'Labrador', 'German Shepherd')
)

test_that('Ensure replace_str function works properly', {
  result <- replace_str(dogs, breed, 'Retriever', 'Ret.')
  expect_equal(result$breed, c('Toy Poodle', 'Golden Ret.', 'Labrador', 'German Shepherd'))
  expect_error(replace_str('not a dataframe', breed, 'Retriever', 'Ret.')) # Test Error - not dataframe
})
```

```R
# mutate + case_when
df |> mutate(province = case_when(province == 'Alberta' ~ 'AB', province == 'British Columbia' ~ 'BC', TRUE ~ province))
# drop_na
df |> drop_na(x:y)  |  df |> drop_na()
# group_by + summarise
df |> group_by(continent) |> summarise(mean_life_exp = mean(lifeExp))
df |> group_by(continent, year) |> summarise(mean_life_exp = mean(lifeExp))
# Ignoring NA in summary calculations
df |> group_by(species) |> summarise(max_bill_length = max(bill_length_mm, na.rm = TRUE))
# Grouped mutate
df |> group_by(country) |> mutate(life_exp_gain = lifeExp - first(lifeExp))
# map_*
map_dbl(df, median, na.rm = TRUE)
# factor to character
gap <- df |> mutate(country = as.character(country), continent = as.character(continent))
# Summarise multiple statistics
df |> summarise(mean_hp = mean(hp), mean_mpg = mean(mpg), sum_hp = sum(hp))
# custom function
mds_map <- function(x, fun) {
  out <- vector("double", ncol(x))
  for (i in seq_along(x)) {out[i] <- fun(x[[i]], na.rm = TRUE)}
  out}
mds_map(df, min) # 使用
```

