# planetary-knowledge-base

## Institutions Data
### institutions.csv
8135 rows × 5 columns

#### Data sources

Sourced from Global Registry of Scientific Collections https://www.gbif.org/grscicoll

(GRSciColl is synced weekly with Index Herbarium https://sweetgum.nybg.org/science/ih/)

#### Column definition

Columns: 'uuid','code','name','country', 'altCodes'

* uuid: Primary identifer
* code: Official institution short form code - e.g. BMNH
* name: Institution name - e.g. Natural History Museum
* country: ISO-3166 2-letter country code
* altCodes: Alternative institution codes - e.g. BM(NH), NHM

#### Relationships

* institution.country -> country.iso

## Country Data
### countries.csv
252 rows × 8 columns

Columns: 'ISO', 'ISO3', 'ISOnumeric', 'FIPS', 'countryName', 'Continent', 'geonameid', 'dependsFrom'

### alternateCountryNames.csv 
44430 rows × 15 columns

Columns: 'ISO', 'ISO3', 'ISOnumeric', 'FIPS', 'countryName', 'Continent', 'geonameid', 'dependsFrom', 'alternateNameId', 'isolanguage', 'altName', 'isPreferredName', 'isShortName', 'isColloquial', 'isHistoric'

#### Data sources

Sourced from GeoNames geographical database: https://www.geonames.org/

#### Column definition
* ISO			: ISO-3166 2-letter country code
* ISO3			: 3-letter ISO country code
* ISOnumeric 		: Numeric ISO country code
* FIPS 			: Most admin1 code are FIPS codes
* countryName		: Name of the geographical country point
* Continent 		: Geographical continent code
* geonameid		: Integer id of record in geonames database
* dependsFrom	: Dependent countries or territories
* alternateNameId	: Integer id of this alternate name
* isolanguage		: ISO 639 language code 2- or 3-characters; 4-characters 'post' for postal codes and 'iata','icao' and faac for airport codes, fr_1793 for French Revolution names,  abbr for abbreviation, link to a website (mostly to wikipedia), wkdt for the wikidataid
altName		: alternate name or name variant
* isPreferredName	: '1', if this alternate name is an official/preferred name
* isShortName		: '1', if this is a short name
* isColloquial		: '1', if this alternate name is a colloquial or slang term
* isHistoric		: '1', if this alternate name is historic and was used in the past

### Continent codes :
* AF : Africa			geonameId=6255146
* AS : Asia			geonameId=6255147
* EU : Europe			geonameId=6255148
* NA : North America		geonameId=6255149
* OC : Oceania		geonameId=6255151
* SA : South America		geonameId=6255150
* AN : Antarctica		geonameId=6255152

## Taxa Data
### taxa.parquet
1907100 rows × 7 columns

#### Data sources

Sourced from GBIF Backbone Taxonomy https://doi.org/10.15468/39omei

Filtered on family=Plantae

#### Column definition

Columns: taxonID, name, authorship, taxonRank, status, parent, synonymOf

* taxonID: Primary identifer
* name: Taxonomic name e.g. Veronicastrum lungtsuanense
* authorship: Taxonomic name authorship e.g. M.Cheng & Z.J.Feng
* taxonRank: Taxonomic rank e.g. species
* status: Taxonomic status e.g. accepted
* parent: Parent taxonID of this taxon 
* synonymOf: If taxon is a synonym, the taxonID of the accepted taxon

#### Relationships

* taxa.parent -> taxa.taxonID
* taxa.synonymOf -> taxa.taxonID

## Specimens Data
### loadSpecimen.ipynb
A data loading and preprocessing script.

#### Data sources
GBIF Occurrence Download - 105,738,391 specimen records.

DOI: https://doi.org/10.15468/dl.5qqpak

#### Column definition

Columns: 'gbifID', 'occurrenceID', 'verbatimScientificName', 'verbatimScientificNameAuthorship', 'countryCode', 'locality', 'stateProvince', 'occurrenceStatus', 'decimalLatitude', 'decimalLongitude', 'day', 'month', 'year', 'basisOfRecord', 'institutionCode', 'collectionCode', 'catalogNumber', 'recordNumber', 'identifiedBy', 'dateIdentified', 'recordedBy', 'typeStatus', 'lastInterpreted', 'issue', 'bottomTaxaRank', 'bottomTaxaValue'

* gbifID: Primary identifer
* occurrenceID: A unique identifier for a particular record of an occurrence (refers to an observed evidence of an organism at a particular time and place)
* verbatimScientificName:  Exact original scientific name
* verbatimScientificNameAuthorship: Exact original scientific name authorship
* countryCode: ISO-3166 2-letter country code
* locality: Specific place where an organism was observed
* stateProvince: Name of the region or state where the observation took place
* occurrenceStatus Whether the organism is actually present or not
* decimalLatitude: Geographical decimal latitude
* decimalLongitude: Geographical decimal longitude
* day: Event day
* month: Event month
* year: Event year
* basisOfRecord: Source of the original observation or collection data
* institutionCode: Official institution short form code
* collectionCode: Collection code
* catalogNumber: Catalog number
* recordNumber: Record number
* identifiedBy: determined by - verbatim
* dateIdentified: Date of indentified
* recordedBy: collected by - verbatim
* typeStatus: Status of a specimen in defining the name of a species
* lastInterpreted: Most recent date and time when the record was processed or updated.
* issue: Potential problems or flags associated with a record
* taxonKey: unique identifier for the taxonomic classification of the organism observed.

#### Relationships
* specimens.taxonKey -> taxa.taxonID [determination]
* specimens.recordedBy -> person. [collectedBy]
* specimens.identifiedBy -> person. [determinedBy]
* specimens.institutionCode -> institutions.code
* specimens.countryCode -> country.iso

## Person (TBC)
