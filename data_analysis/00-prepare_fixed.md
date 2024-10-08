---
title: "Prepare scRNA-Seq analysis"
author: "UC Davis Bioinformatics Core"
date: "2024-08-27"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
---


### Create a new RStudio project

Open RStudio and create a new project, for more info see [Using-Projects](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects):

*File > New Project > New Directory > New Project*

Name the new workshop directory (e.g. scRNA_analysis), and check "use renv with this project" if present.

Learn more about [renv](https://rstudio.github.io/renv/articles/renv.html).

### Install packages
One of R's many benefits is the large, active user community, which produces and maintains many packages that extend the functionality of base R and provide functions that enable bioinformatic analyses without completely custom code.

The following package installation commands should be run individually, **in the R console**. Many of them will require your input to determine which, if any, dependencies should be updated; for the quickest result, attempt 'n' (none) first.

#### R-universe for arm64 installations

r-universe is a new umbrella project by __rOpenSci__. It uses cross-compiling for arm64 binaries.

<span style="color:blue">For those who are using Macs that have M1/M2/M3 chips, if you have trouble installing the packages and get error that is similar to "ld: warning: ignoring file '/Library/Frameworks/R.framework/Versions/4.4-arm64/Resources/lib/libR.dylib': found architecture 'arm64', required architecture 'x86_64'", please go to https://r-universe.dev/search/ and search for the packages and use the installation instructions provided there.</span>

#### BiocManager
BiocManager is an interface for the bioinformatics-specific R package repository. We will be using BiocManager to install other packages when possible, rather than the base R function install.packages.

``` r
if (!requireNamespace("BiocManager", quietly = TRUE)){
    install.packages("BiocManager")
}
<div class='r_output'>
 rmarkdown
The rmarkdown package, when used with others like tinytex and knitr, allows you to knit your Rmd document to nicely-formatted reports.

``` r
if (!any(rownames(installed.packages()) == "rmarkdown")){
  BiocManager::install("rmarkdown")
}
library(rmarkdown)
</div>
#### tinytex
TinyTeX is a small LaTeX distribution for use with R.

``` r
if (!any(rownames(installed.packages()) == "tinytex")){
  BiocManager::install("tinytex")
}
library(tinytex)
<div class='r_output'>
 knitr

``` r
if (!any(rownames(installed.packages()) == "knitr")){
  BiocManager::install("knitr")
}
library(knitr)
</div>
#### kableExtra
The kableExtra package gives the user fine-grained control over table formats. This is useful for knit reports.

``` r
if (!any(rownames(installed.packages()) == "kableExtra")){
  BiocManager::install("kableExtra")
}
library(kableExtra)
<div class='r_output'>
 ggplot2
An extremely popular package by the authors of RStudio, ggplot2 produces highly customizable plots.

``` r
if (!any(rownames(installed.packages()) == "ggplot2")){
  BiocManager::install("ggplot2")
}
library(ggplot2)
</div>
#### dplyr
Like ggplot2 and tidyr, dplyr is part of the "tidyverse" by the RStudio authors: a group of packages designed for data analysis and visualization.

``` r
if (!any(rownames(installed.packages()) == "dplyr")){
  BiocManager::install("dplyr")
}
library(dplyr)
<div class='r_output'>
 tidyr

``` r
if (!any(rownames(installed.packages()) == "tidyr")){
  BiocManager::install("tidyr")
}
library(tidyr)
</div>
#### viridis
viridis produces accessible color palettes.

``` r
if (!any(rownames(installed.packages()) == "viridis")){
  BiocManager::install("viridis")
}
library(viridis)
<div class='r_output'>
 hdf5r
HDF5 (heirarchical data format version five) files can be used to store single cell expression data (including output from Cell Ranger). The hdf5r package provides utilities for interacting with the format.

``` r
if (!any(rownames(installed.packages()) == "hdf5r")){
  BiocManager::install("hdf5r")
}
library(hdf5r)
</div>
#### Seurat
Seurat is an extensive package for the analysis of single cell experiments, from normalization to visualization.

``` r
if (!any(rownames(installed.packages()) == "Seurat")){
  BiocManager::install("Seurat")
}
library(Seurat)
<div class='r_output'>
 ComplexHeatmap
ComplexHeatmap produces beautiful, highly-customizable heat maps.

``` r
if (!any(rownames(installed.packages()) == "ComplexHeatmap")){
  BiocManager::install("ComplexHeatmap")
}
library(ComplexHeatmap)
</div>
#### biomaRt
This package provides an interface to Ensembl databases.

``` r
if (!any(rownames(installed.packages()) == "biomaRt")){
  BiocManager::install("biomaRt")
}
library(biomaRt)
<div class='r_output'>
 org.Hs.eg.db
org.Hs.eg.db contains genome-wide annotation based on Entrez Gene identifiers in the Human genome.

``` r
if (!any(rownames(installed.packages()) == "org.Hs.eg.db")){
  BiocManager::install("org.Hs.eg.db")
}
library(org.Hs.eg.db)
</div>
#### limma
Originally developed for microarray data, limma provides functions for linear modeling and differential expression.

``` r
if (!any(rownames(installed.packages()) == "limma")){
  BiocManager::install("limma")
}
library(limma)
<div class='r_output'>
 topGO
Test gene ontology (GO) term enrichment while accounting for the topology of the GO graph.

``` r
if (!any(rownames(installed.packages()) == "topGO")){
  BiocManager::install("topGO")
}
library(topGO)
</div>
#### remotes
Some packages (or versions of packages) cannot be installed through Bioconductor. The remotes package contains tools for installing packages from a number of repositories, including GitHub.

``` r
if (!any(rownames(installed.packages()) == "remotes")){
  utils::install.packages("remotes")
}
library(remotes)
<div class='r_output'>
 ape
Analysis of Phylogenetics and Evolution (ape) is used to generate and manipulate phylogenetic trees. In this workshop, we will be using ape to investigate the relationships between clusters.

``` r
if (!any(rownames(installed.packages()) == "ape")){
  utils::install.packages("ape")
}
library(ape)
</div>
#### DoubletFinder
DoubletFinder detects multiplets within single cell or nucleus data.

``` r
if (!any(rownames(installed.packages()) == "DoubletFinder")){
  remotes::install_github('chris-mcginnis-ucsf/DoubletFinder')
}
library(DoubletFinder)
<div class='r_output'>
 openxlsx
The openxlsx package is a suite of tools for reading and writing .xlsx files.

``` r
if (!any(rownames(installed.packages()) == "openxlsx")){
  BiocManager::install("openxlsx")
}
library(openxlsx)
</div>
#### HGNChelper
Both R and Excel can introduce changes to gene symbols. HGNChelper can correct gene symbols that have been altered, and convert gene symbols to valid R names.

``` r
if (!any(rownames(installed.packages()) == "HGNChelper")){
  BiocManager::install("HGNChelper")
}
library(HGNChelper)
<div class='r_output'>

 Expression matrix

Move the downloaded dataset to the RStudio Project folder.

If the zip file isn't extracted yet you can extrct it on the R terminal.

In Rstudio, navigate to the terminal tab (next to the console). This gives you access to a bash terminal. Run the following code:

``` bash
unzip 01-CellRanger.zip
</div>
When the download and extraction are complete, you should see three folder: 01-CellRanger


### Download materials and prepare for the next section

In the R console run the following command to download part 1 of data analysis.

#### Markdown template document

``` r
download.file("https://raw.githubusercontent.com/ucsf-cat-bioinformatics/2024-08-SCRNA-Seq-Analysis/main/data_analysis/01-create_object.Rmd", "01-create_object2.Rmd")
<div class='r_output'> Verfiy installation
Finally, we can get the session info to ensure that all of the packages were installed and loaded correctly.

``` r
sessionInfo()
</div>

