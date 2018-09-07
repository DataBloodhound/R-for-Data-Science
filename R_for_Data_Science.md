---
title: "R_for_Data_Science"
author: "Alibek"
date: "September 6, 2018"
output:
    html_document:
        keep_md: true
---

# Chapter 1. Data Visualization with ggplot2.

## Introduction
The most effective way to grasp some insights from data is to visualize it. The most effective library to 
visualize data is ggplot2. "gg" stands for grammar of graphics. To use ggplot2 we need to initialize it.


```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
## ✔ tibble  1.4.2     ✔ dplyr   0.7.6
## ✔ tidyr   0.8.0     ✔ stringr 1.3.1
## ✔ readr   1.1.1     ✔ forcats 0.3.0
```

```
## ── Conflicts ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

This one line of code loads different packages to analyze and visualize data. There's some conflicts in 
function names of dplyr package and core R functions. To specify function from package we need to write 
package::function. For example: dplyr::filter().


## First Steps
Let's use ggplot2 package to answer a question: do cars with big engine use more fuel than cars with 
small engine? It is intuitive that they do, but let's prove it visually. In addition, we can find out 
if releationship between engine size and fuel efficiency is linear or nonlinear. We used preload data 
from ggplot2 - mpg. It is observations of 234 cars from US Environment Protection Agency. 


```r
df = ggplot2::mpg
head(df)
```

```
## # A tibble: 6 x 11
##   manufacturer model displ  year   cyl trans drv     cty   hwy fl    class
##   <chr>        <chr> <dbl> <int> <int> <chr> <chr> <int> <int> <chr> <chr>
## 1 audi         a4      1.8  1999     4 auto… f        18    29 p     comp…
## 2 audi         a4      1.8  1999     4 manu… f        21    29 p     comp…
## 3 audi         a4      2    2008     4 manu… f        20    31 p     comp…
## 4 audi         a4      2    2008     4 auto… f        21    30 p     comp…
## 5 audi         a4      2.8  1999     6 auto… f        16    26 p     comp…
## 6 audi         a4      2.8  1999     6 manu… f        18    26 p     comp…
```


## Creating a ggplot
The most effective way to show relationship between two variables is scatter plot. We use _displ_ as x axis
and _hwy_ as y axis.


```r
ggplot(df) +
    geom_point(mapping = aes(x = displ, y = hwy))
```

![](R_for_Data_Science_files/figure-html/scatter_plot-1.png)<!-- -->

The scatter plot shows negative relationship between fuel efficiency and engine size. Which means that 
cars with bigger engines consume more fuel. 
_ggplot()_ function creates empty graph, then with *geom_point()* function we add points layer to empty 
graph.

## Exercise
Make scatter plot _hwy_ vs. _cyl_.


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = hwy, y = cyl))
```

![](R_for_Data_Science_files/figure-html/scatter_plot_hwy_vs_cyl-1.png)<!-- -->

Make scatter plot _class_ vs. _drv_.


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = class, y =drv))
```

![](R_for_Data_Science_files/figure-html/scatter_plot_class_vs_drv-1.png)<!-- -->


## Aesthetic Mappings
_The greatest value of a picture is when it forces us to notice what we never expected to see. -John Tukey_

Aesthetic function maps data into axis, also it can describe size of points, shape of points and color of 
points. Below, we'll plot same scatter plot with different colors for class of cars.


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![](R_for_Data_Science_files/figure-html/scatter_plot_displ_hwy_color_class-1.png)<!-- -->

Besides colors of class, we can map also size of a points:


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

```
## Warning: Using size for a discrete variable is not advised.
```

![](R_for_Data_Science_files/figure-html/scatter_plot_displ_hwy_size_class-1.png)<!-- -->

There's warning that setting size of points to class is not good idea, since class variable is unordered 
categorical varaible. Transparency of points and shape of points can be mapped in aes function too.


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

![](R_for_Data_Science_files/figure-html/scatter_plot_shape_transparency-1.png)<!-- -->

```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

```
## Warning: The shape palette can deal with a maximum of 6 discrete values
## because more than 6 becomes difficult to discriminate; you have 7.
## Consider specifying shapes manually if you must have them.
```

```
## Warning: Removed 62 rows containing missing values (geom_point).
```

![](R_for_Data_Science_files/figure-html/scatter_plot_shape_transparency-2.png)<!-- -->

There's only 6 type of shapes, and we have 7 categories for a class variable, so suv points didn't assign 
to any shape points. We can set aesthetic properties, for example we can specify color of points:


```r
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy), color = 'blue')
```

![](R_for_Data_Science_files/figure-html/scatter_plot_blue-1.png)<!-- -->
































