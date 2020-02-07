
<!-- README.md is generated from README.Rmd. Please edit that file -->

# metathis <a href='https://pkg.garrickadenbuie.com/metathis'><img src='man/figures/logo.png' align="right" height="120" /></a>

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/metathis)](https://CRAN.R-project.org/package=metathis)
[![Lifecycle:
stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://www.tidyverse.org/lifecycle/#stable)
[![travis](https://travis-ci.org/gadenbuie/metathis.svg?branch=master)](https://travis-ci.org/gadenbuie/metathis)
<!-- badges: end -->

## Why metathis?

The goal of **metathis** is to help you add HTML `<meta>` tags to your
[R Markdown](https://rmarkdown.rstudio.com) and
[Shiny](https://shiny.rstudio.com) apps.

HTML `<meta>` tags provide browsers and social media with metadata about
HTML pages. Using `<meta>` tags will help your users find your articles,
Shiny apps, and presentations, and will help you make sure they look
great in social media timelines.

**metathis** makes the process of adding these tags to your R Markdown
pages and Shiny apps easier by using the
[htmltools](https://github.com/rstudio/htmltools) package to add
`<meta>` tags as a dependency, added directly to the document in an R
code chunk or your Shiny app UI rather than requiring you to adjust
templates or write additional files.

If you want great looking social media cards, the
[`meta_social()`](http://pkg.garrickadenbuie.com/metathis/reference/meta_social.html)
function will help you add everything you need for Twitter, Facebook and
other social media sites that support the Open Graph protocol.

## Installation

You can install the latest version of metathis from
[Github](https://github.com/gadenbuie/metathis) with:

``` r
devtools::install_github("gadenbuie/metathis")
```

## Works In

✅ [R Markdown](https://rmarkdown.rstudio.com) HTML Documents  
✅ [Shiny](https://shiny.rstudio.com) Apps  
✅ [xaringan](https://slides.yihui.name/xaringan)  
✅ [pagedown](https://github.com/rstudio/pagedown)  
✅ [bookdown](https://bookdown.org/)  
❌ [blogdown](https://bookdown.org/yihui/blogdown)  
❌ [pkgdown](https://pkgdown.r-lib.org)

`<meta>` tags can be added to ✅ packages with a standard R chunk

```` markdown
```{r, echo=FALSE}
meta() %>% 
  meta_description("My awesome presentation")
```
````

For other packages or situations, you can use `include_meta()` to
explicitly declare the meta tags as an html dependency or use
`write_meta()` to save the `<meta>` tags to an `.html` file that can be
included via `includes: in_header`. (In blogdown, consult your
blogdown/hugo theme for the correct inclusion method.)

```` markdown
```{r blogdown-meta, echo = FALSE}
meta() %>% 
  meta_description("A fantastic blog post") %>% 
  write_meta("meta.html")
```
````

## Example

### In R Markdown

This is a basic example that re-creates the `<meta>` tags for the [R for
Data Science](https://r4ds.had.co.nz/) book.

``` r
library(metathis)

meta() %>%
  meta_description(
    "This book will teach you how to do data science with R..."
  ) %>% 
  meta_name("github-repo" = "hadley/r4ds") %>% 
  meta_viewport() %>% 
  meta_social(
    title = "R for Data Science",
    url = "https://r4ds.had.co.nz",
    image = "https://r4ds.had.co.nz/cover.png",
    image_alt = "The cover of the R4DS book",
    og_type = "book",
    og_author = c("Garrett Grolemund", "Hadley Wickham"),
    twitter_card_type = "summary",
    twitter_creator = "@hadley"
  )
#> Warning: knitr output format is not HTML. Use `include_meta()` to ensure that
#> the <meta> tags are properly included in the <head> output (if possible).
```

### In Shiny Apps

To use `metathis` in Shiny apps, simply call `meta()` and related tags
anywhere inside your page UI, for example inside `fluidPage()`.

``` r
ui <- fluidPage(
  # Application title
  titlePanel("metathis Example"),
  
  meta() %>%
    meta_social(
      title = "metathis",
      description = "<meta> and social media cards for web things in R",
      url = "https://pkg.garrickadenbuie.com/metathis",
      image = "https://garrickadenbuie.com/apple-touch-icon-114x114.png",
      image_alt = "An image for social meda cards",
      twitter_creator = "@grrrck",
      twitter_card_type = "summary",
      twitter_site = "@grrrck"
  )
  # ... your UI ...
)
```

### In xaringan Slides

To use `metathis` in [xaringan](https://slides.yihui.name/xaringan)
slides, add `meta()` and related tags in a chunk anywhere in your
slide’s source `.Rmd` file. This example is from a [presentation on
the drake package](https://pkg.garrickadenbuie.com/drake-intro/).

```` markdown
```{r meta, echo=FALSE}
library(metathis)
meta() %>%
  meta_general(
    description = "A gentle introduction to reproducible data workflows with the {drake} package.",
    generator = "xaringan and remark.js"
  ) %>% 
  meta_name("github-repo" = "gadenbuie/drake-intro") %>% 
  meta_social(
    title = "Reproducible Data Workflows With Drake",
    url = "https://pkg.garrickadenbuie.com/drake-intro",
    image = "https://pkg.garrickadenbuie.com/drake-intro/assets/images/drake-intro-cover.jpg",
    image_alt = "The first slide of the Reproducible Data Workflows with drake presentation, featuring the drake hex logo and neatly ordered row of items on a desk (eraser, pencil, coffee cup, paperclips).",
    og_type = "website",
    og_author = "Garrick Aden-Buie",
    twitter_card_type = "summary_large_image",
    twitter_creator = "@grrrck"
  )
```
````

## Thanks

Thanks to [Josh Buchea](https://github.com/joshbuchea) for providing an
[excellent and indispensible
resource](https://github.com/joshbuchea/HEAD) on `<meta>` tags and other
things that go in the HTML `<head>` tags.

Thanks also to [Malcolm Barret](https://github.com/malcolmbarrett).
Watching over his shoulder as he developed
[ymlthis](https://r-lib.github.io/ymlthis) made putting this package
together so much easier.

Finally, thanks to the [RStudio team](https://github.com/rstudio) and
others who developed [htmltools](https://github.com/rstudio/htmltools)
for making HTML in R a breeze.
