P8105 Homework 1
================
Jennifer Mizhquiri Barbecho
2021-09-29

# Problem 1

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

``` r
set.seed(10)

problem1_df = tibble(
  samp = rnorm(10),
  greater_than_0_vec_logical = (samp>0),
  vec_char = c("This" , "is" , "a" , "ten", "character" , "vector" , "for" , "this" ,  "problem" , "set"),
  vec_factor = factor(c("level_a" , "level_b" , "level_c" , "level_b" , "level_c" , "level_c" , "level_a" , "level_b" , "level_c" , "level_a"))
  )

problem1_df
```

    ## # A tibble: 10 x 4
    ##       samp greater_than_0_vec_logical vec_char  vec_factor
    ##      <dbl> <lgl>                      <chr>     <fct>     
    ##  1  0.0187 TRUE                       This      level_a   
    ##  2 -0.184  FALSE                      is        level_b   
    ##  3 -1.37   FALSE                      a         level_c   
    ##  4 -0.599  FALSE                      ten       level_b   
    ##  5  0.295  TRUE                       character level_c   
    ##  6  0.390  TRUE                       vector    level_c   
    ##  7 -1.21   FALSE                      for       level_a   
    ##  8 -0.364  FALSE                      this      level_b   
    ##  9 -1.63   FALSE                      problem   level_c   
    ## 10 -0.256  FALSE                      set       level_a

Above, **problem\_df** is printed in its entirety.

I inspect this data frame for the mean of each of the 4 variables.

``` r_mean
mean(problem1_df$samp) ## this returns a value

mean(problem1_df$greater_than_0_vec_logical) ## this returns a value

mean(problem1_df$vec_char) ## this returns NA as the character vector is not numeric or logical

mean(problem1_df$vec_factor) ## this returns NA as the factor vector is not numeric or logical
```

As means can only be calculated from numeric or logical vectors, results
are returned only for variables, *samp* and
*greater\_than\_0\_vec\_logical*. I can convert the other two variables
into a numeric vector.

``` r_numeric_conversion
mean(as.numeric(problem1_df$vec_char)) ## returns NAs introduced by coercion

mean(as.numeric(problem1_df$vec_factor)) ## returns a value
```

I am able to obtain a mean value for the factor vector but not for the
character vector. This makes sense as the *factor vector* is based on
levels, such that each can be ascribed a value; it should be noted that
each level has not been explicitly assigned an order so the value itself
may not yet be meaningful. Further, the *character vector* does not have
a value but strings of text, and we can expect that there would be no
numeric mean.

# Problem 2

I will now open a dataset called **penguins**.

``` r
data("penguins", package = "palmerpenguins")
library(tidyverse)

head(penguins)
```

    ## # A tibble: 6 x 8
    ##   species island bill_length_mm bill_depth_mm flipper_length_~ body_mass_g sex  
    ##   <fct>   <fct>           <dbl>         <dbl>            <int>       <int> <fct>
    ## 1 Adelie  Torge~           39.1          18.7              181        3750 male 
    ## 2 Adelie  Torge~           39.5          17.4              186        3800 fema~
    ## 3 Adelie  Torge~           40.3          18                195        3250 fema~
    ## 4 Adelie  Torge~           NA            NA                 NA          NA <NA> 
    ## 5 Adelie  Torge~           36.7          19.3              193        3450 fema~
    ## 6 Adelie  Torge~           39.3          20.6              190        3650 male 
    ## # ... with 1 more variable: year <int>

Above, an excerpt of **penguins** is displayed.

*About the data set*

This dataset provides biometric, physical location, and year data for
three sets of penguins across three different islands. There are 8
variables: species, island, bill\_length\_mm, bill\_depth\_mm,
flipper\_length\_mm, body\_mass\_g, sex, year. Further, the number of
columns in **penguins** is 8 and the number of rows is 344.

*Finding the mean and other summary statistics*

You can use a summary function like summary() to get summary statistics
of **penguins**. Executing a summary command would provide insight like
the mean and median of continuous variables like bill depth and bill
length or the frequency by sex or island.

You can also use the mean function to find that the the mean of the
flipper length variable is 200.9152047 mm.

*Visualizing the data*

The data in **penguins** also offers the opportunity to create a
scatterplot *(fig. 1)* of bill length and flipper length by species.

``` r
ggplot(penguins, aes(y = flipper_length_mm, x = bill_length_mm, color = species)) + geom_point()
```

![](template_files/figure-gfm/_scatter-1.png)<!-- -->

*fig 1.* *This scatterplot demonstrates that there is a weakly positive
linear relationship between bill length and flipper length, regardless
of penguin species. Generally, of the three species, the Adelie species
has shorter bills and flippers and the Gentoo flippers has longer bills
and flippers.*

``` r
ggsave("penguins_scatter.pdf")
```

A PDF of this scatterplot (**penguins\_scatter.pdf**) may also be
located in this project directory.

\`\`\`
