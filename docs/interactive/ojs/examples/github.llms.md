# GitHub API

Code

- [Show All Code](javascript:void(0))

- [Hide All Code](javascript:void(0))

- 

  ------------------------------------------------------------------------

- [View Source](javascript:void(0))

Demonstration of using the [GitHub API](https://developer.github.com/v3).

Code

``` js
viewof repo = Inputs.radio(
  [
    "pandas-dev/pandas",
    "tidyverse/ggplot2",
  ], 
  { label: "Repo:", value: "pandas-dev/pandas"}
)
```

Code

``` js
import { chart } with { commits as data } from "@d3/d3-bubble-chart"
chart
```

## Data

``` js
d3 = require('d3')
contributors = await d3.json(
  "https://api.github.com/repos/" + repo + "/stats/contributors"
)
commits = contributors.map(contributor => {
  const author = contributor.author;
  return {
    name: author.login,
    title: author.login,
    group: author.type,
    value: contributor.total
  }
})
```

``` js
Inputs.table(commits, { sort: "value", reverse: true })
```
