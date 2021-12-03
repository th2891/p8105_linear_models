Bootstrapping
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(viridis)
```

    ## Loading required package: viridisLite

``` r
library(modelr)
library(mgcv)
```

    ## Loading required package: nlme

    ## 
    ## Attaching package: 'nlme'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     collapse

    ## This is mgcv 1.8-38. For overview type 'help("mgcv-package")'.

``` r
knitr::opts_chunk$set(
  echo = TRUE,
  warning = FALSE, 
  fig.width = 8, 
  fig.height = 6, 
  out.width = "90%"
)
theme_set(theme_minimal() + theme(legend.position = "bottom"))

options(
  ggplot2.continuous.colour = "viridis",
  ggplot2.continuous.fill = "virids"
)

scale_colour_discrete = scale_color_viridis_d
scale_fill_discrete = scale_fill_viridis_d
```

Bootstrapping

-   idea is to mimic repeated sampling with the one sample you have

-   your sample is drawn at random from your population

\*\* you’d like to draw more samples but can’t

\*\* so you draw a bootstrap sample from one sample you have (sample
with replacement)

\*\* the bootstrap sample has the same size as the original sample and
is drawn with replacement

\*\* analyze this sample using whatever appraoch you want to apply

\*\* repeat

-   the repeated sampling framework often provides useful theoretical
    results under certain assumptions and/or asymptotics

\*\* sample means follow a known distribution \*\* regression
coefficients follow a known distribituion \*\* ORs follow a known
distribution

-   if assumptions aren’t met - or sample isn’t large enough for
    asymptotics, you can’t use “known distribution”

-   bootstrapping gets back to repeated sampling, and uses empirical
    rather than theoretical distribution of your statistic of interest

Coding the bootstrap

-   natural application of iterative tools

-   write function (or functions) to: \*\* draw a sample with
    replacement \*\* analyze the sample \*\* return object of interest

-   repeat process many times

-   keeping track of the bootstrap samples, analysis, and results in a
    single data frame that organizes the process and prevents mistakes

-   use list columns
