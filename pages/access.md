---
layout: page
title: Accessing data
permalink: /database/access/
---


<div class="columns is-vcentered">
<div class="column is-9" markdown="1">
All [published versions]({{site.url}}{{site.baseurl}}/database/milestones) of BioDeepTime are published as [Zenodo](https://zenodo.org) depositions, and are accessible as static files under the main DOI. This DOI always redirects to the most up-to-date version of the database:

<div class="control">
<div class="tags has-addons">
	<span class="tag is-dark">DOI</span>
	<a href="https://doi.org/10.5281/zenodo.7504616" class="tag is-info">10.5281/zenodo.7504616</a>
</div>
</div>

</div>
<div class="column is-3">
<a href="https://doi.org/10.5281/zenodo.7504616"  markdown="1">
<img src="{{site.url}}{{site.baseurl}}/images/logos/zenodo.png" style="border-radius:3%">
</a>
</div>

</div>

* * *

# Files of the most recent version (v0.6)

The current files of **BioDeepTime** (v0.6)are accessible from the links below.
Both the original relational database and a record-denormalized data frame is available for download.

### 1) Record-denormalized data frame
<div class="columns is-vcentered">
<div class="column is-2" markdown="1">
![table]({{site.url}}{{site.baseurl}}/images/table.png)

</div>
<div class="column is-9" markdown="1">

The **BioDeepTime** database in a single table, where every row represents one biogeographic record *(occurrence)*.

This form of the database is optimized for analyses, and can be accessed in binary R (`.rds`), plain text (`.csv`) and Apache Parquet (`.parquet`) formats:

 <a class="button is-link is-light" href="https://zenodo.org/record/7504617/files/biodeeptime.rds?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>.rds</span>
  </a>
 <a class="button" href="https://zenodo.org/record/7504617/files/biodeeptime_csv.zip?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>.csv</span>
  </a>
 <a class="button" href="https://zenodo.org/record/7504617/files/biodeeptime_parquet.zip?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>.parquet</span>
  </a>

</div>
</div>
### 2) SQLite Relational database

<div class="columns is-vcentered">
<div class="column is-2" markdown="1">
![table]({{site.url}}{{site.baseurl}}/images/rdb.png)

</div>
<div class="column is-9" markdown="1">


This is the source of the denormalized table above.  

 <a class="button is-primary is-light" href="https://zenodo.org/record/7504617/files/biodeeptime_sqlite.zip?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>.sqlite</span>
  </a>

</div>
</div>
### 3) Additional data 

##### - References 

 <a class="button" href="https://zenodo.org/record/7504617/files/references.csv?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>References (.csv)</span>
  </a>

##### - BChron ages for Neotoma

 <a class="button" href="https://zenodo.org/record/7504617/files/neotoma_bchron.rds?download=1">
    <span class="icon">
	<i class="fas fa-download"></i>
	</span>
    <span>Neotoma BChron ages (.rds)</span>
  </a>
* * *

<div class="columns is-vcentered">
<div class="column is-8" markdown="1">

# Via the `chronosphere` R package

New versions are automatically added to the `chronosphere` data-versioning framework (currently available in R only). You can access the BioDeepTime with the following coordinates:

```R
library(chronosphere)

# available datasets
available <- chronosphere::datasets(dat="biodeeptime")

# most recent occurrence table
bdt <- chronosphere::fetch(dat="biodeeptime")
```


<a class="button is-link is-light" href="{{site.url}}{{site.baseurl}}/tutorials">Check out the tutorials for a demonstration!</a> 

</div>

<div class="column is-2">
<a href="https://chronosphere.info"><img alt="chronosphere" src="{{site.url}}{{site.baseurl}}/images/logos/chronosphere.png"></a> 
</div>
</div>
