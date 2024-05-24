
<!-- README.md is generated from README.Rmd. Please edit that file -->

# mtf_report_mvp

<!-- badges: start -->
<!-- badges: end -->

The goal of project is to provide a proof-of-concept for automating
Multi-Tier Framework (MTF) survey report creation using R/Quarto.

This project aims to replicate the salient features of MTF reports in
Microsoft Word and thereby demonstrate this to be a viable option for
semi-automated reprot production. The MTF reference document used for
this project can be found
[here](https://openknowledge.worldbank.org/entities/publication/8a84e19f-ae3c-5b4f-8431-f9c0ad028eb3).
See [other reports
here](https://www.worldbank.org/en/results/2020/11/10/measuring-energy-access-in-multidimensional-way-through-household-surveys-multi-tier-energy-access-tracking-framework-global-surveys)

## Setup/installation

This project has the following system dependencies:

- [R](https://cran.rstudio.com/)
- [RStudio](https://posit.co/download/rstudio-desktop/)
- [Quarto](https://quarto.org/docs/get-started/)

In addition, one needs to install these packages with the following
code:

``` r
if (!require("pak")) {
  install.packages("pak")
}

required_packages <- c(
  "tibble", # creating test data
  "flextable", # tables
  "ggplot2", # plots
  "ggtext", # using images as labels
  "scales", # adjusting plot scales/labels
  "ggrepel", # adding non-overlapping labels
  "ggpp", # organizing non-overlapping labels
  "cowplot", # drawing images in/behind the plot
  "magick", # ingest and manipulate the image to be placed in the plot
  "dplyr", # data manipulation
  "forcats", # manipulating string/factor variables
)

pak::pak(required_packages)
```

## Usage

- Download/clone the project
- Open `mtf_report.qmd` in RStudio
- Click on the `Render` button to render the document
- See the resulting Microsoft Word document in `mtf_report.docx`

## Implementation

The project uses Quarto to create a Microsoft Word document that has:

- Style matching the MTF report design guidelines
- Figures and tables auotmatically built from country data

## Background on MTF report style

At a high level, MTF survey reports have:

- **Initiative-level styling.** Every report for a country follow the
  visual design guidelines for the initiative (e.g., heading styles,
  text box styles, etc.).
- **Country-level adaptation of the initiative style.** In particular,
  each country adopts a country-level color scheme, and those color
  decisions inform the visual stylings of document structure (e.g.,
  headings, text boxes, etc.) as well as data visualizations (e.g., a
  country-specific five-color palette for certain plots).
- **Initiative-level content**. For the most part, background
  information on MTF is the same from one report to another. However,
  there is standardized adaptation of content for each country. Beyond
  usage of country data in report figures and tables, some content is
  country-specific. For example, a country map is used, variously, to
  show the dispersion of the survey sample and to serve as an icon in
  charts representing national estimates.

In terms of figures and tables, they exhibited several distinctive
features:

- **Use of a country-specific color palette.** For tables, country
  colors are used for the header and row striping. For plots, a
  country-specific palette is used for visualizations that compare
  groups (that are not MTF tiers).
- **Usage of logos/icons as labels.** For plots that compare national,
  urban, and rural estimtates, icons are used to represent each sample
  group. For the national group, reports use an outline of the country
  featured in the report.
- **Usage of logos/icons as a “watermark” in plots.** For other plots
  that provide subnational estimates, the urban and rural icons are used
  as watermark in the plot to indicate which estimates appear in that
  panel.
