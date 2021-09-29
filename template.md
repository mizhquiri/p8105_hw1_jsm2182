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

I will now move

``` r
data("penguins", package = "palmerpenguins")
library(tidyverse)

view(penguins)
names(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

``` r
summary(penguins)
```

    ##       species          island    bill_length_mm  bill_depth_mm  
    ##  Adelie   :152   Biscoe   :168   Min.   :32.10   Min.   :13.10  
    ##  Chinstrap: 68   Dream    :124   1st Qu.:39.23   1st Qu.:15.60  
    ##  Gentoo   :124   Torgersen: 52   Median :44.45   Median :17.30  
    ##                                  Mean   :43.92   Mean   :17.15  
    ##                                  3rd Qu.:48.50   3rd Qu.:18.70  
    ##                                  Max.   :59.60   Max.   :21.50  
    ##                                  NA's   :2       NA's   :2      
    ##  flipper_length_mm  body_mass_g       sex           year     
    ##  Min.   :172.0     Min.   :2700   female:165   Min.   :2007  
    ##  1st Qu.:190.0     1st Qu.:3550   male  :168   1st Qu.:2007  
    ##  Median :197.0     Median :4050   NA's  : 11   Median :2008  
    ##  Mean   :200.9     Mean   :4202                Mean   :2008  
    ##  3rd Qu.:213.0     3rd Qu.:4750                3rd Qu.:2009  
    ##  Max.   :231.0     Max.   :6300                Max.   :2009  
    ##  NA's   :2         NA's   :2

``` r
nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8

``` r
pull(penguins)
```

    ##   [1] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ##  [16] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ##  [31] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ##  [46] 2007 2007 2007 2007 2007 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ##  [61] 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ##  [76] 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ##  [91] 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2009 2009 2009 2009 2009
    ## [106] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [121] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [136] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [151] 2009 2009 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ## [166] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ## [181] 2007 2007 2007 2007 2007 2007 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ## [196] 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ## [211] 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ## [226] 2008 2008 2008 2008 2008 2008 2008 2009 2009 2009 2009 2009 2009 2009 2009
    ## [241] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [256] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [271] 2009 2009 2009 2009 2009 2009 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ## [286] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007
    ## [301] 2007 2007 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008 2008
    ## [316] 2008 2008 2008 2008 2008 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009
    ## [331] 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 2009

``` r
penguins$flipper_length_mm
```

    ##   [1] 181 186 195  NA 193 190 181 195 193 190 186 180 182 191 198 185 195 197
    ##  [19] 184 194 174 180 189 185 180 187 183 187 172 180 178 178 188 184 195 196
    ##  [37] 190 180 181 184 182 195 186 196 185 190 182 179 190 191 186 188 190 200
    ##  [55] 187 191 186 193 181 194 185 195 185 192 184 192 195 188 190 198 190 190
    ##  [73] 196 197 190 195 191 184 187 195 189 196 187 193 191 194 190 189 189 190
    ##  [91] 202 205 185 186 187 208 190 196 178 192 192 203 183 190 193 184 199 190
    ## [109] 181 197 198 191 193 197 191 196 188 199 189 189 187 198 176 202 186 199
    ## [127] 191 195 191 210 190 197 193 199 187 190 191 200 185 193 193 187 188 190
    ## [145] 192 185 190 184 195 193 187 201 211 230 210 218 215 210 211 219 209 215
    ## [163] 214 216 214 213 210 217 210 221 209 222 218 215 213 215 215 215 216 215
    ## [181] 210 220 222 209 207 230 220 220 213 219 208 208 208 225 210 216 222 217
    ## [199] 210 225 213 215 210 220 210 225 217 220 208 220 208 224 208 221 214 231
    ## [217] 219 230 214 229 220 223 216 221 221 217 216 230 209 220 215 223 212 221
    ## [235] 212 224 212 228 218 218 212 230 218 228 212 224 214 226 216 222 203 225
    ## [253] 219 228 215 228 216 215 210 219 208 209 216 229 213 230 217 230 217 222
    ## [271] 214  NA 215 222 212 213 192 196 193 188 197 198 178 197 195 198 193 194
    ## [289] 185 201 190 201 197 181 190 195 181 191 187 193 195 197 200 200 191 205
    ## [307] 187 201 187 203 195 199 195 210 192 205 210 187 196 196 196 201 190 212
    ## [325] 187 198 199 201 193 203 187 197 191 203 202 194 206 189 195 207 202 193
    ## [343] 210 198

``` r
class(penguins$flipper_length_mm)
```

    ## [1] "integer"

``` r
mean(penguins$flipper_length_mm, na.rm = TRUE)
```

    ## [1] 200.9152
