# Grant Data Harmonization

## Overview
This repository contains code for processing and harmonizing research grant data from multiple funding databases, creating standardized datasets for analysis and transparency. The code integrates data from:

- Europe PMC (EPMC)
- UKRI Gateway to Research
- NIHR Funding and Awards
- European Commission (EC) H2020 and Horizon programmes

## Datasets Produced

The processing generates two standardized datasets:

1. **Research projects.csv** - Harmonized grant information containing:
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
2. **Data Cleaning** - Standardize formats and handle missing values
3. **Country Assignment**:
   - EPMC: Derived from grant currency and funder information
   - UKRI: Based on regional information (mostly UK)
   - NIHR: Uses geocoordinates when direct country information is missing
   - EC: Uses provided country information
4. **Institution Handling**:
   - Prioritizes lead organizations where identified
   - Handles multiple institutions per grant where available
5. **Deduplication**:
   - Prioritizes UKRI > NIHR > EPMC data when overlaps exist
   - Drops duplicate grant IDs while preserving most complete records
6. **Column Harmonization**:
   - Standardizes column names across all sources
   - Ensures consistent data typing

## Known Limitations

- **EPMC Multi-Institutional Grants**: For the ~5.7% of grants with multiple institutions, only one institution is retained in the final dataset (may not always be the lead)
- **NIHR Country Assignment**: Uses UK geocoordinate boundaries to infer UK grants when direct country information is unreliable
- **EC Researcher Information**: Limited individual researcher information for most European Commission grants
- **Multiple Currencies**: Grant amounts are provided in original currencies without conversion
- **Organization IDs**: Inconsistent availability of organizational identifiers (ROR, internal IDs) across sources

## Data Sources

- **Europe PMC**: Biomedical research grant information
  - Source: [Europe PMC](https://europepmc.org/)
  
- **UKRI Gateway to Research**: UK Research and Innovation funded projects
  - Source: [Gateway to Research](https://gtr.ukri.org/)
  
- **NIHR Funding and Awards**: National Institute for Health and Care Research (UK)
  - Source: [NIHR Open Data](https://www.nihr.ac.uk/about-us/our-data/)
  
- **European Commission**: H2020 and Horizon Europe programmes
  - Source: [EU Funding & Tenders Portal](https://ec.europa.eu/info/funding-tenders/opportunities/portal/)

## Usage

This code was developed in Google Colab. To reproduce the datasets:

1. Upload the source files to Google Drive with the same structure as referenced in the code
2. Update file paths if needed
3. Run the notebook/script

```python
# Main processing command
python processing_raw_downloads_harmonising_and_combining_grant_data.py
```

## Note on Code Quality

This is research code developed for data processing transparency. The primary goal is reproducibility of the datasets, not production-ready software. The code handles real-world data integration challenges across disparate sources with different schemas and data quality issues.

## Citation

If you use these datasets in your research, please cite:

```
[Your citation information]
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.
