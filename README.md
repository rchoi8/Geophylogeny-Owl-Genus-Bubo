# Geophylogeny of the Owl and Eagle-Owl Genus *Bubo*

This project investigates the phylogenetic relationships and geographic distributions of horned owls and eagle-owls belonging to the genus *Bubo*. Using mitochondrial COI sequences, sequence cleaning, alignment, consensus building, phylogenetic reconstruction, and geospatial mapping, the study examines whether sister species inhabit similar or distinct regions. By integrating phylogeny with latitude and longitude data, this project visualizes evolutionary patterns alongside species distributions to assess ecological and biogeographical relationships.

## Table of Contents
- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Data Sources](#data-sources)
- [Requirements](#requirements)
- [Usage](#usage)
- [Analysis Workflow](#analysis-workflow)
- [References](#references)

## Introduction
Species within the owl genus *Bubo* (horned owls and eagle-owls) are ecologically important apex predators and indicators of environmental health. Understanding whether closely related species occupy similar or different geographic regions provides insight into ecological adaptation, evolutionary divergence, and conservation needs.  
In this project, COI gene sequences for *Bubo* species were obtained from NCBI using automated queries. After quality filtering, alignment, and consensus sequence generation, a phylogenetic tree was built to identify sister-species relationships. These phylogenetic relationships were then integrated with species occurrence data from the BOLD database to construct a geophylogeny that maps evolutionary history onto global distribution patterns.

This project evaluates:
- **phylogenetic relationships among *Bubo* species**,  
- **whether sister species inhabit similar or distinct regions**,  
- **how phylogeny and geography jointly reflect evolutionary and ecological processes**.

## Project Structure
- `data/`:  
  COI FASTA sequences, metadata tables, and geographic occurrence data for *Bubo* species.

- `scripts/`:  
  R Markdown file (`.Rmd`) containing the full workflow, including NCBI retrieval, cleaning, consensus building, alignment, phylogeny, and mapping.

- `figures/`:  
  Phylogenetic tree of *Bubo*, geophylogeny map, and sequence length histograms.

- `README.md`:  
  Project overview and instructions.

## Data Sources
1. **NCBI Nucleotide Database (GenBank)**  
   COI mitochondrial sequences for the genus *Bubo*, retrieved using the `rentrez` R package (queried October 2024).  
   Search filters included:
   - Taxon: *Bubo*
   - Gene: COI / CO1 / COX1
   - Batch retrieval using web history for large queries

2. **BOLD Systems Database**  
   Geographic occurrence data (species name, latitude, longitude) downloaded from the BOLD API (retrieved October 18, 2024).

## Requirements
- **R (version 4.0 or higher)**

### Required R Packages  
`tidyverse`, `rentrez`, `Biostrings`, `DECIPHER`, `muscle`, `ape`, `msa`, `ggplot2`, `stringr`

## Usage
1. **Data Retrieval**: Query NCBI for COI sequences of *Bubo* using `rentrez` and retrieve metadata from batch summaries.
2. **Quality Control**: Remove sequences with excessive ambiguity, trim Ns, and filter by sequence length to obtain homologous sequences.
3. **Sequence Alignment**: Align sequences using MUSCLE and inspect alignments using `BrowseSeqs`.
4. **Consensus Construction**: Generate consensus sequences for species with multiple records and clean ambiguous bases.
5. **Phylogenetic Reconstruction**: Build a phylogenetic tree using distance-based methods and convert output to `phylo` format.
6. **Geographic Data Processing**: Extract, filter, and standardize BOLD geographic coordinates for relevant *Bubo* species.
7. **Geophylogeny Mapping**: Use `phylo.to.map()` to project the phylogenetic tree onto global coordinates and visualize species distributions.

## Analysis Workflow
1. **Sequence Acquisition and Metadata Retrieval**
   - Query NCBI for COI records of *Bubo*.  
   - Collect IDs and metadata using batch processing.

2. **Sequence Filtering and Cleaning**
   - Remove leading/trailing Ns.  
   - Filter sequences with >1% internal ambiguity.  
   - Accept only sequences near the median length.

3. **Sequence Alignment and Consensus Building**
   - Align sequences using MUSCLE.  
   - Create consensus sequences for species with multiple samples.  
   - Standardize species naming.

4. **Distance Calculation and Phylogeny**
   - Convert sequences to `DNAbin`.  
   - Compute distances using the TN93 model.  
   - Build a phylogenetic tree (TreeLine → phylo).

5. **Geographic Data Preparation**
   - Import species occurrence data from BOLD.  
   - Clean missing values and standardize species names.  
   - Convert coordinates to matrix format.

6. **Geophylogeny Construction**
   - Integrate the phylogenetic tree with coordinates using `phylo.to.map()`.  
   - Plot evolutionary relationships alongside species distributions.

## References
- [IUCN Red List](https://www.iucnredlist.org/)  
- [NCBI GenBank](https://www.ncbi.nlm.nih.gov/genbank/)  
- [BOLD Systems](https://www.boldsystems.org/)  
