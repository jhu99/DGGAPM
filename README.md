# DGGAPM: Efficient Inference of Direct Gene–Gene Associations via High-Dimensional Precision Matrix with Rigorous FDR Control

![](https://img.shields.io/github/r-package/v/jhu99/DGGAPM)
![](https://img.shields.io/github/license/jhu99/DGGAPM)
[![](https://img.shields.io/github/downloads/jhu99/DGGAPM/latest/total)](https://github.com/jhu99/DGGAPM/graphs/traffic)
![](https://img.shields.io/github/stars/jhu99/DGGAPM?style=social)


&emsp;&emsp;We propose a novel method, dGGAPM (Direct Gene-Gene Associations via Precision Matrix), which reconstructs gene coexpression networks by statistically inferring direct gene-gene relationships. Unlike conventional approaches that rely on pairwise correlation measures and may capture indirect associations, dGGAPM leverages high-dimensional precision matrix to more accurately characterize direct interactions while controlling for the influence of all other genes. The main contributions of this research are threefold. First, in contrast to existing methods, we construct the high-dimensional gene network using an estimated precision matrix, providing a rigorous and principled foundation for statistical inference of gene–gene relationships. Second, we recover the network structure through a high-dimensional multiple testing procedure that takes advantage of the asymptotic properties of the precision matrix estimator. Finally, we introduce a data-driven thresholding strategy that achieves strict false discovery rate (FDR) control, ensuring reliable identification of coexpression links in high-dimensional settings. 

## Installation

For installation please use the following codes in R:

```R
install_github("jhu99/DGGAPM")
install.packages("scalreg")
```

## Example

In this example, it calculates estimated precision matrix for a set of $100$ genes across $421$ single cells using gene expression data from mouse embryonic stem cells:
```R
library(DGGAPM)
load('data/expressionData.rda')
p <- 100
h <- 4
res<-dggapm(A,100,4)
R <- res[[1]]      # a precision matrix
adj <- res[[2]]    # a binary adjacency matrix
```
The output includes a precision matrix and a binary adjacency matrix representing the gene co-expression network edges.

### Input of DGGAPM

`A` : A $p \times n$ matrix of gene expression data, where $p$ is the number of genes (here, $100$) and $n$ is the number of cells (here, $421$).

`p` : The number of genes involved in the calculation.

`h` : A regularization parameter controlling the sparsity and stability of the model coefficients (here, $h = 4$).

### Output of DGGAPM

The output of DGGAPM consists of a $p \times p$ estimated precision matrix $R$ with the format:
```
 1.0000000000 -0.024134294 -6.447580e-02  0.0414261210  ...
-0.0241342944  1.000000000  1.771790e-01  0.0129375893  ...
-0.0644757959  0.177178995  1.000000e+00  0.0562895332  ...
 . 
 .
 .
```
where $R\[i,j\]$ represents the partial correlation between gene $i$ and gene $j$.

Based on adaptive thresholding, this correlation matrix can be further transformed into a binary adjacency matrix $adj$, where each entry indicates the presence ($1$) or absence ($0$) of an edge between two genes in the inferred co-expression network:
```
1  0  0  0 ...
0  1  1  0 ...
0  1  1  0 ...
. 
.
.
```

## Applications

The experimental code implementation in the paper can be viewed in applications folder.


