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
      ..$ downloadDate: POSIXct[1:1], format: "2023-07-11 16:02:56"
      ..$ publishDate : chr "2023-01-28"
      ..$ infoURL     : logi NA
      ..$ API         : logi NA
      ..$ additional  : list()

## Basic analysis

The number of records in the database:

Regular Quarto-stlye Rmarkdown follows from here.

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
