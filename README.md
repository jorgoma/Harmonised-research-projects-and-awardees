# Grant Data Harmonization

## Overview
This repository contains code for processing and harmonising research grant data from multiple funding databases, creating standardised datasets to facilitate analyses. The code integrates data from:

- Europe PMC (EPMC)
- UKRI Gateway to Research
- NIHR Funding and Awards
- European Commission (EC) H2020 and Horizon programmes

## Note on Code Quality

This is research code developed for data processing transparency. The primary goal is reproducibility of the datasets, not production-ready software. The code handles real-world data integration challenges across disparate sources with different schemas and data quality issues.

## Datasets Produced

The processing generates two standardised datasets:

1. **Research projects.csv** - Harmonised grant information containing:
   - Grant IDs and titles
   - Abstracts
   - Funding organizations
   - Lead institutions with IDs where available
   - Countries
   - Start/end dates
   - Funding amounts with currencies

2. **Research projects awardees.csv** - Associated researchers and institutions:
   - Researcher names
   - Researcher IDs (ORCID, person_id)
   - Affiliated organizations
   - Roles in projects
   - Associated grant IDs

## Methodology

The data processing workflow performs the following steps:

1. **Data Acquisition** - Load raw data from each source
2. **Data Cleaning** - Standardise formats and handle missing values
3. **Country Assignment**:
   - EPMC: Derived from grant currency and funder information
   - UKRI: Based on regional information (mostly UK)
   - NIHR: Uses geocoordinates when direct country information is missing
   - EC: Uses provided country information
4. **Institution Handling**:
   - Prioritises lead organizations where identified
   - Handles multiple institutions per grant where available
5. **Deduplication**:
   - Prioritizes UKRI > NIHR > EPMC data when overlaps exist
   - Drops duplicate grant IDs while preserving most complete records
6. **Column Harmonisation**:
   - Standardises column names across all sources
   - Identifies minimum set of common columns

## Known Limitations

- **EPMC Multi-Institutional Grants**: For the ~5.7% of grants with multiple institutions, only one institution is retained in the final dataset (may not always be the lead)
- **NIHR Country Assignment**: Uses UK geocoordinate boundaries to infer UK grants when direct country information is unreliable
- **EC Researcher Information**: Limited individual researcher information for most European Commission grants
- **Multiple Currencies**: Grant amounts are provided in original currencies without conversion
- **Organisation IDs**: Inconsistent availability of organisational identifiers (ROR, internal IDs) across sources

## Data Sources

- **Europe PMC**: Biomedical research grant information
  - Source: [Europe PMC](https://europepmc.org/)
  
- **UKRI Gateway to Research**: UK Research and Innovation funded projects
  - Source: [Gateway to Research](https://gtr.ukri.org/)
  
- **NIHR Funding and Awards**: National Institute for Health and Care Research (UK)
  - Source: [NIHR Funding and Awards](https://fundingawards.nihr.ac.uk/)
  
- **European Commission**: H2020 and Horizon Europe programmes
  - Source: [EC's bulk downloads](https://data.europa.eu/data/datasets/cordish2020projects?locale=en)

## Usage

This code was developed in Google Colab. To reproduce the datasets:

1. Upload the source files to Google Drive with the same structure as referenced in the code
2. Update file paths if needed
3. Run the notebook/script

## Linkage to Zenodo

If you are just interested in the final datasets, please find the information in the Zenodo upload with DOI:10.5281/zenodo.15479412


## License

This project is licensed under the Creative Commons Attribution 4.0 International
