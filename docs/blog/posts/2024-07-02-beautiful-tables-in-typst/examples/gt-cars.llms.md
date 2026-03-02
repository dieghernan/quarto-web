``` r
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
library(gt)

gtcars %>%
  dplyr::filter(mfr == "Ferrari", hp < 900) %>%
  dplyr::select(model, hp, mpg_c, mpg_h, msrp) %>%
  gt() %>%
  data_color(
    columns = hp,
    palette = c("white", "orange", "red"),
    domain = c(500, 750)
  ) %>%
  data_color(
    columns = c(mpg_c, mpg_h),
    palette = c("white", "green"),
    domain = c(10, 25)
  ) %>%
  data_color(
    columns = msrp,
    palette = c("white", "pink", "red"),
    domain = NULL
  )
```

| model         | hp  | mpg_c | mpg_h | msrp   |
|---------------|-----|-------|-------|--------|
| 458 Speciale  | 597 | 13    | 17    | 291744 |
| 458 Spider    | 562 | 13    | 17    | 263553 |
| 458 Italia    | 562 | 13    | 17    | 233509 |
| 488 GTB       | 661 | 15    | 22    | 245400 |
| California    | 553 | 16    | 23    | 198973 |
| GTC4Lusso     | 680 | 12    | 17    | 298000 |
| FF            | 652 | 11    | 16    | 295000 |
| F12Berlinetta | 731 | 11    | 16    | 319995 |
