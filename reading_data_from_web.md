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
