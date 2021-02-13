Lab 02 - Plastic waste
================
Vanessa Gill
02/08/2021

## Load packages and data

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read_csv("data/plastic-waste.csv")
```

## Exercises

### Exercise 1

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_bin).

![](lab-02_files/figure-gfm/plastic-waste-all-continent-1.png)<!-- -->

``` r
plastic_waste %>%
  filter(plastic_waste_per_cap > 3.5)
```

    ## # A tibble: 1 x 10
    ##   code  entity continent  year gdp_per_cap plastic_waste_p… mismanaged_plas…
    ##   <chr> <chr>  <chr>     <dbl>       <dbl>            <dbl>            <dbl>
    ## 1 TTO   Trini… North Am…  2010      31261.              3.6             0.19
    ## # … with 3 more variables: mismanaged_plastic_waste <dbl>, coastal_pop <dbl>,
    ## #   total_pop <dbl>

I hadn’t given it much thought but I didn’t know plastic waste was so
high in Trinidad and Tobago. Maybe it’s because their islands which
makes waste management more difficult.

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.02) +
  facet_wrap (~ continent, ncol = 2) +
  theme(legend.position = "none")
```

    ## Warning: Removed 51 rows containing non-finite values (stat_bin).

![](lab-02_files/figure-gfm/plastic-waste-by-continent-1.png)<!-- -->

It looks like they all have a similar range to each other.

### Exercise 2

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/plastic-waste-density-1.png)<!-- -->

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap, 
                     color = continent)) +
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap, 
                     color = continent, 
                     fill = continent)) +
  geom_density(alpha = 0.1)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

I think we defined color and fill of the curves by mapping aesthetics
because but alpha as a characteristic because the alpha affects
everything as a whole but the color and fill are specific to given chart
elements.

### Exercise 3

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = continent, 
                     y = plastic_waste_per_cap)) +
  geom_boxplot()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_boxplot).

![](lab-02_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Exercise 4

Remove this text, and add your answer for Exercise 4 here.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = continent, 
                     y = plastic_waste_per_cap)) +
  geom_violin()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_ydensity).

![](lab-02_files/figure-gfm/plastic-waste-violin-1.png)<!-- -->

The violin plot makes the shape of the distribution more apparent.

### Exercise 5

Remove this text, and add your answer for Exercise 5 here.

``` r
ggplot(data = plastic_waste,
       mapping = aes(x = mismanaged_plastic_waste_per_cap, y = plastic_waste_per_cap)) +
       geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-1.png)<!-- -->

I think this is a weak linear relationship. With more plastic waste,
there is more mismanaged plastic waste for the most part.

### Exercise 6

``` r
ggplot(data = plastic_waste,
       mapping = aes(x = mismanaged_plastic_waste_per_cap, y = plastic_waste_per_cap, color = continent)) +
       geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-continent-1.png)<!-- -->

In Europe, it appears that there’s a strong relationship whereby the
more plastic waste per capita, the more mismanaged plastic waste there
is. Other continents seem to have relationships that are less steep but
are similar in that more waste is related to more mismanaged waste.

### Exercise 7

Remove this text, and add your answer for Exercise 7 here.

``` r
ggplot(data = plastic_waste,
       mapping = aes(x = total_pop, y = plastic_waste_per_cap, color = continent)) +
       geom_point()
```

    ## Warning: Removed 61 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-total-1.png)<!-- -->

``` r
ggplot(data = plastic_waste,
       mapping = aes(x = coastal_pop, y = plastic_waste_per_cap, color = continent)) +
       geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-coastal-1.png)<!-- -->

It appears the coastal population data has a stronger linear
relationship

### Exercise 8

``` r
ggplot(data = plastic_waste,
       mapping = aes(x = coastal_pop/total_pop, y = plastic_waste_per_cap)) +
       geom_point(aes(color = continent)) +
  geom_smooth() + 
  ylim(0,0.75)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 62 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/recreate-viz-1.png)<!-- -->
