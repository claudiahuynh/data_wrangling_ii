Reading data from the web
================
My An Huynh
2024-10-10

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"
drug_use_html = read_html(url)
```

Get the pieces I actually need

``` r
marj_use_df =
  drug_use_html |> 
  html_table() |> 
  first() |> 
  slice(-1)
```

Practice Title was imported as first row in the data.

``` r
url = "https://www.bestplaces.net/cost_of_living/city/new_york/new_york"
cost_living = read_html(url)

cost_living |> 
  html_table(header = TRUE)
```

    ## [[1]]
    ## # A tibble: 8 × 4
    ##   Categories       `New York` `New York` `United States`
    ##   <chr>            <chr>      <chr>      <chr>          
    ## 1 Overall          172.5      121.5      100.0          
    ## 2 Grocery          116.6      103.8      100            
    ## 3 Health           127.6      120.7      100.0          
    ## 4 Housing          224.3      127.9      100.0          
    ## 5 Median Home Cost $677,200   $413,600   $338,100       
    ## 6 Utilities        150.5%     115.9%     100.0%         
    ## 7 Transportation   181.1      140.7      100.0          
    ## 8 Miscellaneous    136.4      121.8      100.0

## CSS selectors

``` r
swm_html = 
  read_html("https://www.imdb.com/list/ls070150896/")
```

``` r
swm_title_vec = 
  swm_html |> 
    html_elements(".ipc-title-link-wrapper .ipc-title__text") |> 
    html_text()

swm_runtime_vec =
swm_html |> 
  html_elements(".dli-title-metadata-item:nth-child(2)") |> 
  html_text()

swm_score_vec =
swm_html |> 
  html_elements(".ipc-rating-star--rating") |> 
  html_text()

swm_df = 
  tibble(
    title = swm_title_vec,
    runtime = swm_runtime_vec,
    score = swm_score_vec
  )
```

Import some books

``` r
books_html = read_html("https://books.toscrape.com") 

books_title = 
  books_html |> 
  html_elements("h3") |> 
  html_text()

books_price =
  books_html |> 
  html_elements(".price_color") |> 
  html_text()

books_df = 
  tibble(
    title = books_title,
    price = books_price
  )
```

## Use API

Get water data

``` r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") |> 
  content()
```

    ## Rows: 45 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Get brfss data Use query to specify how many rows you want to import
(depending on instructions)

``` r
brfss_df = 
  GET("https://chronicdata.cdc.gov/resource/acme-vg9e.csv",
      query = list("$limit" = 5000)) |> 
  content()
```

    ## Rows: 5000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Get pokemon data

``` r
pokemon_df =
  GET("https://pokeapi.co/api/v2/pokemon/ditto") |> 
  content()
```
