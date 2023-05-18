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

