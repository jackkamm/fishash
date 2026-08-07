# fishash

## Introduction

`fishash` is an R package for calling guides in perturbseq data from
UMI counts, based on treating the count matrix as a contingency table.

For each cell barcode and guide barcode, `fishash` tests how likely
the 2 barcodes are to co-occur in reads.  More specifically, it tests
whether the 2 barcodes have an odds ratio greater than 1 using a
one-sided Fisher's exact test. The method also includes a procedure to
correct for hidden confounding due to Simpson's paradox, and performs
a block-dependence-aware multiple testing correction (assuming that
tests from different cells are independent, but tests within a cell
are dependent).

See our
[preprint](https://www.biorxiv.org/content/10.64898/2026.01.22.701179)
for a full description of the method.

## Installation

To install the package, do:
```{R}
devtools::install_github("jackkamm/fishash")
```

Fishash will also become available in the next version of Bioconductor
(3.24). After Bioconductor 3.24 is released (or if you are on the
[devel](https://contributions.bioconductor.org/use-devel.html) version), you can install it with:
```{R}
BiocManager::install("fishash")
```

## Basic usage

Given a count matrix `counts_mat` with guides for rows and cells for
columns, you can assign the guides calling the `fishash()` function:

```{R}
library(fishash)

# returns a SummarizedExperiment
res_fishash <- fishash(counts_mat)

# for the first few cells, print whether they received 0, 1, or 2+ guides:
head(colData(res_fishash)$demux_type)

# print the assigned guides for the first few cells
head(colData(res_fishash)$assignment)
```

For more options, see the help page:

```{R}
help(fishash)
```

## Vignette

See the
[vignette](https://jackkamm.github.io/fishash-vignette.html)
for an example on how to use the package.
