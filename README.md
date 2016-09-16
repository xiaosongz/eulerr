
<!-- README.md is generated from README.Rmd. Please edit that file -->
eulerr
======

[![Travis-CI Build Status](https://travis-ci.org/jolars/eulerr.svg?branch=master)](https://travis-ci.org/jolars/eulerr) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/jolars/eulerr?branch=master&svg=true)](https://ci.appveyor.com/project/jolars/eulerr)

eulerr generates area-proportional euler diagrams that display set relationships (intersections, unions, and disjoints) using circles. [Euler diagrams](https://en.wikipedia.org/wiki/Euler_diagram) are Venn diagrams without the requirement that all set interactions be present (whether they are empty or not). Thus, depending on input, eulerr will sometimes produce Venn diagrams but other times not.

With three or more sets interacting, exact euler diagrams are frequently impossible. In these cases, eulerr will provide the best approximation possible by numerically tuning the circles positions and radiuses so that the sum of squared errors is minimized.

When solutions are approximate, eulerr helpfully provides statistics that allow the user decide if the approximation can be trusted.

Installation
------------

The development version can be installed by running

``` r
devtools::install_github("jolars/eulerr")
```

Usage
-----

``` r
library(eulerr)

sets <- c(A = 10, B = 9, C = 4, "A&B" = 2, "A&C" = 3, "B&C" = 3, "A&B&C" = 2)

fit <- eulerr(sets)
```

We look at the solution,

``` r
fit
#> $circles
#>            x        y         r
#> A 12.4845728 6.879429 10.249012
#> B  0.3372186 1.307356  9.723065
#> C  6.1716324 3.930091  6.482045
#> 
#> $original_areas
#>     A     B     C   A&B   A&C   B&C A&B&C 
#>    10     9     4     2     3     3     2 
#> 
#> $fitted_areas
#>        A        B        C      A&B      A&C      B&C    A&B&C 
#> 9.999998 8.999996 4.000001 2.056520 2.999988 2.999991 1.999978 
#> 
#> $residuals
#>             A             B             C           A&B           A&C 
#>  2.310981e-06  4.409024e-06 -7.328665e-07 -5.652050e-02  1.202451e-05 
#>           B&C         A&B&C 
#>  9.411775e-06  2.216915e-05 
#> 
#> $stress
#> [1] 0.00171429
#> 
#> attr(,"class")
#> [1] "eulerr" "list"
```

and plot it using `plot`.

``` r
plot(fit)
```

License
-------

eulerr is open source software, licensed under GPL-3.

Thanks
------

eulerr would not be possible without Ben Fredrickson's work on [venn.js](http://www.benfrederickson.com) or Leland Wilkinson's [venneuler](https://cran.r-project.org/web/packages/venneuler/index.html).
