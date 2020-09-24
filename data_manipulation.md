data\_manipulation
================

This section is to clean and organize data\!

``` r
library(tidyverse)
```

    ## -- Attaching packages --------

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts -----------------
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
options(tibble.print_min = 3)
litters_data = read_csv("./data/FAS_litters.csv", col_types = "ccddiiii")
litters_data = janitor::clean_names(litters_data)

pups_data = read_csv("./data/FAS_pups.csv",
  col_types = "ciiiii")
pups_data = janitor::clean_names(pups_data)
```

Select.

``` r
select(litters_data, group, litter_number, gd0_weight, pups_born_alive)
```

    ## # A tibble: 49 x 4
    ##   group litter_number gd0_weight pups_born_alive
    ##   <chr> <chr>              <dbl>           <int>
    ## 1 Con7  #85                 19.7               3
    ## 2 Con7  #1/2/95/2           27                 8
    ## 3 Con7  #5/5/3/83/3-3       26                 6
    ## # ... with 46 more rows

``` r
select(litters_data, group:gd_of_birth)
```

    ## # A tibble: 49 x 5
    ##   group litter_number gd0_weight gd18_weight gd_of_birth
    ##   <chr> <chr>              <dbl>       <dbl>       <int>
    ## 1 Con7  #85                 19.7        34.7          20
    ## 2 Con7  #1/2/95/2           27          42            19
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19
    ## # ... with 46 more rows

``` r
select(litters_data, -pups_survive)
```

    ## # A tibble: 49 x 7
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 46 more rows, and 1 more variable: pups_dead_birth <int>

Renaming

``` r
select(litters_data, GROUP = group, LiTtEr_NuMbEr = litter_number)
```

    ## # A tibble: 49 x 2
    ##   GROUP LiTtEr_NuMbEr
    ##   <chr> <chr>        
    ## 1 Con7  #85          
    ## 2 Con7  #1/2/95/2    
    ## 3 Con7  #5/5/3/83/3-3
    ## # ... with 46 more rows

``` r
rename(litters_data, GROUP = group, LiTtEr_NuMbEr = litter_number)
```

    ## # A tibble: 49 x 8
    ##   GROUP LiTtEr_NuMbEr gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
select(litters_data, starts_with("gd"))
```

    ## # A tibble: 49 x 3
    ##   gd0_weight gd18_weight gd_of_birth
    ##        <dbl>       <dbl>       <int>
    ## 1       19.7        34.7          20
    ## 2       27          42            19
    ## 3       26          41.4          19
    ## # ... with 46 more rows

``` r
select(litters_data, litter_number, pups_survive, everything())
```

    ## # A tibble: 49 x 8
    ##   litter_number pups_survive group gd0_weight gd18_weight gd_of_birth
    ##   <chr>                <int> <chr>      <dbl>       <dbl>       <int>
    ## 1 #85                      3 Con7        19.7        34.7          20
    ## 2 #1/2/95/2                7 Con7        27          42            19
    ## 3 #5/5/3/83/3-3            5 Con7        26          41.4          19
    ## # ... with 46 more rows, and 2 more variables: pups_born_alive <int>,
    ## #   pups_dead_birth <int>

``` r
relocate(litters_data, litter_number, pups_survive)
```

    ## # A tibble: 49 x 8
    ##   litter_number pups_survive group gd0_weight gd18_weight gd_of_birth
    ##   <chr>                <int> <chr>      <dbl>       <dbl>       <int>
    ## 1 #85                      3 Con7        19.7        34.7          20
    ## 2 #1/2/95/2                7 Con7        27          42            19
    ## 3 #5/5/3/83/3-3            5 Con7        26          41.4          19
    ## # ... with 46 more rows, and 2 more variables: pups_born_alive <int>,
    ## #   pups_dead_birth <int>

Pups data.

``` r
select(pups_data,litter_number, sex, pd_ears)
```

    ## # A tibble: 313 x 3
    ##   litter_number   sex pd_ears
    ##   <chr>         <int>   <int>
    ## 1 #85               1       4
    ## 2 #85               1       4
    ## 3 #1/2/95/2         1       5
    ## # ... with 310 more rows

Filter

``` r
filter(litters_data,gd_of_birth == 20)
```

    ## # A tibble: 32 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 3 Con7  #2/2/95/3-2         NA          NA            20               6
    ## # ... with 29 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data, pups_born_alive >= 2)
```

    ## # A tibble: 49 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data, pups_survive != 4)
```

    ## # A tibble: 44 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 41 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data, !(pups_survive == 4))
```

    ## # A tibble: 44 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 41 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data,group %in% c("Con7", "Con8"))
```

    ## # A tibble: 15 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
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
    ## 11 Con8  #5/4/3/83/3         28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-~       NA          NA            20               8
    ## 14 Con8  #2/2/95/2           NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # ... with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, group == "Con7" & gd_of_birth == 20)
```

    ## # A tibble: 4 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 3 Con7  #2/2/95/3-2         NA          NA            20               6
    ## 4 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ## # ... with 2 more variables: pups_dead_birth <int>, pups_survive <int>

Filter Pups data.

``` r
filter(pups_data, sex == 1)
```

    ## # A tibble: 155 x 6
    ##   litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##   <chr>         <int>   <int>   <int>    <int>   <int>
    ## 1 #85               1       4      13        7      11
    ## 2 #85               1       4      13        7      12
    ## 3 #1/2/95/2         1       5      13        7       9
    ## # ... with 152 more rows

``` r
filter(pups_data, pd_walk < 11 & sex == 2)
```

    ## # A tibble: 127 x 6
    ##   litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##   <chr>         <int>   <int>   <int>    <int>   <int>
    ## 1 #1/2/95/2         2       4      13        7       9
    ## 2 #1/2/95/2         2       4      13        7      10
    ## 3 #1/2/95/2         2       5      13        8      10
    ## # ... with 124 more rows

``` r
drop_na(litters_data, gd_of_birth)
```

    ## # A tibble: 49 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

Mutate.

``` r
mutate(litters_data,
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower(group)
)
```

    ## # A tibble: 49 x 9
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 con7  #85                 19.7        34.7          20               3
    ## 2 con7  #1/2/95/2           27          42            19               8
    ## 3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 46 more rows, and 3 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>, wt_gain <dbl>

Mutate Pups data.

``` r
mutate(pups_data, substraction = pd_pivot - 7, sum = pd_ears + pd_eyes + pd_pivot + pd_walk)
```

    ## # A tibble: 313 x 8
    ##   litter_number   sex pd_ears pd_eyes pd_pivot pd_walk substraction   sum
    ##   <chr>         <int>   <int>   <int>    <int>   <int>        <dbl> <int>
    ## 1 #85               1       4      13        7      11            0    35
    ## 2 #85               1       4      13        7      12            0    36
    ## 3 #1/2/95/2         1       5      13        7       9            0    34
    ## # ... with 310 more rows

Arrange.

``` r
head(arrange(litters_data, group, pups_born_alive), 10)
```

    ## # A tibble: 10 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  5 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  6 Con7  #1/2/95/2           27          42            19               8
    ##  7 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ##  8 Con8  #2/2/95/2           NA          NA            19               5
    ##  9 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ## 10 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # ... with 2 more variables: pups_dead_birth <int>, pups_survive <int>

%\>%

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names() %>%
  select(-pups_survive) %>%
  mutate(
    wt_gain = gd18_weight - gd0_weight,
    group =  str_to_lower(group)) %>% 
  drop_na(wt_gain)
litters_data
```

    ## # A tibble: 31 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 con7  #85                 19.7        34.7          20               3
    ## 2 con7  #1/2/95/2           27          42            19               8
    ## 3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # ... with 28 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   wt_gain <dbl>

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names(dat = .) %>%
  select(.data = ., -pups_survive) %>%
  mutate(.data = .,
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)) %>% 
  drop_na(data = ., wt_gain)
```

``` r
litters_data %>%
  lm(wt_gain ~ pups_born_alive, data = .) %>%
  broom::tidy()
```

    ## # A tibble: 2 x 5
    ##   term            estimate std.error statistic  p.value
    ##   <chr>              <dbl>     <dbl>     <dbl>    <dbl>
    ## 1 (Intercept)       13.1       1.27      10.3  3.39e-11
    ## 2 pups_born_alive    0.605     0.173      3.49 1.55e- 3
