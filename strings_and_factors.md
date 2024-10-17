Reading data from the web
================
My An Huynh
2024-10-10

String matching needs to be the exact match.

``` r
string_vec = c("My", "name", "is", "Claudia")

str_detect(string_vec, "a")
```

    ## [1] FALSE  TRUE FALSE  TRUE

``` r
str_replace(string_vec, "Claudia", "claudia")
```

    ## [1] "My"      "name"    "is"      "claudia"

``` r
str_replace(string_vec, "e", "E")
```

    ## [1] "My"      "namE"    "is"      "Claudia"

Use ^ to denote the beginning of the string and \$ to denote the end of
the string.

``` r
string_vec = c(
  "i think we all rule for participating",
  "i think i have been caught",
  "i think this will be quite fun actually",
  "it will be fun, i think"
  )

str_detect(string_vec, "^i think")
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
str_detect(string_vec, "i think$")
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
string_vec = c(
  "Time for a Pumpkin Spice Latte!",
  "went to the #pumpkinpatch last weekend",
  "Pumpkin Pie is obviously the best pie",
  "SMASHING PUMPKINS -- LIVE IN CONCERT!!"
  )

str_detect(string_vec, "pumpkin")
```

    ## [1] FALSE  TRUE FALSE FALSE

``` r
str_detect(string_vec,"[Pp]umpkin")
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
string_vec = c(
  '7th inning stretch',
  '1st half soon to begin. Texas won the toss.',
  'she is 5 feet 4 inches tall',
  '3AM - cant sleep :('
  )

str_detect(string_vec, "[0-9][a-zA-Z]")
```

    ## [1]  TRUE  TRUE FALSE  TRUE

## Factors

``` r
sex_vec = factor(c("male", "male", "female", "female"))
as.numeric(sex_vec)
```

    ## [1] 2 2 1 1

``` r
sex_vec = fct_relevel(sex_vec, "male")
```
