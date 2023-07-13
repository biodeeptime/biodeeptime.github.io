---
layout: page
title: Milestones
permalink: database/milestones/
---

<div class="columns">

<div class="column is-8" markdown="1">

# Database milestones

**BioDeepTime** is drawing information from both static and dynamically-updated databases. Due to the heterogeneity of the constituent data, BioDeepTime is compiled manually in semi-regular intervals. These data products are versioned semantically, and are deposited separately - including the code that was used to build the version. These static data products were chosen to enhance reproducibility and tracability of results based on the database.

### Versioning

The planned versioning framework is: 

- **First-level**: Large structural changes and major addition of sources. 
- **Second-level**: Major corrections and additions of new timeseries. 
- **Third-level**: Minor corrections.  

</div>

<div class="column is-4">
<div class="contents" markdown="1">
<div class="menu">
<p class="menu-label">Contents</p>
<ul class="menu-list">
<li>
<a href="#milestones-explained">Milestones explained</a>  
</li>
<li>
<a href="#list-of-known-issues">List of known issues</a>  
</li>
<li>
<a href="#biodeeptime-v100-2023-07-12">Version 1.0.0</a>  
</li>
<li>
<a href="#biodeeptime-v060-2023-01-17">Version 0.6.0</a>  
</li>
</ul>
</div>
</div>
</div>

</div>

* * *

# List of known issues

### MARBEN
- Missing `species` and `genus` columns

### General
- References need manual review especially bibtex. Character encoding is still a recurring problem. Some references entities  represent multiple references. 

* * *

# Change log

## BioDeepTime v1.0.0 [2023-07-12]

### Added
- new field `samples.totalCount` that represents the sample size in the case of count data, rather than the target sampling effort
- Three new `abundanceUnit` categories: `"biomass cover"`, `"biomass weight"`, `"biomass volume"`
- bibtex handles to the `bibtex` column of the `refs` table. The candidate bibtex entries are in the refs.bib file.

### Changed
- The word occurrence was systmatically replaced with `record`. The `occurrences` table was renamed to `records`, its primary key from `occID` to `recordID`.
- The `timeUnits` table was renamed to `timeOriginalUnits` for better consistency. Consequently, the the fields `timeUnitID` and `timeUnit` were rename to `timeOriginalUnitID` and `timeOriginalUnit`, respectively.
- The `ranks` table was renamed to `analyzedRanks` for better consistency.
- Reference entries are forced into UTF-8 encoding

##### BioTime
- Omitted studies 39 and 217 due to potentially erroneous entries
- Added biomass data to where there were no `abundanceUnit`s earlier 
- Time series taxonomic/environment groups are added

##### Neotoma
- sample sum count is moved to `samples.totalCount` from `samples.samplingEffort`. Accordingly `samplingEfforType` is consistently set to `NA`.
- Neotoma references were split, multiple refs per samples are now properly indicated 
- Changed the taxon group to `Plants` 

##### Triton
- New version is used now - indicated to be released soon as Triton 2
- Fixed issues where all abundance values were relative abundances, even when count was indicated.
- The sample sum is now recorded in `samples.totalCount` and not in `samplingEffort`. In case where samples reflect normalization for 1 gramm, the value 1 is now recorded in `samplingEffort` with a `samplingEffortType` of "g".

##### SedTraps
- added missing `samplingEffortType` (all are m^2)

##### MARBEN
- added `samplingEffort` and `samplingEffortType` values from `processing`
- total count of count-type data
- added missing reason: `"Community analysis"`
- added reference to MARBEN

###### PBDB
- added total count of count-type data 

###### Direct uploads
- coccolithophore data: moved total count from `samplingEffort` to `totalCount`

## Removed

###### BioTime
- Studies 39 and 217 were removed due to quality reasons.

* * *

## BioDeepTime v0.6.0 [2023-01-17]

<a href="https://doi.org/10.5281/zenodo.7504617"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.7504617.svg" alt="DOI"></a>

### Added 
- The Geobiodiversity Database - the Fenxiang section

### Changed 
- moved the coccolith data to "Direct uploads"

### Deleted
- occurrenceTypeID column and occurenceType table

### Acknowledged
- The two Neptune time series that have mixed taxonomy represent true data.

* * *
