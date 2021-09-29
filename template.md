P8105 Homework 1
================
Jennifer Mizhquiri Barbecho
2021-09-29

# Problem 1.A

Below I create a data frame called **problem1\_df** comprised of the
following:

-   a random sample of size 10 from a standard Normal distribution
-   a logical vector indicating whether elements of the sample are
    greater than 0
-   a character vector of length 10
-   a factor vector of length 10, with 3 different factor “levels”

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
problem1_df = tibble(
  samp = rnorm(10),
  greater_than_0_logical = (samp>0),
  vec_char = c("This" , "is" , "a" , "ten", "character" , "vector" , "for" , "this" ,  "problem" , "set"),
  vec_factor = factor(c("level_a" , "level_b" , "level_c" , "level_b" , "level_c" , "level_c" , "level_a" , "level_b" , "level_c" , "level_a"))
  )

problem1_df
```

    ## # A tibble: 10 x 4
    ##      samp greater_than_0_logical vec_char  vec_factor
    ##     <dbl> <lgl>                  <chr>     <fct>     
    ##  1  0.228 TRUE                   This      level_a   
    ##  2  0.900 TRUE                   is        level_b   
    ##  3 -2.23  FALSE                  a         level_c   
    ##  4 -0.523 FALSE                  ten       level_b   
    ##  5  0.503 TRUE                   character level_c   
    ##  6  2.06  TRUE                   vector    level_c   
    ##  7 -1.06  FALSE                  for       level_a   
    ##  8 -0.352 FALSE                  this      level_b   
    ##  9  0.935 TRUE                   problem   level_c   
    ## 10  0.598 TRUE                   set       level_a

\#Problem 2

``` r
data("penguins", package = "palmerpenguins")
```
