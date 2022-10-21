Data Visualization with ggplot
================

loading tidyverse

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.5 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.3      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

Creates an empty graph

``` r
ggplot(data = mpg)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

geom_point() adds a layer of points to your plot aes() specify variables
to map to x and y-axes

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

number of rows and columns

``` r
nrow(mtcars)
```

    ## [1] 32

``` r
ncol(mtcars)
```

    ## [1] 11

documentation

``` r
?mpg
```

    ## starting httpd help server ... done

a scatterplot of hwy versus cyl

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = cyl, y = hwy))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

scatterplot of class versus drv

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = class, y = drv))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

Scaling: Assigning unique level of aesthetic to each unique value of the
variable.

Aesthetic color

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

Aesthetic size

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

    ## Warning: Using size for a discrete variable is not advised.

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

Aesthetic aplha (for transparency)

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

Aesthetic shape

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

Manually setting aesthetic properties

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), color = "purple")
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

Mapping a continuous variable to color and size. Continuous variables
cannot be mapped to shape

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, color = year))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, size = year))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, color = hwy, size = displ))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Mapping multiple aesthetics to same variable

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, color = class, size = class, shape = class))
```

    ## Warning: Using size for a discrete variable is not advised.

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

Stroke aesthetic

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), shape = 21, color = "purple", fill = "yellow", size = 4, stroke = 2)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

Conditional operation

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

Facet_wrap(): variable passed should be discrete

will only produce plots for the combinations of variables that have
values

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_wrap(~ class, nrow = 2)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

facet_grid() will produce a grid of plots for each combination of
variables that you specify, even if some plots are empty.

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ cyl)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

Facet on a continuous variable plot contains a facet for each distinct
value

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_wrap(~ cty)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(~ cty)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->
drv \~ . facet by values of drv on the y-axis.

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

. \~ cyl will facet by values of cyl on the x-axis

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

Geometrical Object A geom is the geometrical object that a plot uses to
represent data.

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

geom_smooth()

``` r
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

linetype in geom_smooth()

geom_smooth() separates the cars into three lines based on their drv
value

``` r
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

group aesthetic

``` r
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
ggplot(data = mpg) +
  geom_smooth(
    mapping = aes(x = displ, y = hwy, color = drv),
    show.legend = FALSE
  )
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

Add multiple geom functions

``` r
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

More efficient way

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point() +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(mapping = aes(color = class)) +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

filter

se: Computes standard error of the mean.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(mapping = aes(color = class)) +
  geom_smooth(
    data = filter(mpg, class == 'subcompact'),
    se = FALSE
  )
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

Recreating graphs from exercise

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(size = 3) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(size = 3) +
  geom_smooth(mapping = aes(group = drv), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) +
  geom_point(size = 3) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(mapping = aes(color = drv), size = 3) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(mapping = aes(color = drv), size = 3) +
  geom_smooth(mapping = aes(linetype = drv), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(size = 3, color = 'white') +
  geom_point(mapping = aes(color = drv))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

Statistical Transformations

The algorithm used to calculate new values for a graph is called a stat.
default value for stat is “count”

geom_bar()

``` r
ggplot(dat = diamonds) +
  geom_bar(mapping = aes(x = cut))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->

This works because every geom has a default stat, and every stat has a
default geom.

``` r
ggplot(dat = diamonds) +
  stat_count(mapping = aes(x = cut))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

identity

``` r
demo <- tribble(
  ~a,      ~b,
  "A", 20,
  "B", 35,
  "C", 15
)

ggplot(dat = demo) +
  geom_bar(mapping = aes(x = a, y = b), stat = 'identity')
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->

Bar chart of proportion

``` r
ggplot(data = diamonds) +
  geom_bar(
    mapping = aes(x = cut, y = ..prop.., group = 1)
  )
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

stat_summary()

``` r
ggplot(data = diamonds) +
  stat_summary(
    mapping = aes(x = cut, y = depth),
    fun.min = min,
    fun.max = max,
    fun = median
  )
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

``` r
?stat_summary
```

``` r
ggplot(data = diamonds) +
  geom_pointrange(
    mapping = aes(x = cut, y = depth),
    stat = 'summary',
    fun.min = min,
    fun.max = max,
    fun = median
  )
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

If group = 1 is not included, all the bars will have the same height.

The function geom_bar() assumes that the groups are equal to the x
values since the stat computes the counts within the group.

``` r
ggplot(data = diamonds) +
  geom_bar(mapping = aes(x = cut, y = ..prop..))
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

``` r
ggplot(data = diamonds) +
  geom_bar(
    mapping = aes(x = cut, fill = color, y = ..count.. / sum(..count..))
  )
```

![](DataVisualizationWith-ggplot-_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->
