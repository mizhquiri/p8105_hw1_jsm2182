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

<!-- -->

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
set.seed(10)

problem1_df = tibble(
  samp = rnorm(10),
  greater_than_0_logical = (samp>0),
  vec_char = c("This" , "is" , "a" , "ten", "character" , "vector" , "for" , "this" ,  "problem" , "set"),
  vec_factor = factor(c("level_a" , "level_b" , "level_c" , "level_b" , "level_c" , "level_c" , "level_a" , "level_b" , "level_c" , "level_a"))
  )

problem1_df
```

    ## # A tibble: 10 x 4
    ##       samp greater_than_0_logical vec_char  vec_factor
    ##      <dbl> <lgl>                  <chr>     <fct>     
    ##  1  0.0187 TRUE                   This      level_a   
    ##  2 -0.184  FALSE                  is        level_b   
    ##  3 -1.37   FALSE                  a         level_c   
    ##  4 -0.599  FALSE                  ten       level_b   
    ##  5  0.295  TRUE                   character level_c   
    ##  6  0.390  TRUE                   vector    level_c   
    ##  7 -1.21   FALSE                  for       level_a   
    ##  8 -0.364  FALSE                  this      level_b   
    ##  9 -1.63   FALSE                  problem   level_c   
    ## 10 -0.256  FALSE                  set       level_a

I inspect the data for the mean of each of the 4 variables

``` r_mean
mean(problem1_df$samp)#this returns a value

mean(problem1_df$greater_than_0_logical)#this returns a value

mean(problem1_df$vec_char)#this returns NA as the character vector is not numeric or logical

mean(problem1_df$vec_factor)#this returns NA as the factor vector is not numeric or logical
```

As means can only be calculated from numeric or logical vectors, results
are returned only for variables, *samp* and *greater\_than\_0\_logical*.
I can convert the other two variables into a numeric vector.

``` r_numeric_conversion
mean(as.numeric(problem1_df$vec_char))#returns NAs introduced by coercion

mean(as.numeric(problem1_df$vec_factor))#returns a value
```

I am able to obtain a mean value for the factor vector but not for the
character vector. This makes sense as the *factor vector* is based on
levels, such that each can be ascribed a value; it should be noted that
each level has not been assigned an order so the value itself may not
yet be meaningful. Further, the *character vector* does not have a value
but strings of text, and it makes sense that it would not have a numeric
mean.

# Problem 2

I will now open a dataset called **penguins**.

``` r
data("penguins", package = "palmerpenguins")
library(tidyverse)
```

I then looked through **penguins** to find the variable names and
summary statistics.

``` r_penguins_summary
data("penguins", package = "palmerpenguins")
library(tidyverse)
view(penguins)
names(penguins)
summary(penguins) #this provides summary statistics.
165/(165 + 168 + 11)#this will allow for the percent breakdown of females
```

In **penguins** there are 8 variables: species, island,
bill\_length\_mm, bill\_depth\_mm, flipper\_length\_mm, body\_mass\_g,
sex and year. This dataset provides biometric, physical location, and
time data for three sets of penguins across three different islands. In
species, for example, the most common species is Adelie followed by
Gentoo. About 47% are female (not including 11 missing values).

``` r_penguins_colxrow
data("penguins", package = "palmerpenguins")
library(tidyverse)
ncol(penguins)
nrow(penguins)
```

The number of columns in **penguins** is 8 and the number of rows is
344.

``` r_penguins_flipper_mean
pull(penguins)

penguins$flipper_length_mm

mean(penguins$flipper_length_mm, na.rm = TRUE)
```

The mean flipper length in **penguins** is 200.9152047.

I will now create a scatterplot *(fig. 1)* by of bill length and flipper
length by species.

``` r
ggplot(penguins, aes(y = flipper_length_mm, x = bill_length_mm, color = species)) + geom_point()
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](template_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

*fig 1.* *This scatterplot demonstrates that there is a weakly linear
relationship between bill length and flipper length, regardless of
penguin species. Overall, the Adelie species has shorter bills and
flippers and the Gentoo flippers has longer bills and flippers.*

``` r
ggsave("penguins_scatter.pdf")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values (geom_point).

You may find this scatterplot saved as a PDF in the R project under
**penguins\_scatter.pdf**.

\`\`\`
