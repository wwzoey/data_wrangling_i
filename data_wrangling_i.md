data\_wrangling\_i
================

Practice on Data Import\!

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Path

``` r
getwd()
```

    ## [1] "C:/Users/WUWENZHAO/Desktop/DataScience/data_wrangling_i/data_wrangling_i"

Importing data tables.

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
pups_data = read_csv(file = "./data/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
names(litters_data)
```

    ## [1] "Group"             "Litter Number"     "GD0 weight"       
    ## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
    ## [7] "Pups dead @ birth" "Pups survive"

``` r
litters_data = janitor::clean_names(litters_data)
names(litters_data)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

``` r
names(pups_data)
```

    ## [1] "Litter Number" "Sex"           "PD ears"       "PD eyes"      
    ## [5] "PD pivot"      "PD walk"

``` r
pups_data = janitor::clean_names(pups_data)
names(pups_data)
```

    ## [1] "litter_number" "sex"           "pd_ears"       "pd_eyes"      
    ## [5] "pd_pivot"      "pd_walk"

``` r
litters_data
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
tail(litters_data, 5)
```

    ## # A tibble: 5 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Low8  #100                20          39.2          20               8
    ## 2 Low8  #4/84               21.8        35.2          20               4
    ## 3 Low8  #108                25.6        47.5          20               8
    ## 4 Low8  #99                 23.5        39            20               6
    ## 5 Low8  #110                25.5        42.7          20               7
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
skimr::skim(litters_data)
```

|                                                  |               |
| :----------------------------------------------- | :------------ |
| Name                                             | litters\_data |
| Number of rows                                   | 49            |
| Number of columns                                | 8             |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |               |
| Column type frequency:                           |               |
| character                                        | 2             |
| numeric                                          | 6             |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |               |
| Group variables                                  | None          |

Data summary

**Variable type: character**

| skim\_variable | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
| :------------- | ---------: | -------------: | --: | --: | ----: | --------: | ---------: |
| group          |          0 |              1 |   4 |   4 |     0 |         6 |          0 |
| litter\_number |          0 |              1 |   3 |  15 |     0 |        49 |          0 |

**Variable type: numeric**

| skim\_variable    | n\_missing | complete\_rate |  mean |   sd |   p0 |   p25 |   p50 |   p75 | p100 | hist  |
| :---------------- | ---------: | -------------: | ----: | ---: | ---: | ----: | ----: | ----: | ---: | :---- |
| gd0\_weight       |         15 |           0.69 | 24.38 | 3.28 | 17.0 | 22.30 | 24.10 | 26.67 | 33.4 | ▃▇▇▆▁ |
| gd18\_weight      |         17 |           0.65 | 41.52 | 4.05 | 33.4 | 38.88 | 42.25 | 43.80 | 52.7 | ▃▃▇▂▁ |
| gd\_of\_birth     |          0 |           1.00 | 19.65 | 0.48 | 19.0 | 19.00 | 20.00 | 20.00 | 20.0 | ▅▁▁▁▇ |
| pups\_born\_alive |          0 |           1.00 |  7.35 | 1.76 |  3.0 |  6.00 |  8.00 |  8.00 | 11.0 | ▁▃▂▇▁ |
| pups\_dead\_birth |          0 |           1.00 |  0.33 | 0.75 |  0.0 |  0.00 |  0.00 |  0.00 |  4.0 | ▇▂▁▁▁ |
| pups\_survive     |          0 |           1.00 |  6.41 | 2.05 |  1.0 |  5.00 |  7.00 |  8.00 |  9.0 | ▁▃▂▇▇ |

Arguments to read\_\*.

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv", skip = 10, col_names = FALSE)
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_character(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_double(),
    ##   X6 = col_double(),
    ##   X7 = col_double(),
    ##   X8 = col_double()
    ## )

``` r
head(litters_data)
```

    ## # A tibble: 6 x 8
    ##   X1    X2                 X3    X4    X5    X6    X7    X8
    ##   <chr> <chr>           <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 Con8  #3/5/2/2/95      28.5    NA    20     8     0     8
    ## 2 Con8  #5/4/3/83/3      28      NA    19     9     0     8
    ## 3 Con8  #1/6/2/2/95-2    NA      NA    20     7     0     6
    ## 4 Con8  #3/5/3/83/3-3-2  NA      NA    20     8     0     8
    ## 5 Con8  #2/2/95/2        NA      NA    19     5     0     4
    ## 6 Con8  #3/6/2/2/95-3    NA      NA    20     7     0     7

``` r
pups_data = read_csv(file = "./data/FAS_pups.csv", skip = 10, col_names = FALSE)
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_double(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_double(),
    ##   X6 = col_double()
    ## )

``` r
head(pups_data)
```

    ## # A tibble: 6 x 6
    ##   X1                 X2    X3    X4    X5    X6
    ##   <chr>           <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 #2/2/95/3-2         1     4    NA     8    10
    ## 2 #1/5/3/83/3-3/2     1     4    NA    NA     9
    ## 3 #1/5/3/83/3-3/2     1     4    NA     7     9
    ## 4 #1/5/3/83/3-3/2     1     4    NA     7     9
    ## 5 #1/5/3/83/3-3/2     1     4    NA     7     9
    ## 6 #1/5/3/83/3-3/2     1     4    NA     7     9

Parsing columns.

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv",
 col_types = cols(
   Group = col_character(), 
   `Litter Number` = col_character(),
   `GD0 weight` = col_double(),
   `GD18 weight` = col_double(),
   `GD of Birth` = col_integer(),
   `Pups born alive` = col_integer(),
   `Pups dead @ birth` = col_integer(),
   `Pups survive` = col_integer()
   ))
tail(litters_data)
```

    ## # A tibble: 6 x 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>                  <dbl>         <dbl>         <int>
    ## 1 Low8  #79                     25.4          43.8            19
    ## 2 Low8  #100                    20            39.2            20
    ## 3 Low8  #4/84                   21.8          35.2            20
    ## 4 Low8  #108                    25.6          47.5            20
    ## 5 Low8  #99                     23.5          39              20
    ## 6 Low8  #110                    25.5          42.7            20
    ## # ... with 3 more variables: `Pups born alive` <int>, `Pups dead @
    ## #   birth` <int>, `Pups survive` <int>

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv",
  col_types = "ccddiiii"
)
pups_data = read_csv(file = "./data/FAS_pups.csv",
 col_types = cols(
   `Litter Number` = col_character(),
   `Sex` = col_integer(),
   `PD ears` = col_integer(),
   `PD eyes` = col_integer(),
   `PD pivot` = col_integer(),
   `PD walk` = col_integer()
   ))
tail(pups_data)
```

    ## # A tibble: 6 x 6
    ##   `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##   <chr>           <int>     <int>     <int>      <int>     <int>
    ## 1 #2/95/2             2         4        12          7         9
    ## 2 #2/95/2             2         3        13          6         8
    ## 3 #2/95/2             2         3        13          7         9
    ## 4 #82/4               2         4        13          7         9
    ## 5 #82/4               2         3        13          7         9
    ## 6 #82/4               2         3        13          7         9

``` r
read_csv(file = "./data/FAS_pups.csv",
  col_types = "ciiiii")
```

    ## # A tibble: 313 x 6
    ##    `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##    <chr>           <int>     <int>     <int>      <int>     <int>
    ##  1 #85                 1         4        13          7        11
    ##  2 #85                 1         4        13          7        12
    ##  3 #1/2/95/2           1         5        13          7         9
    ##  4 #1/2/95/2           1         5        13          8        10
    ##  5 #5/5/3/83/3-3       1         5        13          8        10
    ##  6 #5/5/3/83/3-3       1         5        14          6         9
    ##  7 #5/4/2/95/2         1        NA        14          5         9
    ##  8 #4/2/95/3-3         1         4        13          6         8
    ##  9 #4/2/95/3-3         1         4        13          7         9
    ## 10 #2/2/95/3-2         1         4        NA          8        10
    ## # ... with 303 more rows

Other file formats.

``` r
library(readxl)
mlb11_data = read_excel("data/mlb11.xlsx", n_max = 20)
head(mlb11_data,5)
```

    ## # A tibble: 5 x 12
    ##   team   runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##   <chr> <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ## 1 Texa~   855    5659  1599      210   0.283        930          143    96
    ## 2 Bost~   875    5710  1600      203   0.28        1108          102    90
    ## 3 Detr~   787    5563  1540      169   0.277       1143           49    95
    ## 4 Kans~   730    5672  1560      129   0.275       1006          153    71
    ## 5 St. ~   762    5532  1513      162   0.273        978           57    90
    ## # ... with 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

``` r
library(haven)
pulse_data = read_sas("./data/public_pulse_data.sas7bdat")
head(pulse_data,5)
```

    ## # A tibble: 5 x 7
    ##      ID   age Sex   BDIScore_BL BDIScore_01m BDIScore_06m BDIScore_12m
    ##   <dbl> <dbl> <chr>       <dbl>        <dbl>        <dbl>        <dbl>
    ## 1 10003  48.0 male            7            1            2            0
    ## 2 10015  72.5 male            6           NA           NA           NA
    ## 3 10022  58.5 male           14            3            8           NA
    ## 4 10026  72.7 male           20            6           18           16
    ## 5 10035  60.4 male            4            0            1            2

Comparison with Base R

``` r
base_pups_data = read.csv(file = "./data/FAS_pups.csv")
base_pups_data = janitor::clean_names(base_pups_data)
names(base_pups_data)
```

    ## [1] "litter_number" "sex"           "pd_ears"       "pd_eyes"      
    ## [5] "pd_pivot"      "pd_walk"
