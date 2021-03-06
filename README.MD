![GitHub forks](https://img.shields.io/github/forks/wind22zhu/BioMedR.svg?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/wind22zhu/BioMedR.svg?style=social)
![CRAN/METACRAN](https://img.shields.io/cran/v/BioMedR.svg?color=green)
![GitHub repo size](https://img.shields.io/github/repo-size/wind22zhu/BioMedR.svg)
![CRAN/METACRAN](https://img.shields.io/cran/l/BioMedR.svg?color=red&style=plastic)

## Introduction

The BioMedR package offers an R package for generating various molecular descriptors for chemicals, proteins, DNAs/RNAs and their interactions. Also, this package realized some similarity searching methods and powerful clustering methods as well as several useful auxiliary tools, which aims at building integrated analysis pipelines from data acquisition, data checking, and descriptor calculation to modeling. See `vignette('BioMedR')` for the comprehensive user guide.

## Installation

To install the BioMedR package in R, simply type

   ```
   install.packages('BioMedR')
   ```
or 
   ```
   install.packages('devtools')
   library(devtools)
   install_github('wind22zhu/BioMedR')
   ```
if the installation invokes i386 arch, try to use:
   ```
   install_github('wind22zhu/BioMedR', INSTALL_opts="--no-multiarch")
   ```
To make the BioMedR package fully functional (especially the Open Babel and rjava related functionalities), we recommend the users some tips: 

[>>Common installing tips](http://projects.scbdd.com/si/install_biomedr_tips.pdf)
[>>How to install rjava](http://projects.scbdd.com/si/install_rjava.pdf)

Several dependencies of the BioMedR package may require some system-level libraries, check the corresponding manuals of these packages for detailed installation guides.
## Examples
Code snippet 1: example for getting molecules
 ```
> require('BioMedR')
> id <- c('DB00859', 'DB00860')
> SMILES <- BMgetDrug(id, 'drugbank', 'smile')
> print(SMILES[1])
 ```
Code snippet 2: example for calculating molecular descriptors
```
> require(BioMedR)
> smi_f <- system.file('vignettedata/test.smi', package = 'BioMedR')
> mol1 <- readMolFromSmi(smi_f, type = 'mol')
> des_drug <- extrDrugALOGP(mol1)
> print(des_drug[2,])
```
Code snippet 3: example for calculating sequence descriptors
```
> require(BioMedR)
> dna_seq <- readFASTA(system.file('dnaseq/hs.fasta', package = 'BioMedR'))
> des_seq <- extrDNAkmer(dna_seq[[1]])
> head(des_seq)
```
Code snippet 4: example for calculating interaction descriptors
```
> require(BioMedR)
> # results from above snippets
> drug1_mat <- as.matrix(des_drug[2,])
> drug2_mat <- as.matrix(des_drug[3,])
> seq1_mat <- t(as.matrix(des_seq))
> # Calculating
> des_CCI1 <- getCCI(drug1_mat, drug2_mat, type='combine')
> des_CDI1 <- getCDI(drug1_mat, seq1_mat, type='tensorprod')
> # Show result
> colnames(des_CCI1) = paste('CCI', 1:dim(des_CCI1)[2], sep = '_')
> rownames(des_CCI1) = paste('ID', 1:dim(des_CCI1)[1], sep = '_')
> print(des_CCI1)
```

## Features


### BioMedR implemented and integrated the state-of-the-art Chem/Bio molecular descriptors and various data modeling analysis functionalities with R. 
#### 1) For protein sequences, the BioMedR package could

  * Calculate six protein descriptor groups composed of fourteen types of commonly used structural and physicochemical descriptors that include 9920 descriptors.

  * Parallellized pairwise similarity computation derived by protein sequence alignment and Gene Ontology (GO) semantic similarity measures within a list of proteins.

#### 2) For small molecules, the BioMedR package could:

  * Calculate 307 molecular descriptors (2D/3D), including constitutional, topological, geometrical, and electronic descriptors, etc.

  * Calculate more than ten types of molecular fingerprints, including E-state fingerprints, MACCS keys, etc., and parallelized chemical similarity search.
 

#### 3) For DNA molecules, the BioMedR package could:

  * Calculate three nucleic acid composition features describing the local sequence information by means of kmers (subsequences of DNA sequences).

  * Calculate  six autocorrelation features describing the level of correlation between  two oligonucleotides along a DNA sequence in terms of their specific physicochemical properties.
 
  * Calculate two pseudo nucleotide composition features, which can be used to represent a DNA sequence with a discrete model or vector yet still keep considerable sequence order information, particularly the global or long-range sequence order information, via the physicochemical properties of its constituent oligonucleotides.

  * Parallelized pairwise similarity computation derived by fingerprints and maximum common substructure search within a list of small molecules.

#### 4) 9 kinds of descriptor classes were provided for Proteochemometric (PCM) modeling derived by Principal Components Analysis, Factor Analysis and so on. 

#### 5) By combining various types of descriptors for drugs, proteins and DNA in different methods, interaction descriptors representing protein-protein, compound-compound, DNA-DNA,  compound-DNA compound-protein and DNA-protein interactions could be conveniently generated with BioMedR, including:

  * Two types of compound-protein interaction (CPI) descriptors
  * Two types of compound-DNA interaction (CDI) descriptors 
  * Two types of DNA-protein interaction (DPI) descriptors
  * Three types of protein-protein interaction (PPI) descriptors
  * Three types of compound-compound interaction (CCI) descriptors
  * Three types of DNA-DNA interaction (DDI) descriptors

#### 6) 7 specific functionalities for similarity calculation or comparison, and 4 popular clustering analysis algorithms were implemented in BioMedR.

#### 7) Several useful auxiliary utilities are also shipped with BioMedR:

  * Parallelized molecule and protein sequence retrieval from several online databases, like PubChem, ChEMBL, KEGG, DrugBank, UniProt, RCSB PDB, genBank, etc.

  * Loading molecules stored in SMILES/SDF files and loading protein sequences from FASTA/PDB files

  * Molecular file format conversion

The computed protein sequence descriptors, molecular descriptors/fingerprints, interaction descriptors and pairwise similarities are widely used in various research fields relevant to drug disvery, primarily bioinformatics, chemoinformatics, proteochemometrics and chemogenomics.

## Publication
Jie Dong, Min-Feng Zhu, Dong-Sheng Cao, et al. BioMedR: An R/CRAN Package for Integrated Data Analysis Pipeline in Biomedical Study. *Briefings in Bioinformatics*, submitted.

## Contact

The BioMedR package is developed by Computational Biology and Drug Design Group, Central South University, China.
  
  * Dong Jie <biomed@csu.edu.cn> 

  * Minfeng Zhu <wind2zhu@163.com>

  * Dongsheng Cao <oriental-cds@163.com>

