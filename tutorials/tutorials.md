---
title: Tutorials
subttitle: Using BioDeepTime in analytical code
bibliography: 'bibliography.bib'
format:
  gfm: 
    variant: +yaml_metadata_block
permalink: /tutorials/
layout: page
---

The tutorial here represents the absolute basics of using the
BioDeepTime database. More elaborate tutorials will be made available on
[Evolv-ED](https://www.evolv-ed.net/databases/registry/biodeeptime.html).

Add `toc: true` to the metadata of the .md file for a table of contents.

## The Data

### Download

The BioDeepTime database is made available through the ‘chronosphere’
research data API. The [R
client](https://cran.r-project.org/package=chronosphere) to access data
can be installed from the CRAN servers with:

``` r
install.packages("chronosphere")
install.packages("tidyverse")
```

The most up-to-date version of the denormalized BioDeepTiem database can
be accessed with:

``` r
# attach package
library(chronosphere)
```

    Chronosphere - Evolving Earth System Variables
    Important: never fetch data as a superuser / with admin. privileges!

    Note that the package was split for efficient maintenance and development:
     - Plate tectonic calculations -> package 'rgplates'
     - Arrays of raster and vector spatials -> package 'via'

``` r
library(tidyverse) # for data manipulation
```

    ── Attaching packages
    ───────────────────────────────────────
    tidyverse 1.3.2 ──

    ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ✔ tidyr   1.2.0      ✔ stringr 1.4.0 
    ✔ readr   2.1.2      ✔ forcats 0.5.1 
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::collapse() masks divDyn::collapse()
    ✖ tidyr::fill()     masks divDyn::fill()
    ✖ dplyr::filter()   masks stats::filter()
    ✖ dplyr::lag()      masks stats::lag()
    ✖ dplyr::slice()    masks divDyn::slice()

``` r
# download data, verbose=FALSE hides the default chatter 
bdt <- fetch("biodeeptime", verbose=FALSE)
```

Note that this table is rather large and might take a bit of time to
load. The accessible data items can be downloaded with
(`datasets("biodeeptime")`).

### Structure

The default representation of the denormalized table is a `data.frame`,
where every row represents one record or biogeographic observation (the
presence of a taxon in a sample).

``` r
str(bdt)
```

    'data.frame':   7432199 obs. of  38 variables:
     $ db                : chr  "Neotoma" "Neotoma" "Neotoma" "Neotoma" ...
     $ seriesID          : chr  "TS_1" "TS_1" "TS_1" "TS_1" ...
     $ seriesOriginalName: chr  "Konus Exposure, Adycha River" "Konus Exposure, Adycha River" "Konus Exposure, Adycha River" "Konus Exposure, Adycha River" ...
     $ seriesOriginalID  : chr  "11" "11" "11" "11" ...
     $ long              : num  136 136 136 136 136 ...
     $ lat               : num  67.8 67.8 67.8 67.8 67.8 ...
     $ depthUnit         : chr  "cmbct" "cmbct" "cmbct" "cmbct" ...
     $ ageModel          : chr  "4" "4" "4" "4" ...
     $ reason            : chr  "Community analysis" "Community analysis" "Community analysis" "Community analysis" ...
     $ sampleID          : chr  "S_1" "S_1" "S_1" "S_1" ...
     $ sampleOriginalID  : chr  "158" "158" "158" "158" ...
     $ sampleOriginalName: chr  NA NA NA NA ...
     $ depth             : num  0 0 0 0 0 0 0 0 0 0 ...
     $ age               : num  1321 1321 1321 1321 1321 ...
     $ ageProc           : chr  "bchron" "bchron" "bchron" "bchron" ...
     $ ageOld            : num  2463 2463 2463 2463 2463 ...
     $ ageYoung          : num  355 355 355 355 355 ...
     $ timeOriginalUnit  : chr  "Radiocarbon years BP" "Radiocarbon years BP" "Radiocarbon years BP" "Radiocarbon years BP" ...
     $ timeOriginal      : num  1000 1000 1000 1000 1000 1000 1000 1000 1000 1000 ...
     $ timeOriginalOld   : num  NA NA NA NA NA NA NA NA NA NA ...
     $ timeOriginalYoung : num  NA NA NA NA NA NA NA NA NA NA ...
     $ waterDepth        : num  NA NA NA NA NA NA NA NA NA NA ...
     $ preservation      : chr  NA NA NA NA ...
     $ samplingEffort    : num  809 809 809 809 809 809 809 809 809 809 ...
     $ minimumMesh       : num  NA NA NA NA NA NA NA NA NA NA ...
     $ maximumMesh       : num  NA NA NA NA NA NA NA NA NA NA ...
     $ environment       : chr  "Terrestrial or Freshwater" "Terrestrial or Freshwater" "Terrestrial or Freshwater" "Terrestrial or Freshwater" ...
     $ samplingEffortType: chr  NA NA NA NA ...
     $ taxonID           : int  11 6 1 8 7 3 4 10 2 13 ...
     $ analyzedTaxon     : chr  "Cyperaceae" "Cichorioideae" "Ranunculaceae undiff." "Artemisia" ...
     $ species           : chr  NA NA NA NA ...
     $ genus             : chr  NA NA NA NA ...
     $ openNomenclature  : chr  NA NA NA NA ...
     $ analyzedRank      : chr  NA NA NA NA ...
     $ group             : chr  "Vascular plants and bryophytes" "Vascular plants and bryophytes" "Vascular plants and bryophytes" "Vascular plants and bryophytes" ...
     $ abundance         : num  7 3 1 5 3 2 2 6 1 22 ...
     $ abundanceUnit     : chr  "count" "count" "count" "count" ...
     $ refID             : chr  "2" "2" "2" "2" ...
     - attr(*, "chronosphere")=List of 13
      ..$ dat         : chr "biodeeptime"
      ..$ var         : chr "denormalized"
      ..$ res         : logi NA
      ..$ ver         : num 0.6
      ..$ datafile    : chr "biodeeptime.rds"
      ..$ item        : int 14
      ..$ reference   : chr "Jansen A. Smith, Marina C. Rillo, Ádám T. Kocsis, Maria Dornelas, David Fastovich, Huai-Hsuan M. Huang, Lukas J"| __truncated__
      ..$ bibtex      : chr "@misc{jansen_a_smith_2023_7504617,\n author = {Jansen A. Smith and\nMarina C. Rillo and\nÁdám T. Kocsis and\nMa"| __truncated__
      ..$ downloadDate: POSIXct[1:1], format: "2023-07-13 10:46:17"
      ..$ publishDate : chr "2023-01-28"
      ..$ infoURL     : logi NA
      ..$ API         : logi NA
      ..$ additional  : list()

## Basic analyses

The number of time series in the database:

``` r
length(unique(bdt$seriesID))
```

    [1] 10071

The number of records in the database:

``` r
length(bdt$db)
```

    [1] 7432199

The number of unique sampling locations:

``` r
nrow(unique(bdt[, c("long", "lat")]))
```

    [1] 8762

The oldest record in each database:

``` r
bdt %>% group_by(db) %>% summarize(max = max(age))
```

    # A tibble: 9 × 2
      db                               max
      <chr>                          <dbl>
    1 BioTIME                         49.4
    2 Direct uploads             1146200  
    3 Geobiodiversity Database 451050000. 
    4 MARBEN                    77200000  
    5 Neotoma                   23900000  
    6 Neptune SandBox          151075752  
    7 Paleobiology Database    150889174. 
    8 SedTraps                       -28.4
    9 Triton                    65996942. 

Finding the mean age (relative to 1950) of a sample from modern
databases (BioTIME and SedTraps):

``` r
modern <- bdt %>%
  filter(db == "BioTIME" | db == "SedTraps") ## filtering to only modern data

mean(modern$age) 
```

    [1] -44.52683

Finding the mean age (relative to 1950) of a sample from fossil
databases:

``` r
fossil <- bdt %>%
  filter(db != "BioTIME" & db != "SedTraps") ## filtering to exclude modern data

mean(fossil$age) 
```

    [1] 4976267

We can have a citation here: such as (Kocsis et al. 2019)

# References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-kocsis2019package" class="csl-entry">

Kocsis, Ádám T., Carl J. Reddin, John Alroy, and Wolfgang Kiessling.
2019. “The R Package <span class="nocase">divDyn</span> for Quantifying
Diversity Dynamics Using Fossil Sampling Data.” *Methods in Ecology and
Evolution* 10 (5): 735–43. <https://doi.org/10.1111/2041-210X.13161>.

</div>

</div>
