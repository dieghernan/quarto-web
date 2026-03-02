``` r
library(gt)
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
islands_tbl <-
  tibble(
    name = names(islands),
    size = islands
  ) |>
  arrange(desc(size)) |>
  slice(1:10)

gt_tbl <- gt(islands_tbl)

gt_tbl <-
  gt_tbl |>
  tab_header(
    title = "Large Landmasses of the World",
    subtitle = "The top ten largest are presented"
  )

gt_tbl <-
  gt_tbl |>
  tab_source_note(
    source_note = "Source: The World Almanac and Book of Facts, 1975, page 406."
  ) |>
  tab_source_note(
    source_note = md("Reference: McNeil, D. R. (1977) *Interactive Data Analysis*. Wiley.")
  )

# Show the gt table
gt_tbl
```

| Large Landmasses of the World                                       |       |
|---------------------------------------------------------------------|-------|
| The top ten largest are presented                                   |       |
| name                                                                | size  |
| Asia                                                                | 16988 |
| Africa                                                              | 11506 |
| North America                                                       | 9390  |
| South America                                                       | 6795  |
| Antarctica                                                          | 5500  |
| Europe                                                              | 3745  |
| Australia                                                           | 2968  |
| Greenland                                                           | 840   |
| New Guinea                                                          | 306   |
| Borneo                                                              | 280   |
| Source: The World Almanac and Book of Facts, 1975, page 406.        |       |
| Reference: McNeil, D. R. (1977) *Interactive Data Analysis*. Wiley. |       |
