---
layout: page
title: Database structure
permalink: database/structure/
menubar_toc: true
hero_image: "../../images/bg/ocean.jpg"
---
<style>

.content table td{
	text-align: left
}
</style>
## Structure outlines 

BioDeepTime is a relational database compiled and stored in the SQLite 3 standard. Due to heterogeneity of the original data and variation in their focus and scopes, only a fraction of the data fields are copied over from the original database.  

<a href="{{site.url}}{{site.baseurl}}/images/concept.png" ><img src="{{site.url}}{{site.baseurl}}/images/concept.png"></a>
[*The basic entities of BioDeepTime (Smith, Rillo and Kocsis et al. [2023])*]({{site.url}}{{site.baseurl}}/database/attribution/#data-paper)


## Current structure

The structure described here represents the most up-to-date, [v1.0]({{site.url}}{{site.baseurl}}/database/milestones/#biodeeptime-v10-2023-07-12) version of BioDeepTime. The current schema includes 17 tables, which are organized according to the following entity-relationship diagram:

<a href="{{site.url}}{{site.baseurl}}/images/schema.svg" ><img src="{{site.url}}{{site.baseurl}}/images/schema.svg"></a>

* * *

# Description of tables

## Assemblage time series-related tables

<div class="box" markdown="1">
### `sources` table

The `sources` table include information on the constituent databases of the BioDeepTime database.

- **dbID** (INTEGER): Primary key, unique ID of a source database.
- *db* (varchar): The name of a source database.
- *seriesOriginalIDField* (varchar): The name of the field that stores the series IDs in the source database.
- *sampleOriginalIDField* (varchar): The name of the field the stores the sample IDs in the source database.
- *refID* (INTEGER): Foreign key, refers to *refID* in the `refs` table. The reference of the source database.
</div>

<div class="box" markdown="1">
### `series` table

The `series` table includes information unique to an entire assemblage time series.

- **seriesID** (INTEGER): Primary key, unique ID of the assemblage time series. A positive integer that starts with the `TS_` prefix.
- *dbID* (INTEGER): Foreign key, refers to *dbID* in the `sources` table. Codes the source database that the time series is from.
- *long* (float): The present-day longitude coordinate of the time series, assumed to be WGS84.
- *lat* (float): The present-day latitude coordinat of the time series, assumed to be WGS84.
- *seriesOriginalName* (varchar): If applicable, the human-readable name of the time series, as it is saved in the original database.
- *seriesOriginalID* (varchar): The original unique id of the time series, as it is stored in the source database.
- *ageModelID* (INTEGER): Foreign key, refers to *ageModelID* in the `ageModels` table. If explicitly saved, refers to the age model used with the time series.
- *timeOriginalUnitID* (INTEGER): Foreign key, refers to *timeOriginalUnitID* in the `timeOriginalUnits` table. All samples in the time series originally have time information assigned to them. These are in the same unit in every time samples, which is coded in this field.
- *depthUnitID* (INTEGER): Foreign key, refers to *depthUnitID* in the `depthUnits` table. All samples in the time series originally have vertical position (i.e. depth) information assigned to them. These are in the same unit in every time samples, which is coded in this field.
- *reasonID* (INTEGER): Foreign key, refers to *reasonID* in the `reasons` table. The samples in the assemblage time series were analyzed with a scientific goal in mind. 
- *timeDepthUnique* (INTEGER): Boolean field, including either `0` or `1`. Some time series have replicate samples coming from the depth/vertical position. If such replicate samples are not present, then every sample in the series represent a unique time point, coded with `1`. If there are multiple samples coming from the same depth/vertical position, this field is `0`.
- *groupID* (INTEGER):Foreign key, refers to *groupID* in the `groups` table. Every time series is limited to a particular group. 
</div>

<div class="box" markdown="1">
### `ageModels` table

Lookup table for the names of age models.

- **ageModelID** (INTEGER): Primary key, unique ID of an age model name.
- *ageModel* (varchar): The name of an age model.
</div>

<div class="box" markdown="1">
### `timeOriginalUnits` table

Lookup table for the units in which time is expressed in the original database.

- **timeOriginalUnitID** (INTEGER): Primary key, unique ID of unit of time. 
- *timeOriginalUnit* (varchar): The name of the time unit, either age or date. The value is either increasing or decreasing in the direction of time. 

| timeOriginalUnit                  | description                                                             | direction  |
|-----------------------------------|-------------------------------------------------------------------------|------------|
| `AD`                              | Calendar years (AD).                                                    | increasing |
| `ka`                              | Age in thousands of years                                               | decreasing |
| `ma`                              | Age in millions of years                                                | decreasing |
| `Radiocarbon years BP`            | Age in years, result of radiocarbon dating.                             | decreasing |
| `Calibrated radiocarbon years BP` | Age in years, result of radiocarbon dating and calibration.             | decreasing |
| `Calendar years BP`               | Age in years.                                                           | decreasing |
| `Varve years BP`                  | Age in years coming from varve-chronology.                              | decreasing |
| `rday`                            | Days expressed in the date format of R, number of days after 1970-01-01 | increasing |
| `rmonth`                          | Indicates monthly resolution. As `rday`, the 15th day of the month.     | increasing |

</div>

<div class="box" markdown="1">
### `depthUnits` table

Lookup table for the units in which vertical position of sample in a time series is expressed.

- **depthUnitID** (INTEGER): Primary key, unique ID of the unit of the vertical position of the sample. 
- *depthUnit* (varchar): The name of the unit. 

| depthUnit | description                |
|-----------|----------------------------|
| `mbsf`    | meters below sea floor     |
| `cmbct`   | centimeter below core top  |
| `mfsb`    | meters from section bottom |

</div>

<div class="box" markdown="1">
### `reasons` table

Lookup table for the reasons for which the series was described.

- **reasonID** (INTEGER): Primary key, unique ID of the reason. 
- *reason* (varchar): The reason as a string of characters.

| reason               | description                                                                         |
|----------------------|-------------------------------------------------------------------------------------|
| `Community analysis` | The purpose of sample description is community analysis.                            |
| `Biostratigraphy`    | The purpose of sample description is biostratigraphic correlation.                  |
| `Selected species`   | The purpose of sample description is the assesment of a pre-select species.         |
| `Extreme event`      | The purpose of sample description is the assessment of an extreme geological event. |

</div>

<div class="box" markdown="1">

### `groups` table

Lookup table for the groups that the time series describe.

- **groupID** (INTEGER): Primary key, unique ID of the group.
- *group* (varchar): The name of the group. If the records in the time series belong to multiple groups, the entry is `Mixed`.

</div>

## Assemblage sample-related tables

Samples of biological assemblages are grouped into the assemblage time series (multiple samples/series). Samples typically represent different states of the assemblage (temporal horizons), but this is not necessarily the case.  

<div class="box" markdown="1">

### `samples` table

- **sampleID** (varchar): Primary key, the unique ID of the sample in BioDeepTime. A positive integer that starts with the `S_` prefix.
- *seriesID* (varchar): Foreign key, refers to a the *seriesID* field in the `series` table. The ID of the time series, the sample belongs to.
- *sampleOriginalName* (varchar): The original, human-readable name of the sample, copied from the source database.
- *sampleOriginalID* (varchar): The original unique ID of the sample, copied from the source database. These values come from the field which is recorded in the *sampleOriginalIDField* field of the `source` table.
- *timeOriginal* (float): The numeric value that represents the age/date of the sample, copied from the source database. The unit of measurement is time series-specific, and is therefore recorded in the *timeOriginalUnitID* of the `series` table.
- *timeOriginalOld* (float): The recorded older estimate for the age/date of the sample, in the same unit as *timeOriginal.*
- *timeOriginalYoung* (float): The recorded younger estimate for the age/date of the sample, in the same unit as *timeOriginal.*
- *age* (float): Sample age estimate expressed as years Before Present (relative to 1950, higher values mean older ages, negative values represent ages younger than 1950). 
- *ageProcID* (INTEGER): Foreign key, refers to the *ageProcID* field of the `ageProcs` table. The transformation that was used to derive the *age*, *ageOld* and *ageYoung* column
- *ageOld* (float): Older confidence limit of the the age estimate, expressed as years Before Present. 
- *ageYoung* (float): Younger confidence limit of the the age estimate, expressed as years Before Present. 
- *depth* (float): The vertical position of the sample if the assemblage time series has a physical record. The unit of measurement (including directions) is specific to the time series, and is recorded in the *depthUnitID* field of the `series` table.
- *sequence* (float): The order of the samples in the time series, increasing in the direction of time. If samples are contemporaneous, the values are floating point numbers, as output by the `rank()` R function. This column serves internal purposes and is not exported to the denoramlized copy of the database. 
- *waterDepth* (float): The estimated water depth in which the sample was taken, expressed in meters (if applicable). 
- *environmentID* (INTEGER): Foreign key, refers to the *environmentID* field of the `environments` table. The general biological realm that the sample represents. 
- *preservation* (varchar): Textual information on the preservation quality of the sample, copied over from the source database, if it was present. 
- *samplingEffort* (float): Numeric value that expresses a sampling-related quantity. Its unit is recorded in the *samplingEffortType* column.
- *samplingEffortTypeID* (INTEGER): Foreign key, refers to the *samplingEffortTypeID* column of the `samplingEffortTypes` table. The units in which sampling effort is expressed. 
- *minimumMesh* (float): If applicable, the minimum size of the mesh used to filter a microfossil/microorganism sample (in micrometers).
- *maximumMesh* (float): If applicable, the maximum size of the mesh used to filter a microfossil/microorganism sample (in micrometers).
- *totalCount* (float): If applicable, the sum of the sample's total abundance. 

</div>

<div class="box" markdown="1">

### `refs` table

List of references where the original record come from. Includes the references of the source databases.

- **refID** (INTEGER): Primary key, the unique ID of every reference. 
- *ref* (varchar): The reference in text format, as it is stated in the original database. Standardization of format is ongoing.
- *bibtex* (varchar): A bibtex handle for the refs.bib file.

</div>

<div class="box" markdown="1">

### `reflinks` table

Many-to-many connection table, linking assemblage samples to the references. This information is denormalized to text values (multiple refID/sample is separated by a comma).

- *refID* (INTEGER): Foreign key, refers to the *refID* field of the `refs` table. A reference tied to the sample.
- *sampleID* (varchar): Foreign key, refers to the *sampleID* field of the `samples` table. A sample that is described in a reference.

</div>

<div class="box" markdown="1">

### `ageProcs` table

Lookup table, the transformation applied to the sample, which led to the *age* estimate of the `samples`. 

- **ageProcID** (INTEGER): Primary key, the unique ID of the transformation type. 
- *ageProc* (varchar): The name of the transformation. 


| ageProc                   | description                                                                                 |
|---------------------------|---------------------------------------------------------------------------------------------|
| `translated original`     | The original ages were copied, and were translated to years BP.                             |
| `bchron`                  | New ages estimates were calculated with the bchron R package.                               |
| `calibrated original`     | Original, radiometric dates were calibrated using the bchron R package.                     |
| `original`                | The originally stated ages were copied from the `timeOriginal` field.                       |
| `thickness-interpolation` | Ages were calculated from bed thickness during the compilation of the BioDeepTime database. |

</div>

<div class="box" markdown="1">

### `environments` table

Lookup table of the biological realms that the samples represent. 

- **environmentID** (INTEGER): Primary key, the unique ID of the environment. 
- *environment* (varchar): The name of the sampled environment. 


| environment                 | description                                                                     |
|-----------------------------|---------------------------------------------------------------------------------|
| `Marine`                    | The samples represent a marine aquatic environment.                             |
| `Freshwater`                | The samples represent a freshwater aquatic environment.                         |
| `Terrestrial`               | The samples represent terrestrial environment.                                  |
| `Terrestrial or Freshwater` | The samples represent either a terrestrial or a freshwater aquatic environment. |

</div>

<div class="box" markdown="1">

### `samplingEffortTypes` table

Lookup table of the units of sampling efforts.

- **samplingEffortTypeID** (INTEGER): Primary key, the unique ID of the sampling effort type. 
- *samplingEffortType* (varchar): The name of the sampling effort. 

| samplingEffortType | description                                    |
|--------------------|------------------------------------------------|
| `specimens`        | The number of specimens counted in the sample. |
| `g`                | The sample weight in grams.                    |
| `cm3`              | The volume of the sample in cubic centimeters. |
| `ml`               | The volume of the sample in milliliters.       |
| `km2`              | The area of the sample in square kilometers.   |
| `m2`               | The area of the sample in square meters.       |

</div>

## Occurrence record-related tables

The primary unit is one (occurrence) record: the presence of a taxon in a sample, which either is, or isn't associated with an abundance value. 

<div class="box" markdown="1">

### `records` table

Table to record many-to-many connections between taxa and samples. 

- **recordID** (INTEGER): Primary key, unique ID for every record.
- *sampleID* (varchar): Foreign key, refers to the *sampleID* field of the `samples` table.
- *taxonID* (INTEGER): Foreign key, refers to the *taxonID* field of the `taxa` table.
- *abundance* (float): A numeric value that contains the abundance information of the taxon in the sample. 
- *abundanceUnitID* (INTEGER): Foreign key, refers to the *abundanceUnitID* of the `abundanceUnits` table. 
</div>

<div class="box" markdown="1">

### `taxa` table

List of the taxonomic entries that occur in the sample. These entities were copied over from the original databases - assuming that taxonomy homogeneous within an assemblage time series.

- **taxonID** (INTEGER): Primary key, the unique ID of the taxon entry. 
- *analyzedTaxon* (varchar): The character string that refers to a taxon observation. These were copied over from the source databases. 
- *species* (varchar): If available, the clean, most likely binomen of the *analyzedTaxon* entry.
- *genus* (varchar): If available, the clean, genus name the *analyzedTaxon* belongs to. 
- *analyzedTaxonRankID* (INTEGER): Foreign key, refers to the *analyzedTaxonRankID* of the *analyzedRanks* table. The taxonomic rank of the *analyzedTaxon* entry. 
- *openNomenclature* (varchar): Qualifiers of open nomenclature that occur in the *analyzedTaxon* entry.

</div>

<div class="box" markdown="1">

### `analyzedRanks` table

Lookup table of the taxonomic ranks that the record represents.

- **analyzedTaxonRankID** (INTEGER): Primary key, the unique id of the rank.
- *analyzedRank* (varchar): The rank of the analyzed taxon.

| analyzedRank | description           |
|--------------|-----------------------|
| `Species`    | The rank of species.  |
| `Genus`      | The rank of genera.   |
| `Family`     | The rank of families. |
| `Order`      | The rank of orders.   |
| `Class`      | The rank of classes.  |
| `Phylum`     | The rank of phyla.    |
| `indet`      | Unidentified rank.    |

</div>	

<div class="box" markdown="1">

### `abundanceUnits` table

Lookup table of the units in which the abundance of a taxon in a sample is expressed. 

- **abundanceUnitID** (INTEGER): Primary key, the unique ID of the abundance unit.
- *abundanceUnit* (varchar): The name of the unit of abundance.

| abundanceUnit        | description                                                                                       |
|----------------------|---------------------------------------------------------------------------------------------------|
| `count`              | The number of specimens found in the sample (or in an observation, e.g. single quadrat - BioTime) |
| `percent`            | The percentage of the number of specimens occupied by the taxon in the sample.                    |
| `presence`           | Only the presence of a taxon is recorded.                                                         |
| `relative abundance` | The proportion of the number of specimens occupied by the taxon in the sample.                    |
| `density count`      | The number of individuals in a given volume or area. (BioTIME)                                    |
| `mean count`         | The mean number of species across several samples-quadrats (BioTIME)                              |
| `biomass cover`      | The area covered by a taxon in a sample.                                                          |
| `biomass volume`     | The volume of a taxon in a sample.                                                                |
| `biomass weight`     | The weight of a taxon in a sample.                                                                |
| `flux`               | Average number of specimens sampled per day per squared-meter (sediment trap data)                |

</div>
