[![CRAN\_Status\_Badge](https://www.r-pkg.org/badges/version/mixedSCGLR)](https://cran.r-project.org/package=mixedSCGLR)

# mixedSCGLR
Supervised Component Generalised Linear Regression for mixed models

An extension of the Schall's algorithm to combine Supervised-Component regression with GLMM estimation in the multivariate context.

## Installation

``` r
# Dependencies
if (!("Rcpp" %in% installed.packages())) install.packages("Rcpp")
if (!("SCGLR" %in% installed.packages())) install.packages("SCGLR")
if (!("ggplot2" %in% installed.packages())) install.packages("ggplot2")
if (!("plsdepot" %in% installed.packages())) install.packages("plsdepot")

# Install release version from CRAN
install.packages("mixedSCGLR")

# Install development version from GitHub
devtools::install_github("SCnext/mixedSCGLR")
```
## Example

``` r
library(mixedSCGLR)
# load sample data
data(dataGen)
k.opt=4
s.opt=0.1
l.opt=10
withRandom.opt=kCompRand(Y=dataGen$Y, family=rep("poisson", ncol(dataGen$Y)),
                        X=dataGen$X, AX=dataGen$AX,
                        random=dataGen$random, loffset=log(dataGen$offset), k=k.opt,
                        init.sigma = rep(1, ncol(dataGen$Y)), init.comp = "pca",
                        method=SCGLR::methodSR("vpi", l=l.opt, s=s.opt,
                                        maxiter=1000, epsilon=10^-6, bailout=1000))
plot(withRandom.opt, pred=TRUE, plane=c(1,2), title="Component plane (1,2)",
     threshold=0.7, covariates.alpha=0.4, predictors.labels.size=6)
```

![](https://i.imgur.com/rTUqFBx.png)

<sup>Created on 2018-11-29 by the [reprex package](https://reprex.tidyverse.org) (v0.2.1)</sup>
