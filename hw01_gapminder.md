Gapminder Exploration
================

Get the Gapminder data
----------------------

Work with some of the data from the [Gapminder project](http://www.gapminder.org). Since the package is already installed, we just need to load it, also load the package that are useful for analyzing the data.

``` r
library(gapminder)
library(tidyverse)
```

    ## Loading tidyverse: ggplot2
    ## Loading tidyverse: tibble
    ## Loading tidyverse: tidyr
    ## Loading tidyverse: readr
    ## Loading tidyverse: purrr
    ## Loading tidyverse: dplyr

    ## Conflicts with tidy packages ----------------------------------------------

    ## filter(): dplyr, stats
    ## lag():    dplyr, stats

``` r
library(ggplot2)
```

Have a look at the data:

``` r
glimpse(gapminder)
```

    ## Observations: 1,704
    ## Variables: 6
    ## $ country   <fctr> Afghanistan, Afghanistan, Afghanistan, Afghanistan,...
    ## $ continent <fctr> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asi...
    ## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992...
    ## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.8...
    ## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 1488...
    ## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 78...

``` r
dim(gapminder)
```

    ## [1] 1704    6

Explore the variable *"pop"*

``` r
min(gapminder$pop)
```

    ## [1] 60011

``` r
max(gapminder$pop)
```

    ## [1] 1318683096

``` r
ggplot(gapminder, aes(y = pop)) + geom_boxplot(aes(x = factor(1))) +  facet_wrap(~continent, scales = "free")
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-3-1.png)

Because gapminder has too much info, in my work, I just extract the data that belong to the continent of Asia, and variables *"country"*, *"year"*, and *"pop"*.

``` r
gDat <- gapminder[gapminder$continent == "Asia", c("country", "year", "pop")]
str(gDat)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    396 obs. of  3 variables:
    ##  $ country: Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ year   : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ pop    : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...

Plot annual population for different countries in Asia

``` r
ggplot(gDat, aes(x = year, y = pop)) + geom_point(aes(color = country)) 
```

![](hw01_gapminder_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-5-1.png)
